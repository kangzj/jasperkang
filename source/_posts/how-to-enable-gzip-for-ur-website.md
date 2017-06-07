---
title: 如何开启Gzip压缩
tags:
  - apache
  - cpanel
  - direct admin
  - gzip
  - GZIP Output
  - gzippy
  - htaccess
  - http
  - nginx
  - php
  - wordpress
  - 加速
  - 压缩
id: 1206
categories:
  - Blogging
date: 2009-10-29 06:09:20
---

Gzip压缩效率非常高，通常可以达到70%的压缩率，也就是说，如果你的网页有30K，压缩之后就变成了9K左右，好处有二：

*   可以节省带宽资源；
*   [加快加载速度](http://kangzj.net/to-accelerate-wordpress-on-html-level/)。
节省带宽这个对大多数人来说没什么，加快你网页的加载速度确是普适的。前面看到许多朋友都在介绍如何开启Gzip，但是个人感觉方法不甚全，听我给大家道来：

方法大概有三：在Contol Pannel开启Gzip、开启http服务器Gzip、利用php本身的Gzip。

### 1\. 在Contol Panel开启Gzip

#### 1.1 CPanel中开启Gzip

在“SoftWare and Services”那一栏中“Optimize Website”：

![](http://kangzj.net/wp-content/uploads/images/200910/opt-web.jpg "Optimize Website")

<!--more-->

![](http://kangzj.net/wp-content/uploads/images/200910/com-con.jpg "Compress Content")

默认情况只压缩框中的三种[MIME类型](http://kangzj.net/iis6-mime/)，我们选择成Compress all content的话，css和js就也可以被压缩了。当然控制面板的Gzip压缩是基于服务器的，控制面板只不过提供一个友好的接口而已，如果你的技术盲，用控制面板开启Gzip是最好的方法了。

#### 1.2 Direct Admin中开启Gzip

DA在面板中MS没有Gzip压缩的选项，不过可以在.htaccess中开启，打开.htaccess，添加下列的行：
<pre lang="shell">    SetOutputFilter DEFLATE
    AddOutputFilterByType DEFLATE text/html text/css image/gif image/jpeg image/png application/x-javascript</pre>
这样过瘾了，不但php,html,js,css等开启了压缩，连图片都开启了Gzip压缩。

### 2\. 开启http服务器Gzip

只玩过Apache和Nginx，所以只介绍这两种服务器开启Gzip压缩的方法：

#### 1.1 Apache开启Gzip

需要加载deflate模块，如果开启了AllowOverride All的话，可以直接按照在DA中修改.htaccess的方式来开启Gzip压缩。如果没有开启的话，就需要直接写在httpd.conf里面了，不多讲了。

#### 1.2 Nginx开启Gzip

Nginx默认是开启Gzip的，但是他只压缩有限的几种类型，需要我们增加几种，打开nginx.conf，找到下面的行，并修改（没有的请添加）：
<pre lang="shell">    # output compression saves bandwidth
    gzip              on;
    gzip_proxied      any;
    gzip_http_version 1.1;
    gzip_min_length   1100;
    gzip_comp_level   5;
    gzip_buffers      8 16k;
    gzip_types        text/plain text/xml text/css application/x-javascript application/xml application/xml+rss text/javascript application/atom+xml;
    gzip_vary        on;
    #gzip_disable     "MSIE [1-6].";</pre>
gzip_com_level不需要设置成很高，3即可，5的话太耗CPU资源，压缩的效果也不会有什么大的上升。至于比较，大家可以在[Gzip 检测页面](http://www.gidnetwork.com/tools/gzip-test.php)查看各个压缩级别的压缩率，便于选择。

### 3\. 利用php本身的Gzip

这个并不提倡，因为php的效率比服务器端的压缩还是有很大差距的，但是如果服务器不支持Gzip压缩的话，就只能用这种方法来开启Gzip。

#### 1.1 对于WordPress可以安装Gzip相关插件

比如wp super cache中就有Gzip压缩的功能。也有专门的Gzip压缩插件，比如：Gzippy、GZIP Output等。

#### 1.2 修改WordPress源码，增加Gzip功能

不推荐，因为每次升级之后还要再修改一次，很麻烦，不做介绍。想做的话可以参考万戈：[开启GZIP，提速Wordpress](http://www.life-studio.cn/turn-on-gzip-speed-up-wordpress.html)。