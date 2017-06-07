---
title: php代码层次加速WordPress
tags:
  - gzip
  - GZIP Output
  - gzippy
  - php
  - wordpress
  - 主题
  - 插件
  - 缓存
id: 1083
categories:
  - Blogging
date: 2009-10-12 14:21:45
---

所谓“php代码”是指php执行效率，执行查询数量上的优化。我将方法归纳以下几点：

### 1\. 控制插件数量

做过插件的朋友都知道，插件是通过添加一系列的filer或者action来实现功能的。比如大家很熟悉的All in one SEO，每个页面加载title完之后便会调用它的代码以显示页面的描述、关键字等信息。如果插件很多的话，每次调用都会有很大一个调用列表，程序执行时间自然会变得较长。

所以，控制插件数量在加速WordPress上有很大的作用（当然缓存类的插件除外）。看看大家都在用什么插件：

1.  万戈：[《我的 Wordpress 插件秀》](http://www.life-studio.cn/my-wordpress-plugins-show.html)
2.  蓝冰：[《我正在使用中的WP插件》](http://vvvvvv.us/567.html)，蓝冰说换了好多了，权当参考就得了
3.  Kangzj：《Kangzj正在使用的插件们》coming soon...
万戈同学属加速狂类型的，他的原则是能不用插件则不用插件。对于这一点我是部分认同的部分反对的，个人觉得对于用插件应该：

*   能修改主题代码可以实现的，可以不用插件实现（优点是速度相对快，缺点是换主题相当不方便）；如果要修改核心代码者，绝对要用插件实现（否则以后升级WordPress那是相当的麻烦）。
<!--more-->

### 2\. 使用缓存插件

缓存插件有多种，按按照缓存内容的不同可以分为三类：数据库查询缓存、静态页面缓存、部分页面缓存。下面介绍几个典型的缓存插件，大家可以参考使用。

#### 2.1\. 数据库查询缓存：DB Cache

DB Cache缓存数据库查询到文件中，减少数据库查询以达到加速的目的。

#### 2.2\. 静态页面缓存：WP Super Cache / cos html cache

WP Super Cache：WP Cach和Super Cache结合的产物，页面缓存用得最多的应该就是这个插件了。功能强大，还提供gzip压缩。

Cos Html Cache：国人cosbeta作品，缓存页面以加速。

#### 2.3\. 部分页面缓存：WP Widget Cache

WP Widget Cache：仅缓存Widget内容，对于Widget占用大量资源的情况很有效。

同学们可能会问，已经有了强大的静态页面缓存，为什么还要有数据库查询缓存、Widget Cache等这样的缓存插件呢？其实答案很简单，有部分的插件必须在动态页面才可以执行，在静态页面缓存中发挥不了作用，这样的时候DB Cache和Widget Cache就能派上用场了。举个例子：Ozh' Who Sees Ads，这个插件根据来源不同决定是否显示广告，只对从搜索引擎来的一次性访客显示广告（既经常访问的用户隐藏烦人的广告，又可以减少展示次数以提高单价）。

### 3\. 优化主题

主题中有大量的类似于
<pre lang="php">&lt; ?php bloginfo('charset'); ?&gt;</pre>
的代码，可以用直接用实际值来替换，以减少代码的量以提高速度。

### 4\. 启用Gzip压缩

WordPress2.5以前内置Gzip功能，后来去除了。启用Gzip压缩可以大大减少传输数据量（通常压缩率可以达到70%以上）。

1.  **[Louis Han](http://louishan.com/)**：《[WordPress 2.8开启Gzip压缩功能](http://louishan.com/articles/enable-gzip-compress-for-wordpress-2-8.html)》，不但页面可以gzip，css，js也可以。
2.  可用插件：GZIP Output 、CSS Compress、WP Super Cache内置。
设置完毕之后可以到[Gzip 检测页面](http://www.gidnetwork.com/tools/gzip-test.php)进行检测，看设置是否成功。

### 5\. 看看加速效果

打开主题底部模板footer.php，加入这几行：
<pre lang="php">Processed in &lt; ?php timer_stop(1); ?&gt; second(s), &lt; ?php echo get_num_queries(); ?&gt; queries.</pre>
<span style="color: #800000;">**便可以看到优化的结果了，_数据查询_和_处理时间_是不是都减少了不少呢？**</span>

**<span style="color: #800000;">做完了这些，你的WordPress是否有“_飞一样的感觉_”了呢？</span>**