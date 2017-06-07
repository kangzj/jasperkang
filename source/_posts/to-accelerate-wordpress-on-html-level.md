---
title: html代码层次加速WordPress
tags:
  - html
  - wordpress
  - YSlow
  - 加速
id: 1082
categories:
  - Blogging
date: 2009-10-12 14:21:37
---

相比[php代码层次加速WordPress](http://kangzj.net/to-accelerate-wordpress-on-php-level)，html层次上的优化更加重要一些。因为现在的服务器配置都很牛，php执行效率也很高，除非你的WordPress插件多得太离谱，在速度上一般是不会有太多大的影响的（基本上1m以内可以执行完）。而html代码决定了WordPress加载的速度，浏览你博客的速度在很大程度上是这个因素决定的（在同样的网络环境下），用户加载网页的时间有80%花在这上面。要想你的WordPress飞速跑起来，html层次的优化是非常必要的。

### 1\. 使用的工具-YSlow

_Why Slow_是雅虎制作的用来检测你的网站_为什么_会加载_慢_的FireFox插件，html层次的优化还要以它作为指导。下面就以YSlow检测的各个方面，也就是html层次加速的各个方面展开描述。

<!--more-->

### 2\. Make Fewer HTTP Requests - 减少HTTP请求的数量 <span style="color: #ff0000;">※</span>

这是加速你的网页的**关键**，HTTP请求是很浪费时间的，网页中每个对象的加载都要经过建立连接的过程，对象很多的话，累积的时间是惊人的。为此，可以：

*   合并JS，CSS文件。一般来说，每个站都有一套css和js，在每个页面都要加载，合并会给整个站加速。
*   合并切割成小块的图像。
*   在CSS里设置背景图像。
*   区分每个页面加载的css和js，在需要的时候再加载。可以参考林木木：《[小站提速手记之 —— 按需加载 CSS](http://immmmm.com/notes-of-station-speed-demand-load-css.html)》和万戈：《[WP 提速之按需合并压缩 JS 文件](http://www.life-studio.cn/on-demand-combined-compressed-js.html)》

### 3\. Compress Components With Gzip - 用Gzip压缩网页 <span style="color: #ff0000;">※</span>

这项属于[php代码层次加速](http://kangzj.net/to-accelerate-wordpress-on-php-level)的范畴，请稳步查看。

### 4\. Put CSS at Top &amp; Put Js at Bottom - 把CSS放在开头，把JS放在结尾 <span style="color: #ff0000;">※</span>

Yahoo!的统计表明，把CSS放在开头的话可以加快网页渲染的速度。JS文件一般来说较大，而浏览器同时下载元素的数目是有限制的（IE好像是6个），大的JS文件会妨碍其它重要元素的加载。但是有时JS文件中含有document.write等代码，不能放在网页最后也是没有办法的事情。如果JS放在开头而又不想浏览器先加载的话可以用deferred属性，可以起到跟放在网页结尾一样的效果，但是FireFox并不支持这一属性。

### 5\. Avoid CSS Expressions - CSS中不要使用表达式

CSS是一种十分强大的工具，它可以支持动态的表达式。CSS中的表达式会造成很严重的问题，它们不只在网页加载的时候进行运算，甚至在用户动鼠标的时候也会计算。CSS可以统计表达式被运行的次数，在网页上经常动鼠标引起的表达式的运行会达到10,000之多，运行次数数量之大让人吃惊。

### 6\. Make CSS and JS External - 不要把CSS和js直接写入网页中，应加载外部

因为CSS和JS浏览器一般会有缓存，不必每次都从服务器加载，并且也可以减少每个网页的体积。

### 7\. Reduce DNS Lookups - 减少DNS查询的数量

DNS查询也是需要时间的，一个网页中加载的元素最好不要使用太多不同的域名。

### 8\. Minify Javascript and CSS - 去除JS和CSS中的冗余

减小JS和CSS体积以减少加载时间，这个很好理解。参考万戈：《[用 Page Speed 检测多余的 CSS](http://www.life-studio.cn/testing-unused-css-with-page-speed.html)》

### 9\. Avoid URL Redirecting - 减少重定向

重定向增长了加载时间，降低了用户体验。

### 10\. Used Cookie Free Domains  - 用不会传递Cookie的域名 <span style="color: #ff0000;">※</span>

浏览器会对作用域内每个加载的对象传递Cookie，在加载图像或者JS、CSS的时候最好用Cookie-free域名。如果没有多余的域名可以用一个子域实现，但是要设置Cookie的作用域才可以。打开wp-config.php：
<pre lang="php">define('COOKIE_DOMAIN', 'kangzj.net');</pre>
把kangzj.net换成你博客的域名，这样你的所有子域就Cookie-free了。

### 11\. 外部加载部分元素 <span style="color: #ff0000;">※</span>

外链不但可以节省流量，而且可以利用优势的服务器资源，给WordPress加速。

(1) 从Google加载JQuery库：
<pre lang="javascript"><script type="text/javascript" src=http://www.google.com/jsapi"></script>
<script language="javascript" type="text/javascript" &gt;google.load("jquery","1.3.2");</script></script></pre>
或者：
<pre lang="javascript"><script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.3.2/jquery.min.js"></script></pre>
如果加载别的库可以点击这里查看：[http://code.google.com/apis/ajaxlibs/documentation/index.html](http://code.google.com/apis/ajaxlibs/documentation/index.html "http://code.google.com/apis/ajaxlibs/documentation/index.html")

(2) 做个图床，外链图片： [http://kangzj.net/what-is-tu-chuang/ ](http://kangzj.net/what-is-tu-chuang/)

做完这些之后可以评估一下加速的效果，看看加载时间是不是有显著的提高：

[![YSlow-kangzj.net1](http://kangzj.net/wp-content/uploads/images/200909/067b0457c51b_B238/YSlowkangzj.net1_thumb.jpg "YSlow-kangzj.net1")](http://kangzj.net/wp-content/uploads/images/200909/067b0457c51b_B238/YSlowkangzj.net1.jpg)

PS：文中加<span style="color: #ff0000;">※</span>的为很容易实现。

参考：[http://developer.yahoo.com/performance/rules.html](http://developer.yahoo.com/performance/rules.html)