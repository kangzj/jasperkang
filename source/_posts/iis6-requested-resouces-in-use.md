---
title: IIS 6.0“请求的资源正在使用中”解决方法
tags:
  - iis6
id: 31
categories:
  - Systems&amp;Servers
date: 2008-06-24 11:32:23
---

打开网站时提示：请求的资源正在使用中。

一般造成这种情况的原因是因为在服务器版操作系统上装单机版杀毒软件，造成<span style="color: #800000;">JS和VB脚本动态链接库的故障</span>引起的。

解决的方法有二：

一、卸载杀毒软件，重启机器即可。

二、点击开始-运行regsvr32 jscript.dll注册jscript.dll脚本动态链接库，然后运行regsvr32 vbscript.dll注册vbscript.dll脚本动态链接库。

再试一下，OK服务器是不是可以正常访问了？！

<span style="color: #ff0000;">对于HTTP 500错误的处理，千万不能烦躁，有太多的可能性。首先要把IE的“显示友好错信息”关掉，才能看到确实的错误，进而及决。</span>