---
title: 服务器层次加速WordPress
tags:
  - nginx
  - php
  - server
  - wordpress
  - 服务器
id: 1081
categories:
  - Blogging
date: 2009-10-12 14:21:20
---

部分博友有自己的服务器或者VPS，这一部分加速WordPress的方法是针对VPS或者独立服务器的。链接了久酷同学几篇文章，谢谢久酷~

### 1\. 使用轻量级、高性能的Nginx

[Ubuntu 9.04 server用apt安装nginx并配置php(fastcgi)](http://kangzj.net/nginx_php_fastcgi_ubuntu/)

[nginx以unix-domain-socket方式连接fastcgi(php)](http://kangzj.net/nginx-socket-fastcgi-php/)

[Wp-Super-Cache在Nginx下配置](http://www.jiucool.com/wp-super-cache-nginx/)

[Nginx环境下supesite discuz wordpress静态化](http://www.jiucool.com/nginx-rewrite/)

<!--more-->

### 2\. PHP字节码缓存组件apc

JiuCool：《[VPS安装APC加速PHP](http://www.jiucool.com/apc-accelerate-php/)》

### 3\. 为网页静态元素设置过期时间（以Nginx为例）

<pre lang="php">location ~ .(htm|html|gif|jpg|jpeg|png|bmp|ico|rar|css|js|zip|java|jar|txt|flv|swf|mid|doc|ppt|xls|pdf|txt|mp3|wma)$ {
root /home/xq/kangzj.net/public_html/;
expires 2d;
}</pre>

### 4\. 增加Etags

HTTP协议规格说明定义ETag为“被请求变量的实体值” （参见[ http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) —— 章节 14.19）。 另一种说法是，ETag是一个可以与Web资源关联的记号（token）。典型的Web资源可以一个Web页，但也可能是JSON或XML文档。服务器单独负责判断记号是什么及其含义，并在HTTP响应头中将其传送到客户端。

### 5\. 一些负载均衡方法

这对访问量很大的网站十分有用，而我们小博客用一下，就是用来加速了，个人博客一般没有技术，告别是没有资金来玩这个。比如我做的：《[小博增加了一个海外镜像](http://kangzj.net/blog-has-a-mirror-now/)》。