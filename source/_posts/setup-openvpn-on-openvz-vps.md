---
title: OpenVZ VPS安装配置OpenVPN
tags:
  - BurstNET
  - centos
  - iptables
  - OpenVPN
  - OpenVZ
  - vpn
  - vps
id: 1385
categories:
  - Systems&amp;Servers
date: 2009-11-15 00:22:15
---

在安装之前，请先**联系客服打开虚拟机tun/tap、iptables要支持NAT**，最简单的方法就是告诉客服，你要用OpenVPN，让他把应该打开的都打开:-D，如果不给开，那么你就搞不成OpenVPN了，这个教程也就没有必要往下看了。

检测是否开启了tun：
> lsmod | grep tun
> 
> modprobe tun
> 
> 1个1个输完后，如果提示kernel出错，就代表没有开启，或者压根就没有编译进去。
> 
> ——zhihao daigou.in
![](../wp-includes/js/tinymce/plugins/wordpress/img/trans.gif "更多...")<!--more-->或者：
> SSH登陆VPS，我的系统是32的CentOS 5.4。
> OpenVPN需要TUN支持，大多数VPS默认都没有开启，你可以用这个命令检测：cat /dev/net/tun
> 如果返回信息为：cat: /dev/net/tun: File descriptor in bad state 说明正常，否则发个ticket给VPS公司让他们帮忙开吧。
> 另外如果你需要连上OpenVPN后能访问互联网，还需要iptables_nat模块支持，用这个命令检测：iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o venet0 -j MASQUERADE
> 如果返回信息为：iptables: Unknown error 4294967295 说明正常，否则同样需要发个ticket让VPS公司帮忙开通。
> 
> ——Black-Xstar
服务器编译安装配置及客户端配置与一般VPN相同，不再赘述，CentOS用户可以看这篇文章：

《CentOS5下安装OpenVPN》：[http://www.my-china.org.cn/Linux/226/](http://www.my-china.org.cn/Linux/226/ "http://www.my-china.org.cn/Linux/226/")

这里仅说明不同的地方，第三部分**OpenVPN访问外网的设置**请按以下操作：

打开转发：
> <tt>echo 1 &gt; /proc/sys/net/ipv4/ip_forward</tt>
> 
> <tt>/sbin/sysctl -w net.ipv4.ip_forward=1</tt>
配置iptables转发规则（注意加黑的部分，加在rc.local里，保证重启之后还有效）：
> <tt>/sbin/iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o **venet0** -j MASQUERADE</tt>
<span style="color: #ff0000;">UPDATE（by 猫大）：</span>再需要注意的是，虽然openvpn服务监听的是*:1194，但是如果设置的UDP方式，则只能用你的**主IP**来连接，其它IP连接不上。

_注：本文方法在BurstNET VPS中测试成功。_