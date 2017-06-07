---
title: 把自己的博客作了教育网反向代理
tags:
  - dnspod
  - linux
  - nginx
  - 反向代理
  - 教育网
id: 808
categories:
  - Systems&amp;Servers
date: 2009-08-29 00:05:00
---

原先一直以为自己的博客教育网能上，前两天到“[HOUKAI](http://houkai.com)”博客跟他交换链接时，houkai竟然上不了我的博客…鼓捣了半天，终于在教育网架了个反向代理，教育网内直接访问无阻啦~

[![20090829-reverse-proxy-edu](http://kangzj.net/wp-content/uploads/images/200908/b6373bcd1f7b_1239B/20090829reverseproxyedu_thumb.jpg "20090829-reverse-proxy-edu")](http://kangzj.net/wp-content/uploads/images/200908/b6373bcd1f7b_1239B/20090829reverseproxyedu.jpg)
<!--more-->
> 其中，橙色的机器是我在小张那里买的服务器，教育网不能访问；
>
> 其中，服务器A为一台北京电信服务器，跟上海电信之间的连接速度很不错，与教育网不能直接连接，但是与校内教育网服务器B直接有路由；
>
> 其中，服务器B为校内一台教育网服务器。
大家看到图可能就明白了，我作了两重的反向代理才完成这项功能的，哈哈。反向代理用的是nginx(最近对它很是着迷，[怎么设置反向代理？](http://kangzj.net/nginx-php-jsp-asp-aspx/))。

上面的设置完了，但是不能把域名指向服务器B，因为这台服务器只有教育网能访问，于是——智能DNS就派上了用场，我用的是[Dnspod](http://www.dnspod.com)的智能DNS。把域名教育网线路的IP改成服务器B的IP即可！

[![20090829-dnspod-kangzj.net](http://kangzj.net/wp-content/uploads/images/200908/b6373bcd1f7b_1239B/20090829dnspodkangzj.net_thumb.jpg "20090829-dnspod-kangzj.net")](http://kangzj.net/wp-content/uploads/images/200908/b6373bcd1f7b_1239B/20090829dnspodkangzj.net.jpg)

打完收工，教育网的同学可以飞速访问我的博客了，我自己访问自己的博客连网关都不用过了，爽呀~~

常来本人小博的同学们，如果你们也是教育网，上国际不方便（而博客又在国际）或者想给教育网加速，告诉我，我也给你作个反向代理哈~

PS：两台服务器还都算稳定，至少90% Uptime.

好啦，到了提问时间了，要想正常访问我的博客，服务器B还应该有个什么设置呢？答对有奖:-)
