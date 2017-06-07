---
title: 从Feedsky无缝迁移到Feedburner
tags:
  - feedburner
  - FeedSky
  - 订阅
id: 819
categories:
  - Blogging
date: 2009-08-29 19:39:10
---

### 0\. 准备知识

[为什么要用Feedsky或者Feedburner的Feed烧制服务？](http://kangzj.net/feedsky-feed-rss-subdomain/)

### 1\. Feedsky和Feedburner服务比较

Feedsky和Feeburner都是有名的Feed托管服务商，前者是国产，后者已经被Google收购。在2007年8月Feedburner被封之后，大量的用户转向 Feedsky。虽说现在Feedburner解封了，但是很多用户还是害怕哪天再历史重演，更加趋向于选择国内的Feed烧制服务也就是 Feedsky。

<!--more-->但是Feedsky的服务质量比Feedburner有点打折扣，经常抽风，更新慢（这个现在好像已经好多了），订阅数统计有问题。

广告方面Feedsky有“话题营销”、“展示广告”、“点击广告”（点击广告7.24暂停了）几种，比较方便投放，但是跟国内很多广告一样，价格较低。

不过也是有办法让Feedsky展示Google Adsense广告（[怎样做？](http://www.williamlong.info/archives/1490.html)——很简单，把Feedburner加上广告，然后让Feedsky以Feedburner为源更新）。有的同学说我想展示两种广告——好吧——把Feedksy再加上广告就可以了。反过来也是一样的。

Feedburner功能完善、稳定并且可以直接投放Google Adsense广告，Feed更新速度快；缺点是存在被墙的可能性。我最喜欢是他统计订阅数图片的动态效果:-D。

Feedsky和Feedburner各有利有弊，选择上完全看个人喜好。

### 2\. 我的意见：选哪个都好，关键不能被“套牢”

我觉得选择哪个服务不要紧，关键是不能被“套牢”——<span style="text-decoration: underline;">**不要用Feedsky或者Feedburner默认的订订阅地址**</span>。

比如说我，现在是把自己的二级域名feed.kangzj.net绑定的Feedsky，因为想展示Google Adsense方便，所以想转到Feedburner，但是不想损失订户（虽然Feedburner Mybrand支持子域名绑定，但是格式却是http://feed.kangzj.net/kangzj这样的形式的，很不爽——否则事情就更简单了），只要把feed.kangzj.net绑个主机，加个重定向到新的地址就行了！
> RewriteRule . http://feeds.feedburner.com/kangzjnet [L]
如果你想用Feedcat或者别的什么Feed烧制商的服务，改一下这个rewrite的规则就行了，完全不会因为换托管商损失订阅用户。万一哪天Feedburner再挂掉，再挂到Feedsky就可以了，非常灵活。

于是乎从Feedsky无缝迁移到Feedburner，从Feedburner无缝转到Feedsky……就是易如反掌的事情了。

PS：不利用二级域名，[用一个子目录通过rewriter来绑定烧制服务也是可以的](http://kangzj.net/move-from-my-own-feed-to-feedburner/)，这里就不详细介绍了。