---
title: MFC多核多线程编程遇到的问题总结
tags:
  - cevent
  - cmutex
  - queue
  - waitformultipleobjects
  - waitforsingalobject
  - 临界区
  - 互斥
  - 多CPU
  - 多核
  - 多核多线程
  - 多线程
id: 918
categories:
  - Programming
date: 2009-09-10 10:49:33
---

1.  多线程编程必须有操作系统为基础，知道什么是互斥、临界区、事件、信号量等概念；
2.  知道线程是CPU资源分配的基本单位；

    **给线程分配CPU**，可以用：SetThreadAffinityMask(tHandle,0x00000001)函数，tHandle表示线程的HANDLE（不是CWinThread*），第二个参数表示可以使用的CPU的编号，0x00000001表示只能使用第一个CPU；如果0x00000011，表示可以使用第一和第二个CPU，依此类推；<!--more-->
3.  **WaitForSingalObject()的参数是HANDLE而不是对象**，如果是CEvent的对象要写成WaitForSingalObject(CEvent.m_hObject, INFINITE)，不能乱了。用完事件之后，调用Reset来重置状态；
4.  CMutex.lock()已经包含了WaitForSingalObject()的功能，不要重复用。CEvent没有Lock函数，要按3中所说的做；
5.  Wait的两个函数等待的过程中并不消耗CPU；
6.  在访问互斥资源时一定把互斥资源用CMutex.Lock()和CMutex.Unlock()包起来；
7.  **等待所有线程结束**可以用WaiForMultipleObjects()函数，用法跟WaitForSingleObject很相似，但是注意一个参数；
8.  写程序之前一写把各个线程之间的关系、哪些资源是互斥的、哪些代码段应该做成临界区这些弄清楚。如果是同一个函数的各个线程用临界区比用互斥的效率要高很多；
9.  多线程的调试很麻烦，可以用写文件的方法来看线程中各个变量的情况，但是要注意，文件也是互斥资源，不能同时在两个线程里读写；也可以通过单步调试，调试的时候可以只把要调试的线程加上断点，方便一些，否刚程序在各个线程之间跳来跳去，眼花缭乱；
10.  STL中的queue类，没有元素的时候调用.front()或者.end()会出错：“**dque iterator not dereferencable**”。在调用这两个函数之前要确保.size()不为0；
11.  还没想到。