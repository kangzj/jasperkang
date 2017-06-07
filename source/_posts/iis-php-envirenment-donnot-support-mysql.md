---
title: IIS6配置的PHP环境不支持Mysql的解决方法
tags:
  - iis6
  - mysql
  - php
id: 873
categories:
  - Systems&amp;Servers
date: 2009-09-04 01:18:57
---

真的很郁闷，按照以前配置方法配置IIS6：

1\. 把php.ini复制到Windows目录，并更改extension目录位置为php目录的位置，并加载相应的dll；

2\. 把IIS6添加.php的处理器；在扩展中允许.php；重启IIS。

按说这样的设置已经可以，看了phpinfo，发现所有的模块都支持了，唯独不支持Mysql。这我可就郁闷了，以前都是没有问题的啊。没有办法，上网搜搜，结果发现还要**<span style="color: #ff0000;">把libmysql.dll复制到System32下</span>**，记录一下。

参考：[http://blog.samxy.com/post/2009/05/54.html](http://blog.samxy.com/post/2009/05/54.html)