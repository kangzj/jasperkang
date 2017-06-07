---
title: nginx以unix-domain-socket方式连接fastcgi(php)
tags:
  - fastcgi
  - linux
  - nginx
  - php
  - spawn
  - ubuntu
  - unix-socket
id: 400
categories:
  - Systems&amp;Servers
date: 2009-07-22 20:41:36
---

前面已经介绍过[Ubuntu 9.04 server用apt安装nginx并配置php(fastcgi)](../nginx_php_fastcgi_ubuntu/ "Ubuntu 9.04 server用apt安装nginx并配置php(fastcgi)")，不知道大家看到没，在文章中nginx连接fastcgi的方式是http方式的，在linux还有一种速度更快的方法就是通过**unix domain socket**来完成，下面介绍这种方法：

首先建立/tmp/php-cgi.sock文件，然后将之改所有者改为www-data：
> #我直接改成nginx的用户，好像必须要属于nginx的用户组才能正常使用未验证
> sudo chown www-data /tmp/php-cgi.sock
<!--more-->
找到nginx.conf，如果你用的是虚拟机，那么就到/etc/nginx/site-available里改相关文件：
> 修改：
> # fastcgi_pass <span style="color: #ff0000;"> 127.0.0.1:9000</span>;
> fastcgi_pass   <span style="color: #ff0000;"><span style="color: #0000ff;">unix:</span>/tmp/php-cgi.sock</span>;
找到init.d/php-cgi(参考文章开关提到的文章[](../nginx_php_fastcgi_ubuntu/ "Ubuntu 9.04 server用apt安装nginx并配置php(fastcgi)"))：
> 修改：
> #DAEMON_OPTS="-a 127.0.0.1 <span style="color: #ff0000;">-p 9000</span> -C 1 -u www-data -f /usr/bin/php-cgi"
> 
> DAEMON_OPTS="-a 127.0.0.1 <span style="color: #ff0000;">-s /tmp/php-cgi.sock</span> -C 1 -u www-data -f /usr/bin/php-cgi"
然后分别重启nginx 和 spawn-fcgi即可，你的nginx效率就更高啦！:-)