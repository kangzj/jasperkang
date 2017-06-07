---
title: SSH和VPN凸墙的区别与联系分析
tags:
  - OpenVPN
  - ssh
  - vpn
  - 凸墙
id: 1659
categories:
  - Software
date: 2010-03-10 00:39:12
---

好久没写技术文章了，呵呵，从来没写过凸墙的文章呢，这次讲讲。不过不是讲怎么凸墙，SSH代理和VPN是两种最流行的凸墙方式，这篇文章就来谈谈他们的异同。

### SSH方式：

通过SSH连接，在本地与远程服务器之间建立一个加密的管道（Tunnel），SSH客户端监听本地端口，形成SOCKET5代理。由于IE对SOCKET5代理不好，大家一般都是用FireFox。直接将FireFox设置Socket5代理就是可以正常使用的。但是这样，上国内网站也会绕道国外，影响速度。好在FireFox有大量优秀的插件，FoxyProxy和AutoProxy是很常用的通过URL筛选决定是否通过代理访问网站的插件，后者用的尤其多。

<!--more-->

### VPN方式：

VPN其实也是在本地与远程服务器之间建立了一个加密的通道，但是，与SSH不同的是，VPN客户端会虚拟一个网卡出来（这个虚拟的网卡连接的就是刚才说的那个加密通道），然后修改路由，使流量从加密通道走，达到凸墙的目的。当然，VPN也存在跟SSH相同的问题，如果访问国内网站，会绕道国外，速度很慢。聪明的人们又想出了办法：连接了VPN的电脑相当于有两块网卡，只要让国内流量从真实网卡走而国际流量从虚拟网卡走，这个问题就解决了。实际的操作就是手工加入国内IP的路由，让这部分流量直接走本地连接来搞定。

在解决绕道的问题上，大家可以看出SSH方式和VPN方式的不同了，SSH方式可以在URL的级别上筛选网址走加密通道，而VPN方式只能筛选IP。

举个例子，假设xxx是某强屏蔽的关键字，SSH代理+AutoProxy可以做到使http://www.abc.com/xxx走代理，而http://www.abc.com/yyy不走代理，这是VPN方式力所不及的。当然，VPN方式也有它得天独厚的好处，就是不用对应用软件进行任何设置即可使用，这对一些根本没法设置代理的应用软件是莫大的福音，这也是SSH方式力所不及的。

### 最后介绍几个SSH和VPN项目：

SSH帐号(支持IPv6) - [http://sshchina.com](http://sshchina.com)

VPN (PPTP/L2TP/OpenVPN)帐号 - [http://vpnchina.net](http://vpnchina.net)

教育网IPv6 OpenVPN帐号 - [http://eduVPN.com](http://eduVPN.com)

PPTP VPN： [http://pptp.us](http://pptp.us)

yegle的OpenVPN：[http://yegle.net/openvpn/](http://yegle.net/openvpn/)

pptp/l2tp vpn: [http://www.vpn38.net](http://www.vpn38.net)