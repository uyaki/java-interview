# 泛型中extends和super的区别
返回[README.md](./../../README.md)

---
目录

<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=6 orderedList=false} -->
<!-- code_chunk_output -->

* [概念](#概念)
* [区别](#区别)
* [PECS原则](#pecs原则)
* [引用](#引用)
* [返回目录](#返回目录)

<!-- /code_chunk_output -->
## 概念
`<? extends T>`和`<? super T>`是Java泛型中的“通配符（Wildcards）”和“边界（Bounds）”的概念。

- `<? extends T>`：是指 “上界通配符（Upper Bounds Wildcards）”
- `<? super T>`：是指 “下界通配符（Lower Bounds Wildcards）”

## 区别

- 边界区别
  - `<? extends T>` 一切`T`和`T`的派生类（T和它儿孙）
  - `<? super T>`一切`T`和`T`的基类（T和它祖宗)

- 存取区别
  - 上界`<? extends T>`不能往里存，只能往外取
  - 下界`<? super T>`不影响往里存，但往外取只能放在Object对象里

## PECS原则
什么是PECS（Producer Extends Consumer Super）原则，已经很好理解了：

- 频繁往外读取内容的，适合用上界Extends。
- 经常往里插入的，适合用下界Super。

---
## 引用
[【Java】泛型中 extends 和 super 的区别？
](https://itimetraveler.github.io/2016/12/27/%E3%80%90Java%E3%80%91%E6%B3%9B%E5%9E%8B%E4%B8%AD%20extends%20%E5%92%8C%20super%20%E7%9A%84%E5%8C%BA%E5%88%AB%EF%BC%9F/)

---
## 返回目录
[README.md](./../../README.md)
