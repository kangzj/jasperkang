---
title: WordPress“执行请求操作，连接信息必需提供”解决方法
tags:
  - fastcgi
  - nginx
  - php
  - wordpress
  - 无法升级
id: 1041
categories:
  - Blogging
date: 2009-10-01 22:48:23
---

把博客搬回来之后， 后台自动安装插件、删除插件和wordpress升级都不能用了，每次都会出现一个这样的提示“执行请求操作，连接信息必需提供”：

[![link-info](http://kangzj.net/wp-content/uploads/images/200909/c7429d4bb194_2C1E/linkinfo_thumb.jpg "link-info")](http://kangzj.net/wp-content/uploads/images/200909/c7429d4bb194_2C1E/linkinfo.jpg)

### <!--more-->

### 解决方法1：

把wordpress所有的文件所有者改成运行执行php的程序，像我的服务器fastcgi是这样开启的（spawn-fcgi -a 127.0.0.1 -p 9000 -C 10<span style="color: #ff0000;"> -u www-data</span> -f /usr/bin/php-cgi），跟nginx是同一个用户www-data，Ubuntu或者Debian可以用下面的命令改动所有者：
> <span style="background-color: #ffffff;">kangzj@localhost# sudo chown –R </span><span style="color: #ff0000;">www-data</span> public_html
更改之后再运行相关操作便不会再询问连接信息了，问题解决。

如果不确定是哪个用户在运行php的话，可以在后台上传个文件，然后查看它的所有者即可。

### [](http://kangzj.net/wp-content/uploads/images/200909/c7429d4bb194_2C1E/linkinfo_3.jpg)解决方法2：

输入你的主机的“连接信息”，wordpress会登录ftp或者sftp来做相应的操作。这项我没有实践，朋友们可以试一下。

关于sftp: 走ssh的类似ftp的协议，但是用户名和密码不是明文传输，比ftp要安全得多，但是要求你的主机支持ssh（很少有开放ssh的虚拟主机）。