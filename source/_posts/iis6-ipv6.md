---
title: 原来IIS6默认支持IPV6!!
tags:
  - iis6
  - ipv6
id: 45
categories:
  - Systems&amp;Servers
date: 2008-10-30 06:07:58
---

&nbsp;&nbsp;&nbsp;&nbsp;想架一个ipv6的http服务器，在网上查了半天，结果都说要用apache，而且还要自己编译，加入支持ipv6的模块。由于自己编程不是很强，关键是那些工程都太复杂了，就找了个现成的，别的编译好的，才勉强搭了一个http的服务器，还用来提供proxy的服务。

&nbsp;&nbsp;&nbsp;&nbsp;结果今天，在服务器上用[code]netstat -an[/code]查看了下端口，发现IIS6竟然在监听ipv6地址的端口，这真是让人有些兴奋啊，大家好像都不知道的样子，这下子在win下建站也不用另装服务器了，IIS6就可以！但是美中不足的是，IIS6没有图形化界面支持并且不能监听域名（至少我没有发现）~~但是基于端口的虚拟机是没有问题的~~