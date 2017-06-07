---
title: 利用apache进行ipv6/ipv4环境下代理服务器的架设与使用(1)
tags:
  - apache
  - ipv6
  - proxy
id: 44
categories:
  - Systems&amp;Servers
date: 2008-10-22 05:49:53
---

    apache不但是优秀是http服务器，它还可以通过它的模块进行代理服务，而如果已经加载了ipv6模块的apache服务器就可以提供同时可以上ipv6和ipv4的网络的代理服务器。具体步骤如下：
    1.下载有ipv6模块的apache服务器，需要自己编译才能支持ipv6，网上有编译好的，请自行查找。
    2.编辑httpd.conf加载相应的代理模块，我不是很清楚哪个是哪个，我把所有跟proxy有关的模块都加载了:-)，然后加入配置：
      ProxyRequest On/Off #启用或者禁用Apache代理服务。
      CacheRoot "/etc/httpd/proxy" #代理缓存的根目录。
      CacheSize 5 #代理缓存的大小。
      CacheGcInterval 4 #设定运行管理缓存的无用数据搜集程序的时间间隔
      CacheMaxExpire 24 #文件过期时间。
      CacheDefaultExpire 1 #指定未包含过期信息文件的有效期。
      NoCache a-domain.com another-domain.edu #该网站的文件将不被缓存。
    3.修改监听的端口
      如果原来是listen 80的话可以不用修改，如果原来listen ip:80的话，可以加入一行：Listen [::]:80(意思是监听所有ipv6地址)，端口可以改成你想要的。
    OK，架设成功！同时你也有了同时支持一个ipv4和ipv6的网站，内网的同学就有了一个全国乃至全世界ipv6网络都能访问的网站了！
    下个教程将介绍如何用这个代理上网~~