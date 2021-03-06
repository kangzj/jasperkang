---
title: 两道关于指针的C语言笔试题
tags:
  - c
  - cpp
  - c语言
  - 工作
  - 指针
  - 笔试
id: 1125
categories:
  - Programming
date: 2009-10-14 08:30:33
---

实验室的师兄师姐为找工作都在狂做C/C++的笔试题，偶们也掺和了下，做了两道指针方面的，大家一起来看看吧。

### 1\. 求n的值。

int a[20];
char * p1 = (char * )a;
char * p2 = (char *)(a+5);
int n= p2-p1;

答案：20。

解析：int为4个字节，char为1个字节。a是int*型指针，加减运算以4个字节为单位，a+5便会指向第20个字节；而p1,p2是char*型，它们进行加减运算时以1个字节为单位。于是p1指向第1个字节而p2指向第21个字节，于是21-1=20，n的值为20。

### 2\. 求 * p 的值。

<!--more-->

int k = 0X123456;

char * p = (char *) &amp;k;

答案：’V’（字符V）

解析：k为int型，32位，0x123456如果写全的话应该是0x00123456。&amp;k为k的地址，**指向k的低位**。p为char*的指针，它只指向一个字节，于是*p指向的值为0x56，十进制值为86，对应的ASCII码为’V’。
> 附：[深入理解C语言指针的奥秘](http://kangzj.net/c-pointer-usage/)，没搞明白的同学可以全面的学习下C语言的指针及其一些应用。