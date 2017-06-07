---
title: 64M内存的VPS能干点什么？
tags:
  - 64M
  - debian
  - fastcgi
  - ipv6
  - nginx
  - OpenVZ
  - php
  - php-cgi
  - proxy
  - ssh
  - swap
  - vps
  - wo
  - wordpress
  - 反向代理
id: 1196
categories:
  - Systems&amp;Servers
date: 2009-10-27 00:58:46
---

### 1\. VPS相关参数

买的是HostingInside的VPS，参数：

1.  台湾人办的；
2.  服务器位于Fullerton, LA，美国西岸，国内速度不错，HE的网络；
3.  一个ipv4地址，两个ipv6地址（这是我看上它的重要原因）；
4.  基于OpenVZ，64M内存，300MCPU，无Burst，不支持swap；

### 2.  配置Nginx+php跑WordPress

10.21中午11点半买的，一个多小时之后开通，然后紧接着_该服务器所在机房网络出现故障，服务器离线2小时-__-_。安装了debian5，占资源少得让你吃惊：

![](http://kangzj.net/wp-content/uploads/images/200910/free.jpg)

按照[vpsee的方法](http://www.vpsee.com/2009/06/64mb-vps-optimize-debian5/)换了几个软件，裸系统只占不到10M的内存，比起Windows那个吃内存的劲，让人暗爽。

<!--more-->由于只有64M内存，又没有交换区，所以用它来跑LNMP不太可能，更加不要说LAMP。只安装了Nginx, fastcgi方式php，跟[JiuCool同学](http://www.jiucool.com/)借用了个数据库，试验跑WordPress。

启动php-cgi过程中显示内存不足，不过好在启动起来三个php-cgi的进程。这个时候还是不能跑WordPress，会out of memory，于是kill掉三个php-cgi，只剩下一个，空出不少内存，OK，WordPress跑得还挺快，估计一天10, 000个PV应该都不在话下，如果开启wp super cache的话，负载能力便更会有质的提高。

### 3\. IPv4/v6地址物尽其用

然而，太不实在，万一这个php-cgi死掉，我的博客也就玩完了。所以博客没有放在该VPS上，但是独立IP可不能浪费，偶就做了最擅长的[反向代理](http://kangzj.net/tag/%E5%8F%8D%E5%90%91%E4%BB%A3%E7%90%86/)，呵呵~~

然后IPv6地址也不能浪费，一个给[博客](http://kangzj.net/)，另一个就做一个[IPv6在线代理](http://proxy.kangzj.net/)给教育网同学们用。

既然不做WordPress主机，那么php的mysql模块、gd模块便都没有用了，于是给remove掉了。

重新启动php-cgi，奇迹发生了，**原先一个php-cgi进程要占掉20M+内存，现在一个进程只占2M内存**！于是乎启动了四个php-cgi，还剩几十M内存，哇哈哈~~应该可以正常运行了:-D

![](http://kangzj.net/wp-content/uploads/images/200910/now.jpg)

### 4\. 结语

在上篇日志中送了ssh账号，加上本篇日志中介绍的几个应用，现在这个VPS算是物尽其用了，值了，呵呵呵呵:-)

64M内存的VPS其实可以干很多事情的，不是吗？

最后提醒下要买VPS的同志们，一定注意虚拟技术，如果是OpenVZ的，不支持swap，但是最好有burst内存，否则就像我这个，只要内存超过64M就会内存错误，啥也干不成了。基于Xen的可以设置swap，更方便些。