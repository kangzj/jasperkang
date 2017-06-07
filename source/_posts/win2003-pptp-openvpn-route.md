---
title: Win2003作中转VPN服务器多路由共享上网的方法
tags:
  - google
  - OpenVPN
  - twitter
  - vpn
  - Windows 2003
  - youtube
  - 路由
id: 1809
categories:
  - Systems&amp;Servers
date: 2010-12-28 21:25:52
---

《[Windows 2003 上配置 VPN + NAT共享上网](http://kangzj.net/windows-2003-vpn-nat/)》中已经介绍了如何利用windows 2003共享上网。现在的情况的，我还想上twitter, youtube等应用，于是，在这台win 2003上通过OpenVPN连接到一台美国服务器。OpenVPN服务器设置的方法就不说了，可以参考[这里](http://www.black-xstar.com/blog/693.html)。这篇文章的思路和chnroot是相反的，默认走本地，被封锁的才走vpn，更节省流量，速度也更爽些。由于不想让VPN网关成为默认网关，需要把服务器的配置文件中的
<pre>**push "redirect-gateway def1"**</pre>
去掉。

连接成功之后，相当于win 2003有了两块网卡，只要在win 2003的“路由和远程访问里”设置一些静态路由就可以了。至于添加哪些IP，我是这样做的，ping 一下常用网站的IP（比如上面的twitter啊，youtube之类，把C段或者B段都加作走VPN），如下图所示：

[![])CNO[KWPKTPVL_G94TKXFE](http://blog.kangzj.net/wp-content/uploads/2010/12/CNOKWPKTPVL_G94TKXFE_thumb.jpg "])CNO[KWPKTPVL_G94TKXFE")](http://blog.kangzj.net/wp-content/uploads/2010/12/CNOKWPKTPVL_G94TKXFE.jpg)

现在好了，通过vpn连到这台win 2003就可以被封锁的走vpn，而不封锁的直接走本地连接啦~吼吼。还有一点需要注意，网关的IP是你机器分到的IP的上一个IP，我机器分到的IP是10.8.253.6，网关IP是10.8.253.5，这个要是加错了，就不成鸟。。。其实win xp也是可以设置的，只不过要用命令行。

纪念Google.com被强，敏感词敏感词敏感词敏感词！！！