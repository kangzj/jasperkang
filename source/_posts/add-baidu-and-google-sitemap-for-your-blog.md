---
title: 百度Sitemap和Google Sitemap
tags:
  - google
  - seo
  - sitemap
  - 百度
id: 1036
categories:
  - Blogging
date: 2009-10-04 22:41:56
---

<div>

### 1\. 什么是Sitemap[![inside_sitemap](http://kangzj.net/wp-content/uploads/images/200909/SitemapGoogleSitemap_7C7/inside_sitemap_thumb.jpg "inside_sitemap")](http://kangzj.net/wp-content/uploads/images/200909/SitemapGoogleSitemap_7C7/inside_sitemap.jpg)

首先科普下什么是Sitemap（按我自己的理解写的，如果不对，烦请纠正）：
> <span style="background-color: #ffffff;">Sitemap，顾名思义就是“网站地图”。它是一个xml文件，作用却不仅是地图那么简单，还提供了每个页面的较详细的信息：标题、生成时间、更新频率等。Sitemap中收录的URL是整个网站的精髓。</span><span style="background-color: #ffffff;">不同的搜索引擎能够识别的Sitemap格式一般不一致（SEOWhy上说格式一致-_-）。</span>
> 
> <span style="background-color: #ffffff;"><!--more--></span>

### 2\. Baidu(百度) Sitemap和Google Sitemap

很久之前就把博客做了Google 的Sitemap，用的插件是**Google XML Sitemaps**，它在网

<span id="more-1056"> </span>站根目录自动生成一个sitemap.xml文件，就是我们说的Sitemap：[http://kangzj.net/sitemap.xml](http://kangzj.net/sitemap.xml)。可以看到xml的基本单元是url，下面是单独一个单元的结构：
> &lt;loc&gt;http://kangzj.net/&lt;/loc&gt;
> 
> &lt;lastmod&gt;2009-10-01T14:54:05+00:00&lt;/lastmod&gt;
> 
> &lt;changefreq&gt;daily&lt;/changefreq&gt;
> 
> &lt;priority&gt;1.0&lt;/priority&gt;
包括地址、最近修改时间、更新频率和权重几个属性。

最近看到[jiucool](http://www.jiucool.com/)同学做了百度的sitemap，我也跟着做了一下。用的插件是：**Baidu Sitemap Generator**（作者：Lc.），这个插件自动在网站根目录生成一个sitemap_baidu.xml，这是我的百度Sitemap：[http://kangzj.net/sitemap_baidu.xml](http://kangzj.net/sitemap_baidu.xml)。其实百度并没有说明自己通用的Sitemap的格式，只是百度的《互联网论坛收录开放协议》中说到的论坛的Sitemap的格式，wordpress 其实也可以看成是一个论坛【1】，在这个思想的指导下Lc.制作了这个**Baidu Sitemap Generator**插件。可以看到百度Sitemap与Google的Sitemap不尽相同，它的每个单元是&lt;item&gt;
> &lt;link&gt;http://kangzj.net/wordpress-link-info-required-to-proceed-your-request/&lt;/link&gt;
> 
> &lt;title&gt;WordPress&amp;ldquo;执行请求操作，连接信息必需提供&amp;rdquo;解决方法&lt;/title&gt;
> 
> &lt;pubDate&gt;2009-10-01 22:18:42&lt;/pubDate&gt;
> 
> &lt;bbs:pick&gt;1&lt;/bbs:pick&gt;
每一个item包括地址、标题、发布时间等，可以有更加详细的数据，插件作者貌似只实现了这几个。

### 3\. 怎样让搜索引擎发现Sitemap

我们已经有了Sitemap，但是这个Sitemap是给搜索引擎看的，如果搜索引擎找不到它，那我们就白忙活了，怎样使搜索引擎发现你的Sitemap呢？

*   Google：

*   (1) 注册管理员工具，直接在后台提交Sitemap地址
*   (2) robots中指定：Sitemap: [http://kangzj.net/sitemap.xml](http://kangzj.net/sitemap.xml)
</div>
	<li>百度没有管理员工具，可以：

*   (1) 在robots中指定：Sitemap: [http://kangzj.net/sitemap_baidu.xml](http://kangzj.net/sitemap_baidu.xml)
*   (2) 在首页加上Sitemap文件的链接，等待蜘蛛爬
*   (3) <span style="color: #ff0000;">UPDATE: jiucool同学提示，可在这里提交百度Sitemap，但需要先人工审核(MS不太容易，没有试)：[http://news.baidu.com/newsop.html](http://news.baidu.com/newsop.html)</span>
</li>
个人觉得对于Google，直接提交最靠谱；对于百度，两项都要做一下比较保险。

我的robots文件是这样写的([http://kangzj.net/robots.txt](http://kangzj.net/robots.txt)):
> User-agent: *
> 
> Disallow:
> 
> Sitemap: [http://kangzj.net/sitemap.xml](http://kangzj.net/sitemap.xml)
> 
> Sitemap: [http://kangzj.net/sitemap_baidu.xml](http://kangzj.net/sitemap_baidu.xml)
最后：

推荐一个robots检测工具：[http://tool.motoricerca.info/robots-checker.phtml](http://tool.motoricerca.info/robots-checker.phtml "http://tool.motoricerca.info/robots-checker.phtml")

推荐一个robots生成工具：[http://www.mcanerin.com/EN/search-engine/robots-txt.asp](http://www.mcanerin.com/EN/search-engine/robots-txt.asp "http://www.mcanerin.com/EN/search-engine/robots-txt.asp")

推荐一个在线Sitemap生成器：[http://www.sitemapspal.com/](http://www.sitemapspal.com/ "http://www.sitemapspal.com/")

### 4\. 参考资料

1.  百度Sitema Generator Plugin：[http://www.liucheng.name/?p=884](http://www.liucheng.name/?p=884 "http://www.liucheng.name/?p=884")
2.  百度Sitemap的详细介绍：[http://www.okajax.com/a/200807/0H2O352008.html](http://www.okajax.com/a/200807/0H2O352008.html "http://www.okajax.com/a/200807/0H2O352008.html")
3.  Google Sitemap详解：[http://www.seotest.cn/blog/google-sitemap-xiangjie.html](http://www.seotest.cn/blog/google-sitemap-xiangjie.html "http://www.seotest.cn/blog/google-sitemap-xiangjie.html")
PS: Yahoo, Ask也支持标准的Sitemap协议的，可以在robots.txt中指定。