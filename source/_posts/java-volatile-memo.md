---
title: JAVA volatile关键字特性备忘
tags:
  - java
  - volatile
  - 多线程
id: 1921
categories:
  - Programming
date: 2012-09-26 10:08:11
---

1.  <span style="color: #000000;">对volatile变量的读写有一个全局的排序，但是volatile变量跟常规变量的读写顺序没并没有保证</span>
2.  <span style="color: #000000;">volatile的值不会被缓存，所有线程读取到的都是当前的（主存中的）值</span>
3.  <span style="color: #000000;">对volatile的变量的读写好像是用了synchronized包围起来一样</span>