---
title: 关于OpenDNS和DNS劫持
tags:
  - dns
  - dnspod
  - DNS污染
  - google
  - OpenDNS
  - 域名劫持
  - 防止域名劫持
id: 1480
categories:
  - Systems&amp;Servers
date: 2009-12-08 16:36:14
---

DNSPod官方博客《[我为什么不建议使用OpenDNS和Google Public DNS](http://blog.dnspod.com/2009/12/why-not-opendns-and-google-public-dns/)》给我们纠正了一些看法，全文大体说明了以下几个问题：

1.  因为DNS查询用的是UPD协议，某墙十分容易就可以篡改，所以使用OpenDNS并不能防止域名被劫持；
2.  GoogleDNS解析速度还可以OpenDNS解析速度较慢（达到600多ms）；
3.  GoogleDNS或者OpenDNS会解析出国外国外镜像网站IP，因而降低访问速度；
说得很对，但是第1条还有一种情况奶罩没有考虑到，就是国内DNS服务器可以直接劫持域名的。这种情况，OpenDNS或者GoogleDNS是可以防止的。

对第3条我是深有体会，[学校机房电信专线，却设置了学校的DNS服务器（教育网），结果导致一大堆网站上不了](http://kangzj.net/longest-distance-of-the-world/)，道理完全相同。

既然某墙升级了，可以直接更改DNS查询包来劫持域名，我们应该怎么做？

<!--more-->

### 1\. 超级无敌hosts文件

没什么好办法了，只能拿出我们的终极武器hosts文件。操作系统进行DNS查询时会首先读取这个文件，如果文件里有，就不会再去查询DNS了。网上经常会流传一些更改hosts以达到突破某墙的效果，慢慢收集。

### 2\. 通过加密代理来查询DNS

再一点，IE是自动利用代理服务器来查询DNS的，而FF默认是查询本地设置，用SSH Sockets代理来上网，可能一些网站还是上不了。FF可以通过如下设置更改成利用代理服务器来查询DNS：

在地址栏输入：about:config

点击”我保证会小心”，就到了设置页，双击：network.proxy.socks_remote_dns

该值会变成true，就表示更改成功。

还有什么别的方法，请大家补充啊。

<span style="color: #800000;">PS：留言中请不要提“翻”X那个X“墙”两字，请用fq两个字母替代，谢谢。</span>