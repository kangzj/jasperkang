---
title: 加速WordPress
tags:
  - html
  - php
  - wordpress
  - 加速
  - 提速
  - 服务器
  - 浏览器
  - 静态
id: 1084
categories:
  - Others
date: 2009-10-12 14:22:15
---

走动挺多的博友中有几个加速癖，以[万戈](http://www.life-studio.cn/)、[林木木](http://immmmm.com/)为首的几个家伙更是加速狂人，我要是不加加速岂不是太out了。于是乎，咱做起了科研，写了这篇文章。

用户网页加载时间分为三部分：
> 网页执行时间+页面及页面元素加载时间+浏览器渲染网页时间
针对这三部分时间，我将加速的方法依加速的方式分成以下几类：[php代码层次加速](http://kangzj.net/to-accelerate-wordpress-on-php-level/)，[html代码层次加速](http://kangzj.net/to-accelerate-wordpress-on-html-level/)，[服务器层次加速 ](http://kangzj.net/to-accelerate-wordpress-on-server-level/)，鼓励你的用户放弃IE :mrgreen:

<!--more-->

### 1\. [php代码层次加速WordPress](http://kangzj.net/to-accelerate-wordpress-on-php-level)

所谓“php代码层次”是指php执行效率，执行查询数量层次上的优化。我将方法归纳了几点：

1.  控制插件数量
2.  使用缓存插件

    1.  数据库查询缓存：DB Cache
    2.  静态页面缓存：WP Super Cache / Cos Html Cache
    3.  部分页面缓存：WP Widget Cache

3.  优化主题
4.  启用Gzip压缩

### 2\. [html代码层次加速WordPress](http://kangzj.net/to-accelerate-wordpress-on-html-level/)

相比php代码层次加速WordPress，html层次上的优化更加重要一些。因为现在的服务器配置都很牛，php执行效率也很高，除非你的WordPress插件多得太离谱，在速度上一般是不会有太多大的影响的（基本上1m以内可以执行完）。而html代码决定了WordPress加载的速度，浏览你博客的速度在很大程度上是这个因素决定的（在同样的网络环境下），用户加载网页的时间有80%花在这上面。要想你的WordPress飞速跑起来，html层次的优化是非常必要的。

1.  Make Fewer HTTP Requests - 减少HTTP请求的数量 ※
2.  Compress Components With Gzip - 用Gzip压缩网页 ※
3.  Put CSS at Top &amp; Put Js at Bottom - 把CSS放在开头，把JS放在结尾 ※
4.  Avoid CSS Expressions - CSS中不要使用表达式
5.  Make CSS and JS External - 不要把CSS和js直接写入网页中，应加载外部
6.  Reduce DNS Lookups - 减少DNS查询的数量 ※
7.  Minify Javascript and CSS - 去除JS和CSS中的冗余
8.  Avoid URL Redirecting - 减少重定向
9.  Used Cookie Free Domains  - 用不会传递Cookie的域名 ※
10.  外挂部分元素 ※

### 3\. [服务器层次加速WordPress](http://kangzj.net/to-accelerate-wordpress-on-server-level/)

部分博友有自己的服务器或者VPS，这一部分是针对VPS或者独立服务器的。

1.  使用轻量级、高性能的Nginx
2.  PHP字节码缓存组件apc
3.  为网页静态元素设置过期时间（以Nginx为例）
4.  header中增加Etags和Expires
5.  其它负载均衡方法

### 4\. 鼓励你的用户放弃IE，间接加速WordPress

鼓励他们使用FireFox、Opera、Chrome等高性能浏览器。 :grin:

<span style="color: #800000;">你的WordPress飞起来没有？</span>