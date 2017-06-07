---
title: Ubuntu Server覆盖安装Nginx并配置Etags & Expires
tags:
  - bash
  - debian
  - Etags
  - expires
  - nginx
  - php
  - ubuntu
  - 加速
id: 1128
categories:
  - Systems&amp;Servers
date: 2009-10-15 03:30:14
---

[![image](http://kangzj.net/wp-content/uploads/images/200910/fa2c2ceb7808_122F5/image_thumb_3.png "image")](http://kangzj.net/wp-content/uploads/images/200910/fa2c2ceb7808_122F5/image_3.png) Ubuntu是基于Debian的，继承了Debian的优良特性，apt就是其一。每次要装软件直接apt-get install解决问题，非常方便。但是源里的软件相对比较过时，并且缺乏定制性（比如软件的小插件等）。

Ubuntu 9.04里带的Nginx是0.6.32版，据Jiucool情报讲，有漏洞。当时就想编译安装一个，但是苦于缺少一些库又没时间一一添加而没有安装。今天Ubuntu源里的Nginx更新到了0.6.35，修正了Bug，偶直接给Upgrade了一下。

这两天又折腾加速，YSlow评级要想到A的话，须让Nginx给静态元素加Etags，需要加个插件。加插件的话就要重新编译Nginx，干脆一不做二不休，干掉现在的0.6，搞个0.7.62玩。

最方便就是覆盖掉现在的老版本的Nginx，服务那些脚本就都不用重写直接可以用了。<!--more-->

### 1\. 首先覆盖安装Nginx (部分操作需要sudo)

#### (1) 安装编译需要的各种库（有些可能多余，最后可以autoremove）。

<pre lang="bash">apt-get install gcc libjpeg62-dev libjpeg62 libpng12-0 libpng12-dev libfreetype6 libfreetype6-dev libxml2 libxml2-dev zlib1g zlib1g-dev libglib2.0-0 libglib2.0-dev libbz2-1.0 libbz2-dev libncurses5 libncursesw5-dev libpcre3 libpcre3-dev libmhash-dev git-core</pre>

#### (2) 安装带Etags模块的Nginx，并把Nginx所有的配置设置成现在机器上老Nginx的配置。

<pre lang="bash">curl -O http://sysoev.ru/nginx/nginx-0.7.62.tar.gz

tar -zxvf ./nginx-0.7.62.tar.gz

git clone git://github.com/mikewest/nginx-static-etags.git ./nginx-static-etags

cd nginx-0.7.62/

./configure --add-module=../nginx-static-etags --prefix=/usr --conf-path=/etc/nginx/nginx.conf --http-log-path=/var/log/nginx/access.log --error-log-path=/var/log/nginx/error.log --user=www-data --group=www-data --with-http_stub_status_module --with-http_ssl_module --sbin-path=/usr/sbin/nginx --pid-path=/var/run/nginx.pid --lock-path=/var/lock/nginx.lock --http-proxy-temp-path=/var/lib/nginx/proxy --http-fastcgi-temp-path=/var/lib/nginx/fastcgi

make

make install</pre>
效果：
<pre lang="bash">  nginx path prefix: "/usr/local/nginx"
  nginx binary file: "/usr/local/nginx/sbin/nginx"
  nginx configuration prefix: "/usr/local/nginx/conf"
  nginx configuration file: "/usr/local/nginx/conf/nginx.conf"
  nginx pid file: "/usr/local/nginx/logs/nginx.pid"
  nginx error log file: "/usr/local/nginx/logs/error.log"
  nginx http access log file: "/usr/local/nginx/logs/access.log"
  nginx http client request body temporary files: "client_body_temp"
  nginx http proxy temporary files: "proxy_temp"
  nginx http fastcgi temporary files: "fastcgi_temp"</pre>

### 2\. 然后配置Nginx以打开Etags和Expires

下面是一个server的一部分，把所有的静态元素加了Etags属性和Expires的时间。
<pre lang="bash">location ~ .(htm|html|gif|jpg|jpeg|png|bmp|ico|rar|css|js|zip|java|jar|txt|flv|swf|mid|doc|ppt|xls|pdf|txt|mp3|wma)$ {
      root /home/xq/kangzj.net/public_html/;
      FileETag on;
      expires 7d;
}</pre>
于是咱的首页也达到YSlow的A等级了，除了CDN做不了，其它全部A，总分92！晒下：

[![image](http://kangzj.net/wp-content/uploads/images/200910/fa2c2ceb7808_122F5/image_thumb.png "image")](http://kangzj.net/wp-content/uploads/images/200910/fa2c2ceb7808_122F5/image.png)