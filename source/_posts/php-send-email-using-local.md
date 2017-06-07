---
title: 配置php利用本机发送电子邮件
tags:
  - php
  - php-email
  - sendmail
id: 151
categories:
  - Web-Development
date: 2009-06-15 16:35:57
---

    利用php脚本来发送电子邮件(email)是十分简单的，你只要正确配置下php.ini文件就可以了。如果你的机器的Windows的或者是*nix的而本机运行有smtp服务器的话，我们当然想直接利用了。

<!--more-->

    php.ini中相关的选项是[mail function]部分，名字是sendmail_path。这个值应该设为sendmail的路径，对于linux/unix的系统一般来说是/usr/sbin/sendmail或者是/usr/bin/sendmail（检查一下你的系统，确保是正确的）。你的配置文件这一部分大体是这样的：

[mail function]
sendmail_path = /usr/sbin/sendmail

如果你用的不是sendmail，而是qmail的话，就应该写成/var/qmail/bin/sendmail了。