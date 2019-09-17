# String、StringBuffer、StringBuilder的区别
返回[README.md](./../../README.md)

---
目录
<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=6 orderedList=false} -->
<!-- code_chunk_output -->

* [联系与区别](#联系与区别)
	* [String 和 StringBuffer：](#string-和-stringbuffer)
	* [StringBuilder](#stringbuilder)
* [使用策略](#使用策略)
* [引用](#引用)
* [返回目录](#返回目录)

<!-- /code_chunk_output -->

---
## 联系与区别
- 都是final类，都不允许被继承；
- String类长度是不可变的，StringBuffer和StringBuilder类长度是可以改变的；
- StringBuffer类是线程安全的，StringBuilder不是线程安全的

### String 和 StringBuffer：
- String是不可变的对象。
```
String -> 改变长度 -> 新建String -> 指针指向新的String
```
- 对StringBuffer对象本身进行操作，而不是生成新的对象并改变对象引用。
- 在某些情况下，String对象的字符串拼接其实是被Java Compiler编译成了StringBuffer对象的拼接，所以这些时候String对象的速度并不会比StringBuffer对象慢。
```java
String s1 = “This is only a” + “ simple” + “ test”;
StringBuffer Sb = new StringBuilder(“This is only a”).append(“ simple”).append(“ test”);

//Java Compiler直接把上述第一条语句编译为：

String s2 = “This is only a”;

String s3 = “ simple”;

String s4 = “ test”;

String s1 = s2 + s3 + s4;
//这时候，Java Compiler会规规矩矩的按照原来的方式去做，String的concatenation（即+）操作利用了StringBuilder（或StringBuffer）的append方法实现，此时，对于上述情况，若s2，s3，s4采用String定义，拼接时需要额外创建一个StringBuffer（或StringBuilder），之后将StringBuffer转换为String；若采用StringBuffer（或StringBuilder），则不需额外创建StringBuffer
```

### StringBuilder
如果可能，建议优先采用该类，因为在大多数实现中，它比 StringBuffer 要快。但不保证同步。

## 使用策略
- 基本原则：如果要操作少量的数据，用String ；单线程操作大量数据，用StringBuilder ；多线程操作大量数据，用StringBuffer。
- 不要使用String类的”+”来进行频繁的拼接，因为那样的性能极差的，应该使用StringBuffer或StringBuilder类，这在Java的优化上是一条比较重要的原则。
- StringBuilder一般使用在方法内部来完成类似”+”功能，因为是线程不安全的，所以用完以后可以丢弃。StringBuffer主要用在全局变量中。
- 除非确定系统的瓶颈是在 StringBuffer 上，并且确定你的模块不会运行在多线程模式下，才可以采用StringBuilder；否则还是用StringBuffer。
- 为了获得更好的性能，在构造 StringBuffer 或 StringBuilder 时应尽可能指定它们的容量。当然，如果你操作的字符串长度（length）不超过 16 个字符就不用了，当不指定容量（capacity）时默认构造一个容量为16的对象。不指定容量会显著降低性能。

---
## 引用
[Java String、StringBuffer 和 StringBuilder 的区别
](http://www.runoob.com/w3cnote/java-different-of-string-stringbuffer-stringbuilder.html)

---
## 返回目录
[README.md](./../../README.md)
