---
title: 为CentOS/Redhat/Fedora添加多个IPv6地址
tags:
  - centos
  - fedora
  - ipv6
  - linux
  - redhat
id: 1713
categories:
  - Systems&amp;Servers
date: 2010-03-24 21:00:37
---

这年头IPv4地址紧张得要命，但是IPv6地址却泛滥地要命。很多服务器托管商分配IPv6地址的时候一般直接分配/64，也就是2的64次方个地址，比所有的IPv4地址加起来还多。地址多了，加起来也要命，下面介绍两种为CentOS/Fedora/Redhat批量添加多个IPv6地址的方法。
> 假设要为eth0添加2607:f0d0:1002:11::10 到 2607:f0d0:1002:11::50共41个IPv6地址
<!--more-->

### 方法一：打开/etc/rc.local添加增加IPv6地址的命令

<div style="background: none repeat scroll 0% 0% #fdfdfd; color: black;"><span style="text-decoration: underline;">Bash语言</span>:</div>
<div class="source" style="font-family: &amp;amp;amp; color: #000000; background-color: #f9f7ed;"><span style="color: #008000;">#IP Alias</span>
<span style="color: #0000ff;">for </span><span style="color: #000000;">ip in </span><span style="color: #000000;">{</span><span style="color: #000000;">10..40</span><span style="color: #000000;">}</span>; <span style="color: #0000ff;">do</span><span style="color: #000000;"> /sbin/ifconfig eth0 inet6 add 2607:f0d0:1002:11::</span><span style="color: #0000ff;">${</span><span style="color: #000000;">ip</span><span style="color: #0000ff;">}</span><span style="color: #000000;">/64; </span><span style="color: #0000ff;">done</span></div>
在命令行执行一下，再添加到rc.local，这样重启之后也有效了。

### 方法二：修改/etc/sysconfig/network-script/ifcfg-eth0，增加Secondary IPv6地址

<div style="background: none repeat scroll 0% 0% #fdfdfd; color: black;"><span style="text-decoration: underline;">Bash语言</span>:</div>
<div class="source" style="font-family: &amp;amp;amp; color: #000000; background-color: #f9f7ed;"><span style="color: #000000;">IPV6ADDR_SECONDARIES</span><span style="color: #000000;">=</span><span style="color: #a31515;">"2607:f0d0:1002:11::10/64 </span>
<span style="color: #a31515;">2607:f0d0:1002:11::11/64 </span>
<span style="color: #a31515;">2607:f0d0:1002:11::12/64 </span>
<span style="color: #a31515;">2607:f0d0:1002:11::13/64 </span>
<span style="color: #a31515;">2607:f0d0:1002:11::14/64"</span></div>
添加完成后，重启网络接口即可：
<div style="background: none repeat scroll 0% 0% #fdfdfd; color: black;"><span style="text-decoration: underline;">Bash语言</span>:</div>
<div class="source" style="font-family: &amp;amp;amp; color: #000000; background-color: #f9f7ed;"><span style="color: #000000;">service network restart</span></div>
有时新加的IPv6地址不能立即ping通，稍等几分钟之后即可。

最后宣传下我的 IPv6代理 ： [http://ipv6-proxy.kangzj.net/](http://ipv6-proxy.kangzj.net/)