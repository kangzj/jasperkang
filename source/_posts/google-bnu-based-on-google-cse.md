---
title: 基于Google自定义搜索的“Google师大”
tags:
  - google
  - google师大
  - wordpress
  - 自定义搜索
id: 971
categories:
  - Web-Development
date: 2009-09-17 16:05:28
---

![google-bnu](http://kangzj.net/wp-content/uploads/images/200909/Google_9C47/googlebnu_thumb.jpg "google-bnu")

演示：[http://g.xinqing100.net](http://g.xinqing100.net) （教育网） [http://kangzj.net](http://kangzj.net)  （右上角的搜索框）

“我爱水煮鱼”介绍过怎样把“[Google自定义搜索整合到WordPress](http://fairyfish.net/2008/04/29/integrate-google-custom-search-into-wordpress/)”，我已经做了，大家可以搜索下试试，就在**右上角的搜索框里搜索**。确实比原先的站内搜索要好用（原来的搜索只是搜索日志，而不包括留言及其它页面），并且不占用服务器资源，建议大家都整下，呵呵。这里我再给大家介绍下我用Google自定义搜索做的“Google师大”，专门搜索北师大的网站，大家有兴趣的话，看完之后也可以给自己的学校或者单位做个这样的搜索啊：

[](http://kangzj.net/wp-content/uploads/images/200909/Google_9C47/googlebnu.jpg)

<!--more-->1\. 创建两个页面，分别来做搜索页面和搜索结果页面。

2\. 登录到 [Google 自定义搜索](http://www.google.com/coop/cse/)，创建你的自定义搜索。在**选择一些网站**的时候加入你们学校的所有的网站，比如我们学校，我就先加了这么几条：
> <span style="background-color: #ffffff">*.bnu.edu.cn/*</span>
> 
> <span style="background-color: #ffffff">*.xinqing100.net/*</span>
> 
> <span style="background-color: #ffffff">*.bnulife.com/*</span>
所有的bnu.edu.cn和其它几个域的子域下所有的页面都有搜索的范围之中，很容易设置吧，可以把跟学校相关的论坛啊，网站啊都加上去。

3\. 在输入你的基本信息和网站之后（如果你想通过搜索赚钱，还可以和adsense账户绑定；我没有绑定，选择的是不显示广告，公益性质的）。

4\. 搜索结果托管选项选项：

[![google-cse](http://kangzj.net/wp-content/uploads/images/200909/Google_9C47/googlecse_thumb.jpg "google-cse")](http://kangzj.net/wp-content/uploads/images/200909/Google_9C47/googlecse.jpg) 我选择的是第二项，你也可以根据实际情况来选择。

5\. 指定搜索结果详情：输入你第一步创建页面的页面的地址。如我的：[http://g.xinqing100.net/search/](http://g.xinqing100.net/search/) - 其实就是建立了一个/search/目录，在下面放了个index.htm文件而已。

然后就可以用了！

6\. 美化一下你的搜索界面吧，现在你有了一个专属你们学校的搜索引擎了。

Google就是这么强大，就是这么友好，呵呵~~试试吧

<span style="color: #800000">PS：搜索结果代码必须放在&lt;body&gt;&lt;/body&gt;里面，否则结果无法显示。</span>