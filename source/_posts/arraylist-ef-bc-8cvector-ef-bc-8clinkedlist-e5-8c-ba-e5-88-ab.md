---
title: Java中ArrayList，Vector，LinkedList区别
tags:
  - ArrayList
  - Collection
  - java
  - LinkedList
  - List
  - queue
  - Vector
id: 1972
comment: false
categories:
  - Programming
date: 2014-03-28 10:20:41
---

三种结构都实现了Collection接口和List接口。而LinkedList还实现了Queue接口。

内部实现区别：

* ArrayList可以理解为一个可变长度数组，特点是内存连续，随机访问快，插入、删除慢，扩展容量时，每次增加原容量的50%；

* Vector可以理解为线程安全的ArrayList，扩展容量时，每次容量翻倍；

* LinkedList实现上为一个双向链表，随机访问慢，插入、删除快。

refrence: [http://www.programcreek.com/2013/03/arraylist-vs-linkedlist-vs-vector/](http://www.programcreek.com/2013/03/arraylist-vs-linkedlist-vs-vector/)