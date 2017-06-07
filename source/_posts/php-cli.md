---
title: php-cli简介——不会Shell语言，一样用Shell！
tags:
  - cron
  - linux
  - php
  - php-cli
  - preminder
  - shell
  - 命令行
id: 916
categories:
  - Systems&amp;Servers
date: 2009-09-08 23:16:11
---

### 1.基础知识

#### 1.1 什么是Shell编程?

在 Unix 中，shell 可不是简单的命令解释器（典型的有 Windows 中的 DOS ），而是一个全功能的编程环境。Shell 是操作系统的一部分，用来与用户打交道，并且可以用来协调各个命令【1】。用Shell编程可以灵活地解决大量重复任务，十分方便。但是，Shell的语法十分怪异（个人意见），不容易记，如果现在熟悉的语言可以用来写shell那就好了——比如php——就可以快速开发Shell程序了（比如我的[Preminder](http://apps.kangzj.net/preminder/)的后台程序），于是便有了这篇文章，本文以Linux为例说明php-cli的用法，其它平台的版本类似。

#### 1.2 什么是php-cli?

刚才说到，我们可以用php来开发Shell程序。有的同学可能会问啦：“php不是用来做网页的么？-_-”。是的，php可以用来做动态网页，并且当初php就是为做动态网页而开发的语言，但是理论上php可以用来做任何的程序，甚至是桌面程序，而**php-cli**是php在命令行运行的支持环境，也就是我们说的可以用来写Shell的环境支持。
> **php-cli**是php Command Line Interface的简称，如同它名字的意思，就是php在命令行运行的接口，区别于在Web服务器上运行的php环境（php-cgi, isapi等）【2】。
也就是说，php不单可以写前台网页，它还可以用来写后台的程序。

<!--more-->

### 2\. 执行php-cli脚本

#### 2.1 php-cli的语法

当然是跟php一模一样啦，因为它就是php嘛！只不过一些默认的参数与php-cgi不同，比如运行时间：php-cli默认运行时间是无穷，而网页php默认设置是30s。

#### 2.2 执行php-cli脚本

##### 2.2.1\. 直接在终端执行php

<pre lang="shell">kangzj@localhost# php -r 'print_r(get_defined_constants());'</pre>

##### 2.2.2\. 运行php-cli脚本文件

<pre lang="shell">kangzj@localhost# php my_script.php

kangzj@localhost# php -f my_script.php</pre>
上而说的php文件就是一般的php文件没有什么不同。还有一种方式，就是在文件中指令解释器，就可以直接在终端以”./test.php执行脚本了”，test.php就像下面这样：
<pre lang="php">#!/usr/bin/php -q
&lt;?php
  echo "Hello world of PHP CLI!";
?&gt;</pre>
补充：php的Shell程序并不一定以php为扩展名，可以以任意扩展名，甚至不要扩展名，只是为了清楚，我才用的php扩展名。

##### 2.2.3\. 用Cron执行php-cli脚本

[cron是一个linux下的定时执行工具，可以在无需人工干预的情况下运行作业](http://kangzj.net/linux-cron/)，周期性作业，比如备份数据，[Preminder](http://apps.kangzj.net/preminder/)定期查询PR等等，添加的方法：打开/etc/crontab，添加：
<pre lang="shell">0 13 * * * /usr/bin/php -f /home/phpscripts/phpcli.php</pre>

### 4\. 结语

如果你会php的话，那么你也会了一种Shell编程语言！

如果你不会php，你去学php，就相当于一下子学会动态网页和Shell两种语言！并且你甚至可以用php来写具有图形界面的应用程序，Dnspod的动态域名客户端中就有一种是用php开发的。

php的易学是出名的，如果你还不会，那是在犹豫什么呢？

另外，再宣传一下我的”[Preminder](http://apps.kangzj.net/preminder/)”——PR更新Email提醒服务~~

### 5\. 参考文献

1.  Linux Shell简介 ： [http://www.linuxsir.org/main/?q=node/135](http://www.linuxsir.org/main/?q=node/135 "http://www.linuxsir.org/main/?q=node/135")
2.  PHP Command Line Interface : Mystic Unleashed ：[http://www.php-cli.com/](http://www.php-cli.com/ "http://www.php-cli.com/")
3.  ch 4.2， php manual ： [http://www.php.net](http://www.php.net)
PS：Shell命令还是要知道一些的，否则有些功能不太好实现。