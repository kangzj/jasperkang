---
title: 我到底需要多少流量的主机？
tags:
  - 主机
  - 流量
  - 空间
id: 979
categories:
  - Blogging
date: 2009-09-19 12:49:35
---

无论是_hugege_还是_小张_还是_wopus_，还是国内主机，还是国外主机，都有一个重要参数，那就是流量。最小的有2G的，大到几十到几百G不等。那么独立博客应该怎样确定自己到底需要多少流量呢——既不能浪费钱，也不能让流量不够使——这就是Kangzj写这篇文章的目的。

### 1\. 评估自己网页的大小

推荐一个工具yslow（Why Slow?），Firefox下可以通过搜索插件来安装：

[![yslow](http://kangzj.net/wp-content/uploads/images/200909/ec0ecfa0dba8_8BAD/yslow_thumb.jpg "yslow")](http://kangzj.net/wp-content/uploads/images/200909/ec0ecfa0dba8_8BAD/yslow.jpg)

<!--more-->在右下角就会出现：[![right-yslow](http://kangzj.net/wp-content/uploads/images/200909/ec0ecfa0dba8_8BAD/rightyslow_thumb.jpg "right-yslow")](http://kangzj.net/wp-content/uploads/images/200909/ec0ecfa0dba8_8BAD/rightyslow.jpg) 。点击图标即可调出主界面，详细的使用很简单，不详细说了。

评估结果是有一项是Components是我们需要的：

[![components](http://kangzj.net/wp-content/uploads/images/200909/ec0ecfa0dba8_8BAD/components_thumb.jpg "components")](http://kangzj.net/wp-content/uploads/images/200909/ec0ecfa0dba8_8BAD/components.jpg) 这个是我的首页的结果，总大小：382.8K。但这并不是这个网页耗费我主机的流量，因为我有不少东西都是外链：

1.  doc: 就是网页文本的大小，这个是肯定要加载的，53K；
2.  js：网页加载的js，其中有170多K是统计和Google广告还有调用的Google的JQuery，也就是说，这一项只耗费30K左右的流量；
3.  css：这项基本都是调用的自己网站，这40K有效；
4.  iframe：直接忽略；
5.  cssimage：主题里的图片，67.7K；
6.  image：这个我都是外链，忽略；如果你不想把图片外链，那么把这项也考虑进去。
好了，这么一看，整个网页：53+30+40+67=180K。现在好了，我们有一个基准了（为什么用首页当做基准？——第一，通常首页的浏览量最大且最具代表性；第二，通常首页加载了所有的js, css）。虽然有些css和js会缓存，但是，因为有流量从搜索引擎过来，基本是没有缓存的，我们应该按照比较坏的情况来估计。

PS：Yslow这个工具主要是用来看网站加载速度的，你可以试试哦。

### 2\. 估计需要多少流量

上而已经估计了每个网页有多大，而主机商会提供给我们流量的多少，我们就来算一下：

如果是2G的流量：

2G/180k=380，也就是大约每天350的点击量（因为会的搜索引擎的光顾，要给搜索引擎留点），如果新站就已经很多文章，可能还要更多的考虑搜索引擎。有一次我的机器一天之间被baidu spider爬了500M的流量，百度spider真的很笨。

综合你现在的访问量，你很容易就可以算出你每月需要多少流量了。当然老站的话，每个月统计下自己的流量到底是多少，是更加保险的做法^^

### 3\. Kangzj的建议

1.  建议初期买少些流量，不要觉得什么都Unlimited就是好的，很浪费钱；
2.  最好主机商承诺可以随时退款或者更换主机类型的（比如可以换成更多流量的主机等）；
3.  多多利用[图床](http://kangzj.net/what-is-tu-chuang/)来放图片和附件，好处是1.可以节省流量 2.网站更换空间打包及传输更加容易 3\. 相当于是CDN加速；
算好大约需要多少流量，够用就好，不要花些没有必要的钱。当然如果你很有钱的话，就忽略我这篇文章吧:-)