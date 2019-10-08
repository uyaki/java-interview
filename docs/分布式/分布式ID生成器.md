# 分布式ID生成器

一个唯一 ID 在一个分布式系统中是非常重要的一个业务属性，其中包括一些如订单 ID，消息 ID ，会话 ID，他们都有一些共有的特性：

- 全局唯一。
- 趋势递增。

全局唯一很好理解，目的就是唯一标识某个次请求，某个业务。

通常有以下几种方案：

## 基于数据库

可以利用 `MySQL` 中的自增属性 `auto_increment` 来生成全局唯一 ID，也能保证趋势递增。 但这种方式太依赖 DB，如果数据库挂了那就非常容易出问题。

### 水平扩展改进

但也有改进空间，可以将数据库水平拆分，如果拆为了两个库 A 库和 B 库。 A 库的递增方式可以是 `0 ,2 ,4 ,6`。B 库则是 `1 ,3 ,5 ,7`。这样的方式可以提高系统可用性，并且 ID 也是趋势递增的。

但也有如下一下问题：

- 想要扩容增加性能变的困难，之前已经定义好了 A B 库递增的步数，新加的数据库不好加入进来，水平扩展困难。
- 也是强依赖与数据库，并且如果其中一台挂掉了那就不是绝对递增了。

## 本地 UUID 生成

还可以采用 `UUID` 的方式生成唯一 ID，由于是在本地生成没有了网络之类的消耗，所有效率非常高。

但也有以下几个问题：

- 生成的 ID 是无序性的，不能做到趋势递增。
- 由于是字符串并且不是递增，所以不太适合用作主键。

## 采用本地时间

这种做法非常简单，可以利用本地的毫秒数加上一些业务 ID 来生成唯一ID，这样可以做到趋势递增，并且是在本地生成效率也很高。

但有一个致命的缺点:当并发量足够高的时候**唯一性**就不能保证了。

## Twitter 雪花算法

可以基于 `Twitter` 的 `Snowflake` 算法来实现。它主要是一种划分命名空间的算法，将生成的 ID 按照机器、时间等来进行标志。

### 原理

SnowFlake算法产生的ID是一个64位的整型，结构如下（每一部分用“-”符号分隔）：



**0 - 0000000000 0000000000 0000000000 0000000000 0 - 00000 - 00000 - 000000000000**



**1位标识部分**，在java中由于long的最高位是符号位，正数是0，负数是1，一般生成的ID为正数，所以为0；

**41位时间戳部分**，这个是毫秒级的时间，一般实现上不会存储当前的时间戳，而是时间戳的差值（当前时间-固定的开始时间），这样可以使产生的ID从更小值开始；41位的时间戳可以使用69年，(1L << 41) / (1000L * 60 * 60 * 24 * 365) = 69年；

**10位节点部分**，Twitter实现中使用前5位作为数据中心标识，后5位作为机器标识，可以部署1024个节点；

**12位序列号部分**，支持同一毫秒内同一个节点可以生成4096个ID；



SnowFlake算法生成的ID大致上是按照时间递增的，用在分布式系统中时，需要注意数据中心标识和机器标识必须唯一，这样就能保证每个节点生成的ID都是唯一的。或许我们不一定都需要像上面那样使用5位作为数据中心标识，5位作为机器标识，可以根据我们业务的需要，灵活分配节点部分，如：若不需要数据中心，完全可以使用全部10位作为机器标识；若数据中心不多，也可以只使用3位作为数据中心，7位作为机器标识。

```java
public class SnowFlake {
 
    /**
    * 起始的时间戳
    */
    private final static long START_STMP = 1480166465631L;
 
    /**
    * 每一部分占用的位数
    */
    private final static long SEQUENCE_BIT = 12; //序列号占用的位数
    private final static long MACHINE_BIT = 5;  //机器标识占用的位数
    private final static long DATACENTER_BIT = 5;//数据中心占用的位数
 
    /**
    * 每一部分的最大值
    */
    private final static long MAX_DATACENTER_NUM = -1L ^ (-1L << DATACENTER_BIT);
    private final static long MAX_MACHINE_NUM = -1L ^ (-1L << MACHINE_BIT);
    private final static long MAX_SEQUENCE = -1L ^ (-1L << SEQUENCE_BIT);
 
    /**
    * 每一部分向左的位移
    */
    private final static long MACHINE_LEFT = SEQUENCE_BIT;
    private final static long DATACENTER_LEFT = SEQUENCE_BIT + MACHINE_BIT;
    private final static long TIMESTMP_LEFT = DATACENTER_LEFT + DATACENTER_BIT;
 
    private long datacenterId;  //数据中心
    private long machineId;    //机器标识
    private long sequence = 0L; //序列号
    private long lastStmp = -1L;//上一次时间戳
 
    public SnowFlake(long datacenterId, long machineId) {
        if (datacenterId > MAX_DATACENTER_NUM || datacenterId < 0) {
            throw new IllegalArgumentException("datacenterId can't be greater than MAX_DATACENTER_NUM or less than 0");
        }
        if (machineId > MAX_MACHINE_NUM || machineId < 0) {
            throw new IllegalArgumentException("machineId can't be greater than MAX_MACHINE_NUM or less than 0");
        }
        this.datacenterId = datacenterId;
        this.machineId = machineId;
    }
 
    /**
    * 产生下一个ID
    *
    * @return
    */
    public synchronized long nextId() {
        long currStmp = getNewstmp();
        if (currStmp < lastStmp) {
            throw new RuntimeException("Clock moved backwards.  Refusing to generate id");
        }
 
        if (currStmp == lastStmp) {
            //相同毫秒内，序列号自增
            sequence = (sequence + 1) & MAX_SEQUENCE;
            //同一毫秒的序列数已经达到最大
            if (sequence == 0L) {
                currStmp = getNextMill();
            }
        } else {
            //不同毫秒内，序列号置为0
            sequence = 0L;
        }
 
        lastStmp = currStmp;
 
        return (currStmp - START_STMP) << TIMESTMP_LEFT //时间戳部分
                | datacenterId << DATACENTER_LEFT      //数据中心部分
                | machineId << MACHINE_LEFT            //机器标识部分
                | sequence;                            //序列号部分
    }
 
    private long getNextMill() {
        long mill = getNewstmp();
        while (mill <= lastStmp) {
            mill = getNewstmp();
        }
        return mill;
    }
 
    private long getNewstmp() {
        return System.currentTimeMillis();
    }
 
}
```

