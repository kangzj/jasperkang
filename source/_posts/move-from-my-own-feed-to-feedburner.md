---
title: 从WordPress提供的Feed转移到Feedburner
tags:
  - feed
  - feedburner
  - rss
  - wordpress
id: 833
categories:
  - Blogging
date: 2009-08-09 18:43:53
---

这里的程序不一定是指WordPress，所有的网站程序都是适用的。这里仅拿WordPress来举例说明一下。

WordPress以是否开启url rewrite区别，有两种种订阅地址：

1\. 开启了url rewrite: http://yourdomain.com/feed/

2.  未开启的：http://yourdomain.com/?feed=rss2

<!--more-->假设你用的是第一种的地址，申请的Feedburner的地址是：http://feeds.feedburner.com/kangzjnet

打开.htaccess（没有的新建一个就可以了），添加：
> RewriteCond %{HTTP_USER_AGENT} !^.*(FeedBurner|FeedValidator) [NC]
> RewriteRule /feed/ [http://feeds.feedburner.com/kangzjnet](http://feeds.feedburner.com/kangzjnet)
OK搞定，不会损失定户，转向了FeedBurner。第二种格式转向Feedburner，或者转向Feedsky也是差不多的。

说到这里，有问题请留言。说得不对的也请指出:-)