---
title: SUSE_10下apache+php+mysql配置指南
tags:
  - apache
  - linux
  - mysql
  - php
  - suse
id: 83
categories:
  - Systems&amp;Servers
date: 2009-05-29 02:23:25
---

apache,php,mysql都是随系统装上去的，装好了之后，把网站放上去竟然不行，于是同学便来找我帮忙看看。

 SUSE里apache的默认配置文件还真是不一样，是放在/etc/apache2下面，不借一般的RedHat啥的都是放在/etc/httpd/conf下面。并且，suse把apache的配置文件拆成了N多个，有一主配置文件httpd.conf(这个名字倒是一样，不过乍一见也真是接受不了)，它把其它所有的文件全都include进去了，于是这个文件便成了“不建议修改”的文件了。简单的介绍下几个主要的置文件吧：
 <!--more-->

加载模块管理：/etc/apache2/sysconfig.d/loadmodule.conf

更改监听的端口：/etc/apache2/listen.conf

默认的主机：/etc/apache2/default-server.conf

更改apache运行的用户：/etc/apache2/uid.conf

所有的虚拟机配置文件：/etc/apache2/vhost.d/ 下面，每个主机一个文件，可以打开其默认的文件当做参考

其它配置可以加在conf.d/下面。比如，安装php支持，编译安装自然不用说了，然后在loadModule里加一条，然后在conf.d/下面，新建一个php5.conf，内容： 
<pre>

1.  <span><span>&lt;IfModule mod_php5.c&gt;  </span></span>
2.  <span>        AddHandler application/x-httpd-php .php4  </span>
3.  <span>        AddHandler application/x-httpd-php .php5  </span>
4.  <span>        AddHandler application/x-httpd-php .php </span><span style="color: #ff0000;"><span>.html  </span></span>
5.  <span>        AddHandler application/x-httpd-php-source .php4s  </span>
6.  <span>        AddHandler application/x-httpd-php-source .php5s .htmls  </span>
7.  <span>        AddHandler application/x-httpd-php-source .phps  </span>
8.  <span>        DirectoryIndex index.php4  </span>
9.  <span>        DirectoryIndex index.php5  </span>
10.  <span>        DirectoryIndex index.php  </span>
11.  <span>&lt;/IfModule&gt; </span>
</pre>
可以看到，我把.html文件交给了php程序解释了，这样可以做到直接在.html文件里写php程序，正常解释执行，让人看不出网页到底是用什么设计的，并且不会影响到正常的.html文件(只是效率可能会低那么一小点点)，呵，有意思吧~~~

还有几个要注意的问题，这里一并说了：

1.  要给.html文件以执行权限，可以这样： chmod 755 -R /srv/www/htdocs 给所有文件执行权限；
2.  打开/etc/php5/cli/php.ini 把display_errors打开，否则如果一旦页面执行有错，服务器只会返回500错误(服务器内部错误)，而不显示php脚本的具体错误，不利于调试。甚至让人觉得服务器好像不支持php的错觉。
自带的 mysql 只要chkconfig mysql on设置成自启动即可，然后最好装一个phpmyadmin便于管理~~

全文完，有问题请留言。