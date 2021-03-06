# README

<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=6 orderedList=false} -->
<!-- code_chunk_output -->

* [Java篇](#java篇)
	* [Java基础知识](#java基础知识)
	* [多线程](#多线程)
	* [集合](#集合)
	* [JVM](#jvm)
* [计算机网络](#计算机网络)
* [数据结构与算法](#数据结构与算法)
* [数据库](#数据库)
* [Spring](#spring)
	* [Spring概述](#spring概述)
* [JavaWeb](#javaweb)
	* [Servlet与Tomcat](#servlet与tomcat)

<!-- /code_chunk_output -->

## Java篇
### Java基础知识
- [java中==和equals和hashCode的区别](/Java篇/Java基础知识/java中==和equals和hashCode的区别.md)✔️
- [int和Integer的区别](/Java篇/Java基础知识/int和Integer的区别.md)✔️
- [抽象类的意义](/Java篇/Java基础知识/抽象类的意义.md)✔️
- [抽象类与接口的区别](/Java篇/Java基础知识/抽象类与接口的区别.md)✔️
- [能否创建一个包含可变对象的不可变对象](/Java篇/Java基础知识/能否创建一个包含可变对象的不可变对象.md)✔️
- [String、StringBuffer、StringBuilder的区别](/Java篇/Java基础知识/String、StringBuffer、StringBuilder的区别.md)✔️
- [泛型中extends和super的区别](/Java篇/Java基础知识/泛型中extends和super的区别.md)✔️
- [final，finally，finalize的区别](/Java篇/Java基础知识/final，finally，finalize的区别.md)✔️
- [序列化的方式](/Java篇/Java基础知识/序列化的方式.md)
- [String转化为Integer的方式及其原理](/Java篇/Java基础知识/String转化为Integer的方式及其原理.md)
- [静态属性和静态方法能否被继承、重写，why](/Java篇/Java基础知识/静态属性和静态方法能否被继承、重写，why.md)
- [成员内部类、静态内部类、局部内部类和匿名内部类的理解已经在项目内的应用](/Java篇/Java基础知识/成员内部类、静态内部类、局部内部类和匿名内部类的理解已经在项目内的应用.md)
- [常见编码方式](/Java篇/Java基础知识/常见编码方式.md)
- [如何格式化日期](/Java篇/Java基础知识/如何格式化日期.md)
- [Java的异常体系](/Java篇/Java基础知识/Java的异常体系.md)
- [什么是异常链](/Java篇/Java基础知识/什么是异常链.md)
- [throw和throws的区别](/Java篇/Java基础知识/throw和throws的区别.md)
- [反射的原理及创建类实例的三种方式](/Java篇/Java基础知识/反射的原理及创建类实例的三种方式.md)✔️
- [java当中的4种引用](/Java篇/Java基础知识/java当中的4种引用.md)
- [深拷贝和浅拷贝的区别是什么](/Java篇/Java基础知识/深拷贝和浅拷贝的区别是什么.md)
- [编译器常量与使用的风险是什么](/Java篇/Java基础知识/编译器常量与使用的风险是什么.md)
- [聊聊String的intern方法](/Java篇/Java基础知识/聊聊String的intern方法.md)
- [a=a+b和a+=b的区别](/Java篇/Java基础知识/a=a+b和a+=b的区别.md)
- [静态代理和动态代理的区别及使用场景](/Java篇/Java基础知识/静态代理和动态代理的区别及使用场景.md)
- [谈谈对java多态的理解](/Java篇/Java基础知识/谈谈对java多态的理解.md)
- [实现多态的机制是什么](/Java篇/Java基础知识/实现多态的机制是什么.md)
- [如何将一个Java对象序列化到文件里](/Java篇/Java基础知识/如何将一个Java对象序列化到文件里.md)
- [对Java反射的理解](/Java篇/Java基础知识/对Java反射的理解.md)
- [对Java注解的理解](/Java篇/Java基础知识/对Java注解的理解.md)
- [对依赖注入的理解](/Java篇/Java基础知识/对依赖注入的理解.md)✔️
- [举例说明泛型原理](/Java篇/Java基础知识/举例说明泛型原理.md)
- [String为什么要设计成不可变的](/Java篇/Java基础知识/String为什么要设计成不可变的.md)
- [为什么要对Object中的equal和hashCode重写](/Java篇/Java基础知识/为什么要对Object中的equal和hashCode重写.md)

### 多线程
- [开启线程的3种方式](/Java篇/多线程/开启线程的3种方式.md)✔️
- [进程、线程、协程之间的区别](/Java篇/多线程/进程、线程、协程之间的区别.md)✨
- [线程之间是如何通信的](/Java篇/多线程/线程之间是如何通信的.md)✔️
- [Deamon线程](/Java篇/多线程/Deamon线程.md)✔️
- [什么是ReentrantLock可重入锁](/Java篇/多线程/什么是ReentrantLock可重入锁.md)
- [什么是线程组，为什么在Java中不推荐使用](/Java篇/多线程/什么是线程组，为什么在Java中不推荐使用.md)
- [乐观锁和悲观锁的理解，如何实现](/Java篇/多线程/乐观锁和悲观锁的理解，如何实现.md)
- [Java中用到的线程调度算法是什么](/Java篇/多线程/Java中用到的线程调度算法是什么.md)
- [同步方法和同步块，哪个是更好的选择](/Java篇/多线程/同步方法和同步块，哪个是更好的选择.md)
- [run和start方法的区别](/Java篇/多线程/run和start方法的区别.md)
- [如何控制某个方法允许被并发访问线程的个数](/Java篇/多线程/如何控制某个方法允许被并发访问线程的个数.md)
- [wait和sleep的区别](/Java篇/多线程/wait和sleep的区别.md)
- [Thread类中的yieId方法的作用](/Java篇/多线程/Thread类中的yieId方法的作用.md)
- [什么是不可变对象，它对并发应用有什么帮助](/Java篇/多线程/什么是不可变对象，它对并发应用有什么帮助.md)
- [wait、notify的理解](/Java篇/多线程/wait、notify的理解.md)
- [为什么wait、notify、nitifyAll这些方法不在Thread对象里面](/Java篇/多线程/为什么wait、notify、nitifyAll这些方法不在Thread对象里面.md)
- [什么导致线程阻塞](/Java篇/多线程/什么导致线程阻塞.md)
- [java中同步的方法](/Java篇/多线程/java中同步的方法.md)
- [谈谈对Synchronized、类锁、方法锁、重入锁的理解](/Java篇/多线程/谈谈对Synchronized、类锁、方法锁、重入锁的理解.md)
- [static Synchronized方法的多线程访问和作用](/Java篇/多线程/static_Synchronized方法的多线程访问和作用.md)
- [同一个类里两个Synchronized方法两个线程同时访问的问题](/Java篇/多线程/同一个类里两个Synchronized方法两个线程同时访问的问题.md)
- [如何确保main方法所在的线程是java程序最后结束的线程](/Java篇/多线程/如何确保main方法所在的线程是java程序最后结束的线程.md)
- [volatile的作用](/Java篇/多线程/volatile的作用.md)
- [ThreadLocal的作用](/Java篇/多线程/ThreadLocal的作用.md)
- [对NIO的理解](/Java篇/多线程/对NIO的理解.md)
- [什么是Callable和Future](/Java篇/多线程/什么是Callable和Future.md)
- [ThreadLocal、volatile和Synchronized的区别](/Java篇/多线程/ThreadLocal、volatile和Synchronized的区别.md)
- [Synchronized和Lock的区别](/Java篇/多线程/Synchronized和Lock的区别.md)
- [ReentrantLock和synchronized和volatile的区别](/Java篇/多线程/ReentrantLock和synchronized和volatile的区别.md)
- [CycliBarriar和CountdownLatch的区别](/Java篇/多线程/CycliBarriar和CountdownLatch的区别.md)
- [CopyAndWriteArrayList可以用于什么场景](/Java篇/多线程/CopyAndWriteArrayList可以用于什么场景.md)
- [ReentrantLock的内部实现](/Java篇/多线程/ReentrantLock的内部实现.md)
- [lock的原理](/Java篇/多线程/lock的原理.md)
- [invokeAndWait和invokeLater的区别](/Java篇/多线程/invokeAndWait和invokeLater的区别.md)
- [多线程中的忙循环是什么](/Java篇/多线程/多线程中的忙循环是什么.md)
- [怎么检测一个线程是否拥有锁](/Java篇/多线程/怎么检测一个线程是否拥有锁.md)
- [死锁的4个必要条件](/Java篇/多线程/死锁的4个必要条件.md)
- [对象锁和类锁是否互相影响](/Java篇/多线程/对象锁和类锁是否互相影响.md)
- [什么是线程池，如何使用](/Java篇/多线程/什么是线程池，如何使用.md)
- [java线程池中summit和execute的区别](/Java篇/多线程/java线程池中summit和execute的区别.md)
- [java中interrupted和isInterrupted的区别](/Java篇/多线程/java中interrupted和isInterrupted的区别.md)
- [用java实现阻塞队列](/Java篇/多线程/用java实现阻塞队列.md)
- [BlockingQueue介绍](/Java篇/多线程/BlockingQueue介绍.md)
- [多线程有什么要注意的问题](/Java篇/多线程/多线程有什么要注意的问题.md)
- [如何保证多线程读写文件的安全](/Java篇/多线程/如何保证多线程读写文件的安全.md)
- [多线程断点续传的原理](/Java篇/多线程/多线程断点续传的原理.md)
- [断点续传的实现](/Java篇/多线程/断点续传的实现.md)
- [实现生产者消费者模式](/Java篇/多线程/实现生产者消费者模式.md)
- [ReadWriteLock是啥](/Java篇/多线程/ReadWriteLock是啥.md)
- [用Java写一个将导致死锁的程序，你将怎么解决](/Java篇/多线程/用Java写一个将导致死锁的程序，你将怎么解决.md)
- [SimpleDateFormat是线程安全的吗](/Java篇/多线程/SimpleDateFormat是线程安全的吗.md)
- [同步集合和并发集合有什么区别](/Java篇/多线程/同步集合和并发集合有什么区别.md)
- [Timer类，如何创建一个有特定时间间隔的任务](/Java篇/多线程/Timer类，如何创建一个有特定时间间隔的任务.md)

### 集合

### JVM

## 计算机网络

## 数据结构与算法

## 数据库

## Spring
### Spring概述
- [使用Spring框架的好处](/Spring/Spring概述/使用Spring框架的好处.md)
- [Spring由哪些模块组成](/Spring/Spring概述/Spring由哪些模块组成.md)
- [AOP模块](/Spring/Spring概述/AOP模块.md)
- [Web模块](/Spring/Spring概述/Web模块.md)
- [核心容器（应用上下文）模块](/Spring/Spring概述/核心容器（应用上下文）模块.md)
- [什么是SpringIOC容器](/Spring/Spring概述/什么是SpringIOC容器.md)
- [IOC的优点是什么](/Spring/Spring概述/IOC的优点是什么.md)
- [ApplicationContext通常的实现是什么](/Spring/Spring概述/ApplicationContext通常的实现是什么.md)
- [Bean工厂和ApplicationContexts的区别](/Spring/Spring概述/Bean工厂和ApplicationContexts的区别.md)
## JavaWeb
### Servlet与Tomcat
- [Servlet生命周期](/JavaWeb/Servlet与Tomcat/Servlet生命周期.md)✔️
