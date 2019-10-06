# Deamon线程（守护线程）
返回[README.md](./../../README.md)

---
目录

<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=6 orderedList=false} -->
<!-- code_chunk_output -->

* [用户线程与守护线程](#用户线程与守护线程)
* [设置守护线程](#设置守护线程)
* [引用](#引用)
* [返回目录](#返回目录)

<!-- /code_chunk_output -->

---
## 用户线程与守护线程
User Thread(用户线程)
Daemon Thread(守护线程)
> GC就是一个典型的守护线程
- 只要当前JVM实例中尚存在任何一个非守护线程没有结束，守护线程就全部工作；
- 只有当最后一个非守护线程结束时，守护线程随着JVM一同结束工作。
- 如果 User Thread已经全部退出运行了，只剩下Daemon Thread存在了，虚拟机也就退出了。

## 设置守护线程
```java
Thread daemonTread = new Thread();
  // 设定 daemonThread 为 守护线程，default false(非守护线程)
 daemonThread.setDaemon(true);
 // 验证当前线程是否为守护线程，返回 true 则为守护线程
 daemonThread.isDaemon();
```
- thread.setDaemon(true)必须在thread.start()之前设置，否则会跑出一个IllegalThreadStateException异常。你不能把正在运行的常规线程设置为守护线程。
- 在Daemon线程中产生的新线程也是Daemon的。
- 不要认为所有的应用都可以分配给Daemon来进行服务，比如读写操作或者计算逻辑。因为你不可能知道在所有的User完成之前，Daemon是否已经完成了预期的服务任务。一旦User退出了，可能大量数据还没有来得及读入或写出，计算任务也可能多次运行结果不一样。这对程序是毁灭性的。




---
## 引用
[Java中守护线程的总结](https://blog.csdn.net/shimiso/article/details/8964414)

---
## 返回目录
[README.md](./../../README.md)
