---
title: OpenVPN添加本地路由方法
tags:
  - OpenVPN
  - route
  - vpn
  - 本地路由
  - 路由
id: 1666
categories:
  - Systems&amp;Servers
date: 2010-03-15 18:40:26
---

在上一篇文章中提到过，[VPN可以通过添加本地路由的方式来提高访问速度](http://kangzj.net/difference-between-ssh-vpn/)，这篇文章以OpenVPN为例，讲下怎么添加这些路由。

### 1\. 在OpenVPN配置文件中增加

OpenVPN在连接成功之后会自动增加一些路由，把默认网关改成VPN的，使所有流量都从VPN走。OpenVPN提供了在配置文件中添加路由的功能，我们可以增加一些本地路由，使本地流量不走VPN，既节省了流量（如果限流量的话），又提高了上网的速度。

打开sample.ovpn配置文件，在文件末尾添加即可，如果添加的路由数目超过100条，则要加一句 <span style="color: #000080;">max-routes</span> ，如下所示：

<!--more-->
> max-routes 1000
> route 58.17.0.0 255.255.0.0 net_gateway
> route 58.18.0.0 255.254.0.0 net_gateway
> route 58.20.0.0 255.255.0.0 net_gateway
> route 58.24.0.0 255.254.0.0 net_gateway
> route 58.30.12.136 255.255.255.255 net_gateway
> route 58.32.232.0 255.255.252.0 net_gateway
> route 58.53.208.0 255.255.240.0 net_gateway
> route 58.59.1.15 255.255.255.255 net_gateway
> route 58.59.1.16 255.255.255.254 net_gateway
> route 58.59.128.0 255.255.128.0 net_gateway
> route 58.60.8.0 255.255.248.0 net_gateway
> route 58.60.112.239 255.255.255.255 net_gateway
> route 58.61.32.0 255.255.254.0 net_gateway
> route 58.61.34.0 255.255.255.0 net_gateway
> ………………
这样，OpenVPN连接成功之后就会添加这些路由，达到本地地址走本地接口的目的。

附：[教育网freeip.txt](http://kangzj.net/upload/freeip.txt) [中国IP地址分配列表](http://ftp.apnic.net/apnic/dbase/data/country-ipv4.lst)

### 2\. 利用route add命令添加

route add是dos命令，用以添加路由的，只要我们执行下就OK了，命令格式如下：
> route add 110.6.0.0 mask 255.254.0.0 %gw% metric 5
> route add 110.16.0.0 mask 255.252.0.0 %gw% metric 5
> route add 110.40.0.0 mask 255.252.0.0 %gw% metric 5
> route add 110.48.0.0 mask 255.255.0.0 %gw% metric 5
> route add 110.51.0.0 mask 255.255.0.0 %gw% metric 5
> route add 110.52.0.0 mask 255.254.0.0 %gw% metric 5
> route add 110.56.0.0 mask 255.248.0.0 %gw% metric 5
> route add 110.64.0.0 mask 255.254.0.0 %gw% metric 5
> route add 110.72.0.0 mask 255.254.0.0 %gw% metric 5
> 
> ………………………
**<span style="color: #800080;">这种方法对其它各类的VPN应该是通用的。</span>**

附：[国内IP地址路由](http://chnroutes.googlecode.com/files/pre_created_for_win.zip)

### 3\. 第三种方式chnroutes

在OpenVPN中调用.bat批处理文件来添加路由，我实验的不太成功，有兴趣的可以参照：[http://code.google.com/p/chnroutes](http://code.google.com/p/chnroutes) 。