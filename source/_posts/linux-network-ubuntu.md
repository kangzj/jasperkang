---
title: ubuntu 8.10(intrepid)网络设置问题
tags:
  - linux
  - ubuntu
  - 网络设置
id: 49
categories:
  - Systems&amp;Servers
date: 2008-11-14 06:24:34
---

    在图形界面总改了IP和DNS之类之后，重启这些设置就没了，很郁闷，就上网搜了一下，结果有人说新建一个连接就可以了，我就照做了，果然是可以的。
    但是原来为什么不行呢？发现有这两个设置只有一个不同的地方，就是系统设置那里，把勾去掉就OK了，ubuntu的网络就不用每次重启后都设置了！