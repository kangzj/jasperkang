---
title: 'Java中HashSet, TreeSet, LinkedHashSet区别'
tags:
  - HashSet
  - java
  - LinkedHashSet
  - Set
  - TreeSet
id: 1977
comment: false
categories:
  - Programming
date: 2014-03-28 10:32:57
---

三个结构都实现了Set接口，不允许含有重复元素。

* HashSet是用哈希表实现的，增删查的复杂度都是O（1），不能保证元素的顺序

* TreeSet是用一个树形结构实现（红黑树），增删查的复杂度为O（log(n)），维护一个排序的Set，可以用 first(), last(), headSet(), tailSet()等获取最大最小的元素。

* LinkedHashSet是用链表+哈希表实现，因为是Linked，所以可以保持插入的顺序，增删查复杂度都是O（1）