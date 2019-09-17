# int和Integer的区别

返回[README.md](./../../README.md)

---
目录
<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=6 orderedList=false} -->
<!-- code_chunk_output -->
* [区别](#区别)
* [区别](#区别)
* [Integer 和 int 大小比较](#integer-和-int-大小比较)
* [引用](#引用)
* [返回目录](#返回目录)

<!-- /code_chunk_output -->

---
## 区别
- Integer是int的包装类，int则是java的一种基本数据类型
- Integer变量必须实例化后才能使用，而int变量不需要
- Integer实际是对象的引用，当new一个Integer时，实际上是生成一个指针指向此对象；而int则是直接存储数据值
- Integer的默认值是null，int的默认值是0
## Integer 和 int 大小比较
- 两个通过new生成的Integer变量永远是不相等的（因为new生成的是两个对象，其内存地址不同）
```java
Integer a = new Integer(100);
Integer b = new Integer(100);
System.out.print(a == b); //false
```
- Integer变量和int变量比较时，只要两个变量的值是向等的，则结果为true
```java
Integer a = new Integer(999);
int b = 999;
System.out.print(a == b); //true
```
> 包装类Integer和基本数据类型int比较时，java会自动拆包装为int，然后进行比较，实际上就变为两个int变量的比较

- 非new生成的Integer变量和new Integer()生成的变量比较时，结果为false。
```java
Integer a = new Integer(100);
Integer b = 100;
System.out.print(a == b); //false
```
> 非new生成的Integer变量指向的是java常量池中的对象，而new Integer()生成的变量指向堆中新建的对象，两者在内存中的地址不同

- 对于两个非new生成的Integer对象，进行比较时，如果两个变量的值在区间-128到127之间，则比较结果为true，如果两个变量的值不在此区间，则比较结果为false

```java
Integer a = 100;
Integer b = 100;
System.out.print(a == b); //true
```
```java
Integer a = 128;
Integer b = 128;
System.out.print(a == b); //false
```
原因如下
```java
public static Integer valueOf(int i){
    assert IntegerCache.high >= 127;
    if (i >= IntegerCache.low && i <= IntegerCache.high){
        return IntegerCache.cache[i + (-IntegerCache.low)];
    }
    return new Integer(i);
}
```
> java对于-128到127之间的数，会进行缓存，Integer i = 127时，会将127进行缓存，下次再写Integer j = 127时，就会直接从缓存中取，就不会new了

---
## 引用
[java面试题之int和Integer的区别](https://www.cnblogs.com/guodongdidi/p/6953217.html)

---
## 返回目录
[README.md](./../../README.md)
