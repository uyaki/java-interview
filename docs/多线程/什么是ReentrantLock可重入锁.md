# 什么是ReentrantLock可重入锁

---
目录

<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=6 orderedList=false} -->
<!-- code_chunk_output -->

* [什么是可重入](#什么是可重入)
* [与 synchronized 的异同](#与-synchronized-的异同)
* [引用](#引用)
* [返回目录](#返回目录)

<!-- /code_chunk_output -->

---

## 什么是可重入

所谓的可重入是指，线程可对同一把锁进行重复加锁，而不会被阻塞住，这样可避免死锁的产生。

> ReentrantLock 内部是基于 AbstractQueuedSynchronizer（以下简称AQS）实现的


## 与 synchronized 的异同

特性              | synchronized | ReentrantLock | 相同
-----------------|--------------|---------------|----
可重入            | 是           | 是            | ✅
响应中断          | 否           | 是            | ❌
超时等待          | 否           | 是            | ❌
公平锁            | 否           | 是            | ❌
非公平锁          | 是           | 是            | ✅
是否可尝试加锁     | 否           | 是            | ❌
是否是Java内置特性 | 是           | 否            | ❌
自动获取/释放锁    | 是           | 否            | ❌
对异常的处理       | 自动释放锁   | 需手动释放锁  | ❌



---
## 引用

[ReentrantLock实现原理](https://uyaba.github.io/java-interview/#/多线程/ReentrantLock实现原理)

[AQS](https://uyaba.github.io/java-interview/#/多线程/AQS)

---
## 返回目录
[README.md](./../../README.md)
