---
title: 'PHP Speedy : 加多少Cache你也快不过我！'
tags:
  - PHP Speedy
  - PHP Speedy WP
  - wordpress
  - WordPress优化
  - YSlow
  - 加速
id: 1470
categories:
  - Web-Development
date: 2009-12-06 01:17:59
---

![php_speedy_logo_medium](http://kangzj.net/wp-content/uploads/images/200912/YSlowAphp_speedy_10FA/php_speedy_logo_medium_thumb.gif "php_speedy_logo_medium")前些日子曾经写过一篇博文《[加速WordPress](http://kangzj.net/methods-to-accelerate-wordpress/)》，完全用手工来调整，加速我们的WordPress，[html代码层次加速WordPress](http://kangzj.net/to-accelerate-wordpress-on-html-level/)是其中最为有效的手段。即使你的全静态页面，如果一个网页中加载过多js, css的话，也会慢得要命。

下面有朋友留言问，是不是有插件可以自动进行这些优化，我当时没有发现有类似插件。今天终于被我找到了，没错，就是**PHP Speedy **! 装了YSlow的同学可以先测下我博客的所有页面，绝对全都是A，如果你发现有不是A的，告诉哥，哥赏糖吃你，吼吼！

<!--more-->

先说下PHP Speedy的主要功能：

PHP Speedy扫描博客加载的js, css，并将它们合并压缩，减少HTTP请求数量，以加快博客的加载速度。下面是一组对比：

下面是未用PHP Speedy时网页加载的时间流图，14个HTTP请求，总共花去了4.44秒：[![uncompressed-small](http://kangzj.net/wp-content/uploads/images/200912/YSlowAphp_speedy_10FA/uncompressedsmall_thumb.gif "uncompressed-small")](http://kangzj.net/wp-content/uploads/images/200912/YSlowAphp_speedy_10FA/uncompressedsmall.gif)

下面是用PHP Speedy之后网页加载的时间流图，只有4个HTTP请求，只用了1.1秒：

[![compressed-small](http://kangzj.net/wp-content/uploads/images/200912/YSlowAphp_speedy_10FA/compressedsmall_thumb.gif "compressed-small")](http://kangzj.net/wp-content/uploads/images/200912/YSlowAphp_speedy_10FA/compressedsmall.gif) 使用之后，网页加载的速度快了4倍！咱们用YSlow测下，看评分怎么样：

[![compressed_yslow](http://kangzj.net/wp-content/uploads/images/200912/YSlowAphp_speedy_10FA/compressed_yslow_thumb.gif "compressed_yslow")](http://kangzj.net/wp-content/uploads/images/200912/YSlowAphp_speedy_10FA/compressed_yslow.gif)** 96分！A等级！！**而之前，这个网页的得分只有44分，是个F，惊人吧！由F优化成A，只是装了一个插件而已，完全告别苦苦的手工调整优化，爽吧。

最后，当然是放出这个WordPress PHP Speedy插件的下载地址啦：[http://aciddrop.com/2008/07/15/php-speedy-wp-version-047-works-with-wp26/](http://aciddrop.com/2008/07/15/php-speedy-wp-version-047-works-with-wp26/ "http://aciddrop.com/2008/07/15/php-speedy-wp-version-047-works-with-wp26/")

安装之后，后台启用即可。该插件的功能相当强大，就不一一详述，有问题可以留言讨论。

PS：PHP Speedy不但可以用于WordPress，它可以用于任何PHP项目，详情参见：[http://aciddrop.com/php-speedy/](http://aciddrop.com/php-speedy/)

注：本文使用图片归PHP Speedy作者所有。

<span style="color: #800000;">再PS：发现PHP Speedy会增加0.5s左右的执行时间，我想这也就是Lc.说得变慢的原因吧，查查他的代码，看看是怎么回事，嗯~</span>

现在我博客是PHP Speedy + WP Super Cache，无敌了，所有页面秒开！！
