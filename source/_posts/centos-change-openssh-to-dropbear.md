---
title: CentOS中用dropbear替换OpenSSH
tags:
  - centos
  - dropbear
  - OpenSSH
  - sshd
id: 1740
categories:
  - Systems&amp;Servers
date: 2010-06-02 11:22:31
---

dropbear是轻量的sshd服务器，与OpenSSH相比，他更简洁，更小巧，运行起来占用的内存也更少。如果你的VPS只有128M内存，甚至64M内存，而你又比较喜欢开多个ssh终端，或者开一些ssh账号给其他同学用的话，还是比较有必要的，因为，每一个普通用户登录，OpenSSH会开两个sshd进程，而dropbear只开一个进程，这样算起来，OpenSSH内存占用是dropbear的5-6倍。

Debian系统的看这里：[http://www.vpsee.com/2009/06/64mb-vps-optimize-debian5/](http://www.vpsee.com/2009/06/64mb-vps-optimize-debian5/ "http://www.vpsee.com/2009/06/64mb-vps-optimize-debian5/")

好了，不说了，开弄。<!--more-->

### 1\. 下载dropbear

> wget [http://matt.ucc.asn.au/dropbear/dropbear-0.52.tar.gz](http://matt.ucc.asn.au/dropbear/dropbear-0.52.tar.gz "http://matt.ucc.asn.au/dropbear/dropbear-0.52.tar.gz")
> 
> tar -xvzf dropbear-0.52.tar.gz
> 
> cd dropbear-0.52
> 
> ./configure
> 
> #先不要急于make和make install

### 2\. 编译安装dropbear

OpenSSH不要马上停掉，否则，一量dropbear安装失败就连不上vps了(有console access的除外)。先把OpenSSH换个端口：
> vi /etc/ssh/sshd_config
找到Port 22换成Port 2200

再执行：
> service sshd restart
于是OpenSSH就监听2200端口了，好了，下面可以编译安装dropbear了：
> make &amp;&amp; make install

### 3\. 配置dropbear

sshd服务器都需要公钥啊啥啥的，下面就来生成一下：
> mkdir /etc/dropbear
> 
> /usr/local/bin/dropbearkey -t dss -f /etc/dropbear/dropbear_dss_host_key
> 
> /usr/local/bin/dropbearkey -t rsa -s 4096 -f /etc/dropbear/dropbear_rsa_host_key
这就配置完成了，启动就更简单了：
> /usr/local/sbin/dropbear
设置成开机自动启动：
> vi /etc/rc.local
在最后加一行：
> /usr/local/sbin/dropbear

### 4\. dropbear的补充说明

dropbear默认的安装路径是：/usr/local/sbin

如果想监听特定的端口，按如下格式执行，如果不加此参数则会监听默认端口：
> /usr/local/sbin/dropbear –p 2222
更改默认监听的端口方法：

在编译dropbear之前，先执行（把2222换成您希望的端口即可）：
> sed -i 's/22/2222/g' options.h
安装需要以下的包，在安装之前可以先执行一下：
> yum install zlib* gcc make
还有其他问题的，可以：
> /usr/local/sbin/dropbear -h
自己看帮助去吧。