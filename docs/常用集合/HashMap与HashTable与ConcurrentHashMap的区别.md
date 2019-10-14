# HashMap与HashTable与ConcurrentHashMap的区别

<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=6 orderedList=false} -->
<!-- code_chunk_output -->

* [HashMap源码解析](#hashmap源码解析)
* [HashMap与HashTable](#hashmap与hashtable)
* [结论](#结论)
* [参考链接](#参考链接)

<!-- /code_chunk_output -->
## HashMap源码解析
请先阅读 [HashMap源码解析](https://gknoone.github.io/java-interview/#/常用集合/HashMap源码解析)

## HashMap与HashTable

- HashTable和HashMap都实现了Map接口，但是HashTable的实现是基于Dictionary抽象类
- 在HashMap中，null可以作为键，这样的键只有一个；可以有一个或多个键所对应的值为null。当get()方法返回null值时，既可以表示HashMap中没有该键，也可以表示该键所对应的值为null。因此，在HashMap中不能由get()方法来判断HashMap中是否存在某个键，而应该用`containsKey()`方法来判断。而在HashTable中，无论是key还是value都不能为null。
> 主要的区别有：线程安全性，同步(synchronization)，以及速度。

- HashMap几乎可以等价于Hashtable，除了HashMap是非synchronized的，并可以接受null(HashMap可以接受为null的键值(key)和值(value)，而Hashtable则不行)。
- HashMap是非synchronized，而Hashtable是synchronized，这意味着Hashtable是线程安全的，多个线程可以共享一个Hashtable；而如果没有正确的同步的话，多个线程是不能共享HashMap的。Java 5提供了ConcurrentHashMap，它是HashTable的替代，比HashTable的扩展性更好。
- 另一个区别是HashMap的迭代器(Iterator)是fail-fast迭代器，而Hashtable的enumerator迭代器不是fail-fast的。所以当有其它线程改变了HashMap的结构（增加或者移除元素），将会抛出ConcurrentModificationException，但迭代器本身的remove()方法移除元素则不会抛出ConcurrentModificationException异常。但这并不是一个一定发生的行为，要看JVM。这条同样也是Enumeration和Iterator的区别。
- 由于Hashtable是线程安全的也是synchronized，所以在单线程环境下它比HashMap要慢。如果你不需要同步，只需要单一线程，那么使用HashMap性能要好过Hashtable。
- HashMap不能保证随着时间的推移Map中的元素次序是不变的。

> 要注意的一些重要术语：
1. sychronized意味着在一次仅有一个线程能够更改Hashtable。就是说任何线程要更新Hashtable时要首先获得同步锁，其它线程要等到同步锁被释放之后才能再次获得同步锁更新Hashtable。
2. Fail-safe和iterator迭代器相关。如果某个集合对象创建了Iterator或者ListIterator，然后其它的线程试图“结构上”更改集合对象，将会抛出ConcurrentModificationException异常。但其它线程可以通过set()方法更改集合对象是允许的，因为这并没有从“结构上”更改集合。但是假如已经从结构上进行了更改，再调用set()方法，将会抛出IllegalArgumentException异常。
3. 结构上的更改指的是删除或者插入一个元素，这样会影响到map的结构。
## 结论
Hashtable和HashMap有几个主要的不同：线程安全以及速度。仅在你需要完全的线程安全的时候使用Hashtable，而如果你使用Java 5或以上的话，请使用ConcurrentHashMap吧。

## 参考链接
- [HashMap和Hashtable的区别](http://www.importnew.com/7010.html)
- [HashMap、HashTable与ConcurrentHashMap的区别
](https://blog.csdn.net/universe_ant/article/details/58661724)
