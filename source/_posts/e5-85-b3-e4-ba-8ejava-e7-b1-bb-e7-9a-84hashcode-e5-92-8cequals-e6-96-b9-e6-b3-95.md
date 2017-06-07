---
title: 关于Java类的hashCode和equals方法
tags:
  - equals
  - hashCode
  - java
id: 1979
comment: false
categories:
  - Programming
date: 2014-03-28 10:49:55
---

前面两篇文章中提到了利用哈希表的数据结构，如HashMap，HashSet等，这些数据结构利用对象的hashCode和equals函数来识别对象是否相同，原则如下：

* hashCode不同的对象一定不同

* hashCode相同的对象不一定相同

比方说HashMap，查找元素时，会先以key的hashCode来查找，如果找到对象，然后再以equals方法来判定是否相等，如果相等，才返回相应的value。

自定义数据结构做key时，需要成对的实现两个函数才可以正确的使用利用哈希表实现的数据结构。