---
title: unresolved external symbol _main问题的解决方法
tags:
  - vc6
id: 6
categories:
  - Programming
date: 2008-07-25 10:04:08
---

C/C++控制台程序都是从main函数开始执行的，而窗口界面的GUI程序则是从WinMain开始执行。

可能是因为链接器的子系统选项被改成了
控制台(/SUBSYSTEM:CONSOLE)

所以链接器以为此程序是控制台程序，查找main入口，显然会出错。
<!--more-->解决方法：
将链接器的子系统选项改为：
Windows (/SUBSYSTEM:WINDOWS)

如果是VS.NET 2003
选择 项目-&gt;属性-&gt;配置属性-&gt;链接器-&gt;System
将子系统改为：
Windows (/SUBSYSTEM:WINDOWS)