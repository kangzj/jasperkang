---
title: 对朋友隐藏广告-Ozh' Who Sees Ads
tags:
  - google
  - google adsense
  - Ozh' Who Sees Ads
  - php
  - wordpress
  - 插件
id: 1117
categories:
  - Blogging
date: 2009-10-13 10:18:12
---

为什么要对朋友隐藏广告呢：

**第一，减少展示次数，提高广告单价**。常来的访客一般来说是不会点击广告的，他们对广告已经熟视无睹，过多的展示会降低每次点击的单价，对朋友隐藏广告有现实的必要性。
**第二，界面对常来的朋友更加友好。**方便博友交流，去除广告的干扰，界面更清爽。

下面主角登场了，这款插件叫做：**Ozh' Who Sees Ads**。

怎样安装就不介绍了，下面介绍下它的使用。

<!--more-->

[![who-see-ads](http://kangzj.net/wp-content/uploads/images/200909/2a70a33b4e30_142A1/whoseeads_thumb.jpg "who-see-ads")](http://kangzj.net/wp-content/uploads/images/200909/2a70a33b4e30_142A1/whoseeads.jpg) 可以设置多种规则来控制广告的显示包括：

1.  对搜索引擎来的访客是否显示广告
2.  经常来的用户是否显示广告
3.  发布超过多长时间的文章显示广告
4.  是否对已登录用户显示广告
5.  ……
各个规则可以调整顺序，“Who Sees Ads”从第一条规则开始匹配，找到匹配就执行相应策略。下面是我的显示广告的规则：

[![my-who-sees-ads-rules](http://kangzj.net/wp-content/uploads/images/200909/2a70a33b4e30_142A1/mywhoseesadsrules_thumb.jpg "my-who-sees-ads-rules")](http://kangzj.net/wp-content/uploads/images/200909/2a70a33b4e30_142A1/mywhoseesadsrules.jpg) 效果是：
> **如果是从搜索引擎来的一定显示，如果是“常来用户”那么不显示，其它情况全部显示。**
规则设置完毕之后，可以用下面的代码调用（postAd是广告的名称）：

在模板调用：<tt>&lt;?php wp_ozh_wsa("postAd");?&gt;</tt>

<tt>在编辑器调用：</tt><tt>&lt;!--wsa:postAd--&gt;</tt>

设置界面下方还有其它设置，比如定义“常来朋友”和“点击保护”；

*   “常来朋友”：定义在m天之内有m个PV以上的为“常来朋友”；
*   “点击保护”：为登录用户保护广告不被误点击以防止违反Google的协议。
_我这几个名词翻译的真烂。_

<span style="color: #800000;"> PS：</span>如果安装了页面静态化的插件，这个插件会失去作用。折中的考虑可以把DB Cache+Widget Cache配合使用，既可以加速，这个插件也不会失效，我的博客现在就是这样的。