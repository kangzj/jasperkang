---
title: 利用Nginx反向代理功能架设Ubuntu升级源
tags:
  - linux
  - nginx
  - source.list
  - ubuntu
  - ubuntu源
  - 升级
id: 985
categories:
  - Systems&amp;Servers
date: 2009-09-19 14:20:19
---

![](http://www.ubuntu.org.cn/themes/ubuntu07/images/masthead-cds.jpg)

[北师大的网络情况以前说过了，学校里必须过验证网关才能上外网](http://kangzj.net/squid-tranparent/)。为了方便校内同学方便地（不费流量地）升级Ubuntu，也可以充分利用服务器的资源，做了个Ubutu校内的升级源。机器比较老，没有很大的硬盘，做个源的话至少需要上百G的空间，不太现实。于是Kangzj想了出这个方法，在校内一台能上外网的服务器上反向代理一个速度快的Ubuntu源。我选择的是中科大的Ubuntu源（谢谢），速度可以到10M。非常简单，建了一个虚拟主机，然后就解决问题了，下面附上nginx配置文件：

<!--more-->
> <span style="background-color: #ffffff;"> </span> server {
> 
>        listen 80;
> 
>        server_name gnu.xinqing100.net;
> 
>        access_log /var/log/nginx/gnu.xinqing100.net.access.log;
> 
>        location /ubuntu/ {
> 
>            proxy_pass [http://debian.ustc.edu.cn/ubuntu/](http://debian.ustc.edu.cn/ubuntu/);
> 
>        }
> 
>        location /icons/ {
> 
>            proxy_pass [http://debian.ustc.edu.cn/icons/](http://debian.ustc.edu.cn/icons/);
> 
>        }
> 
> }
只要修改source.list为：
> deb [http://gnu.xinqing100.net/ubuntu/](http://gnu.xinqing100.net/ubuntu/) jaunty main restricted universe multiverse
> deb [http://gnu.xinqing100.net/ubuntu/](http://gnu.xinqing100.net/ubuntu/) jaunty-security main restricted universe multiverse
> deb [http://gnu.xinqing100.net/ubuntu/](http://gnu.xinqing100.net/ubuntu/) jaunty-updates main restricted universe multiverse
> deb [http://gnu.xinqing100.net/ubuntu/](http://gnu.xinqing100.net/ubuntu/) jaunty-backports main restricted universe multiverse
> deb [http://gnu.xinqing100.net/ubuntu/](http://gnu.xinqing100.net/ubuntu/) jaunty-proposed main restricted universe multiverse
> deb-src [http://gnu.xinqing100.net/ubuntu/](http://gnu.xinqing100.net/ubuntu/) jaunty main restricted universe multiverse
> deb-src [http://gnu.xinqing100.net/ubuntu/](http://gnu.xinqing100.net/ubuntu/) jaunty-security main restricted universe multiverse
> deb-src [http://gnu.xinqing100.net/ubuntu/](http://gnu.xinqing100.net/ubuntu/) jaunty-updates main restricted universe multiverse
> deb-src [http://gnu.xinqing100.net/ubuntu/](http://gnu.xinqing100.net/ubuntu/) jaunty-backports main restricted universe multiverse
> deb-src [http://gnu.xinqing100.net/ubuntu/](http://gnu.xinqing100.net/ubuntu/) jaunty-proposed main restricted universe multiverse universe multiverse
如果是9.04，直接用这个就可以；
8.10把jaunty换成intrepid
8.04把jaunty换成hardy
9.10把jaunty换成karmic

校内就可以不能过网关升级Ubuntu甚至网络安装Ubuntu了！