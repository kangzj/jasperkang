---
title: 配置php利用远程smtp服务器发送电子邮件
tags:
  - php
  - php-email
  - smtp
  - socket
id: 153
categories:
  - Web-Development
date: 2009-06-15 16:58:35
---

    php的特性，使我们可以很容易地利用网页来发送邮件，[配置php利用本地mail服务器发送电子邮件](http://kangzj.net/php-send-email-using-local/)十分简单，同样，[配置php利用远程mail服务器发送电子邮件](http://kangzj.net/php-send-email-using-remote)也很容易。php.ini中相关配置选项是[mail configuration]。只要将smtp服务器和你的电子邮件配置好就可以了（当然这里的服务器必须是没有验证的）。

    这里要注意一点，php中的mail函数利用远程smtp服务器发送邮件只有在windows系统才可用。在其它平台上，我们大可以直接用sendmail或者PEAR Mail Package等等。配置好了的话，大约是这样的：

[mail function]
SMTP = smtp.kangzj.net.ru
sendmail_from = [kangzj@kangzj.net.ru](mailto:kangzj@kangzj.net.ru)