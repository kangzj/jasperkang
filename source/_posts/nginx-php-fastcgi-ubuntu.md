---
title: Ubuntu 9.04 server用apt安装nginx并配置php(fastcgi)
tags:
  - fastcgi
  - nginx
  - php
  - ubuntu
id: 67
categories:
  - Systems&amp;Servers
date: 2009-05-18 14:14:18
---

转自：http://vpsblog.rashost.com/20080524-ubuntu-nginx/    “RASHOST VPS主机官方博客”
> 这篇文章是用http方式连接fastcgi，也可以用效率更高的unix domain socket - [nginx以unix-domain-socket方式连接fastcgi(php)](../nginx-socket-fastcgi-php/ "nginx以unix-domain-socket方式连接fastcgi(php)")
由于Ubuntu 904已经包含了nginx，所以根本不要编译，安装超简单！

修改/etc/apt/sources.list文件内容为国内镜像，然后运行：

apt-get update
apt-get install nginx

<!--more-->
即可完成安装

启动nginx：

/etc/init.d/nginx start
然后就可以访问了，http://localhost/ ， 一切正常！如果不能访问，先不要继续，看看是什么原因，解决之后再继续。

下面配置php和mysql。

安装php和MySQL:

apt-get install php5-cli php5-cgi mysql-server-5.0 php5-mysql
我们需要/usr/bin/spawn-fcgi这个文件，而它是属于lighttpd这个包里面的，所以我们安装lighttpd然后把它设置为开机不启动：

apt-get install lighttpd #我们只要/usr/bin/spawn-fcgi
rcconf #去掉lighttpd开机自启动
修改nginx的配置文件：/etc/nginx/sites-available/default
修改 server_name 58.30.17.154;
修改index的一行修改为：
index index.php index.html index.htm;

去掉下面部分的注释：

location ~ .php$ {
fastcgi_pass   127.0.0.1:9000;
fastcgi_index  index.php;
fastcgi_param  SCRIPT_FILENAME /var/www/nginx-default$fastcgi_script_name;
include /etc/nginx/fastcgi_params;
}
重新启动nginx:

/etc/init.d/nginx stop
/etc/init.d/nginx start
启动fastcgi php:

spawn-fcgi -a 127.0.0.1 -p 9000 -C 10 -u www-data -f /usr/bin/php-cgi
为了让php-cgi开机自启动：

cd /etc/init.d
cp nginx php-cgi
vim php-cgi
替换nginx为php-cgi
并修改相应部分为：

DAEMON=/usr/bin/spawn-fcgi
DAEMON_OPTS="-a 127.0.0.1 -p 9000 -C 10 -u www-data -f /usr/bin/php-cgi"
...
stop)
echo -n "Stopping $DESC: "
pkill -9 php-cgi
echo "$NAME."
然后运行rcconf设置php-cgi为开机自启动

在/var/www/nginx-default/目录下创建一个文件：

echo '&lt; ?phpinfo();?&gt;'  &gt; /var/www/nginx-default/index.php
然后浏览器访问nginx就可以看到一切正常了