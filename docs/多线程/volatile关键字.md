# volatile

<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=6 orderedList=false} -->
<!-- code_chunk_output -->

* [volatile 的作用](#volatile-的作用)
* [volatile 的应用](#volatile-的应用)
	* [双重检查锁的单例模式](#双重检查锁的单例模式)
	* [控制停止线程的标记](#控制停止线程的标记)

<!-- /code_chunk_output -->

## volatile 的作用

1. 保证内存可见性
   - 当线程A更新了 volatile 修饰的变量时，它会立即刷新到主线程
   - 将其余缓存中该变量的值清空，导致其余线程只能去主内存读取最新值。
2. 保证代码执行顺序
   - 写操作肯定是在读操作之前，也就是说读取的值肯定是最新的。
3. **不能保证原子性**。

## volatile 的应用

### 双重检查锁的单例模式

```java
public class Singleton {
  private static volatile Singleton singleton;

  private Singleton() {
  }

  public static Singleton getInstance() {
    if (singleton == null) {
      synchronized (Singleton.class) {
        if (singleton == null) {
          singleton = new Singleton();
        }
      }
    }
    return singleton;
  }
}
```

这里的 `volatile` 关键字主要是为了防止指令重排。 如果不用 `volatile` ，`singleton = new Singleton();`，这段代码其实是分为三步：

- 分配内存空间。(1)
- 初始化对象。(2)
- 将 `singleton` 对象指向分配的内存地址。(3)

加上 `volatile` 是为了让以上的三步操作顺序执行，反之有可能第三步在第二步之前被执行就有可能导致某个线程拿到的单例对象还没有初始化，以致于使用报错。

### 控制停止线程的标记

```java
private volatile boolean flag ;
private void run(){
  new Thread(new Runnable() {
    @Override
    public void run() {
      while (flag) {
        doSomeThing();
      }
    }
  });
}

private void stop(){
  flag = false ;
}
```
