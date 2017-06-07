---
title: php-socket编程通过smtp服务器发送电子邮件
tags:
  - php
  - php-email
  - sendmail
  - smtp
  - socket
id: 157
categories:
  - Web-Development
date: 2009-06-15 16:59:11
---

   [配置php利用本机发送电子邮件](http://kangzj.net/php-send-email-using-local/)和[配置php利用远程smtp服务器发送电子邮件](http://kangzj.net/php-send-email-using-remote-smtp/)在发送电子邮件的时候用的都是php中的mail函数，而这篇文章中据说的，是利用php中的socket编程来连接smtp服务器，从而发送邮件，相当于是用php写了一个发送email的客户端。网上流行的几个php的邮件类，可以完成这样的功能，比如：

<!--more-->
> swiftmailer
> 
>      一个完全采用面向对象编码用于发送e-mail的PHP函数库。Swift不依赖于PHP的mail()函数，因为用它发送多封邮件时会占用较高的服务器资源。Swift通过直接连到SMTP服务器或MTA能够更快，更高效地发送邮件。
> 
>     官方网站：[http://www.swiftmailer.org/](http://www.swiftmailer.org/)
    Discuz!源码中也有相关的代码，有兴趣的可以找出来看看。最后附上我写的一个php程序，用来发群发email的：[点击下载](http://blog.kangzj.net/wp-content/uploads/2009/06/email.rar)

如果使用中有问题，可以留言讨论。