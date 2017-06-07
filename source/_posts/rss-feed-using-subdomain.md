---
title: WordPress中用feed子域名来发布RSS Feed的方法
tags:
  - feed
  - php
  - rss
  - wordpress
  - 域名
  - 子域名
id: 335
categories:
  - Blogging
date: 2009-07-19 11:53:42
---

发布RSS Feed到feed二级子域名有很多种方法。jorwang提供了一种用解决方案：[新建一个虚拟主机，新建一个index.php，然后用readfile加载rss](http://jorwang.com/htm/314.htm "另一种方法")。我也来提供一种方法，核心方法和jorwang相同，但是不需要新建一个站点。

如果你不能像jorwang一样新建一个站，你就用我的方法吧：

1\. 把你的feed.xxx.com域名指向你的主域名如www.xxx.com（可以建一个cname）， 然后给你的虚拟主机添加别名feed.xxx.com(DirectAdmin中叫做绑定新域名)。

2\. WordPress的rewrite都是先加载index.php的，于是乎我们可以通过index.php来检测和处理域名。
<!--more-->
打开index.php，**在最开始**加上这么几句：
> $host = $_SERVER['HTTP_HOST'];
> if($host=='feed.xxx.com')
> {
>      @readfile('http://xxx.com/feed/');
>      exit;
> }
OK，搞定，就这么简单！现在就可以用子域名http://feed.xxx.com来发布你的RSS Feed了！
_注：以后升级完的时候注意检查下index.php有没有被修改，如果被修改了的话，再照本文加一次即可。_