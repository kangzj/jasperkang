---
title: 用Windows Live Writer发布WordPress日志
tags:
  - Window Live Writer
  - wordpress
id: 786
categories:
  - Blogging
date: 2009-08-26 13:27:02
---

### １. WordPress在线编辑 Vs Windows Live Writer

![20080825-wlw](http://kangzj.net/wp-content/uploads/images/200908/LiveWriterWordPress_A1DA/20080825wlw_thumb.jpg "20080825-wlw")WordPress的在线编辑很好用，并且有自动保存的功能来防止文章意外丢失。但是也有缺点的：

1.  比如每次自动保存都会形成一个版本，占用大量的数据库空间；
2.  使日志的ID不连续；
3.  如果网速慢，载入速度和自动保存的速度将会很慢；
4.  方便多个WordPress(也包含其它博客)文章的发表；
5.  如果你有一个图床的话（或者附件床——[什么是图床？](http://kangzj.net/what-is-tu-chuang/)），需要手动上传附件并手动填写URL，很繁琐。
<!--more-->所以Windows Live Writer很有存在的必要，有了它，你就可以像用FrontPage或者DreamWeaver来编辑网站一样了——一个本地化的所见即所得的html编辑器，然而Windows Live Writer的功能不止这些，今天Kangzj就给大家介绍下如何使用Window Live Writer发布WordPress日志。

### 2\. 下载并安装Windows Live Writer

官方的下载地址：[http://download.live.com/writer](http://download.live.com/writer "http://download.live.com/writer")，选择相应的版本下载。

[![20080825-setup](http://kangzj.net/wp-content/uploads/images/200908/LiveWriterWordPress_A1DA/20080825setup_thumb.jpg "20080825-setup")](http://kangzj.net/wp-content/uploads/images/200908/LiveWriterWordPress_A1DA/20080825setup.jpg)下载下来的是Windows Live 的安装程序，包含很多其它的工具，酌情安装，但是一定别把Writer取消了，然后等待完成安装。

### 3\. 开始设置Windows Live Writer和WordPress

首先，设置WordPress打开XML-RPC协议。登入后台，打开设置-&gt;撰写，将该选项打上钩。

然后，打开Windows Live Writer，进行首次运行配置：

[![20080825-conf](http://kangzj.net/wp-content/uploads/images/200908/LiveWriterWordPress_A1DA/20080825conf_thumb.jpg "20080825-conf")](http://kangzj.net/wp-content/uploads/images/200908/LiveWriterWordPress_A1DA/20080825conf.jpg)[![20080825-conf-1](http://kangzj.net/wp-content/uploads/images/200908/LiveWriterWordPress_A1DA/20080825conf1_thumb.jpg "20080825-conf-1")](http://kangzj.net/wp-content/uploads/images/200908/LiveWriterWordPress_A1DA/20080825conf1.jpg) [![20080825-conf-2](http://kangzj.net/wp-content/uploads/images/200908/LiveWriterWordPress_A1DA/20080825conf2_thumb.jpg "20080825-conf-2")](http://kangzj.net/wp-content/uploads/images/200908/LiveWriterWordPress_A1DA/20080825conf2.jpg)[![20080825-conf-3](http://kangzj.net/wp-content/uploads/images/200908/LiveWriterWordPress_A1DA/20080825conf3_thumb.jpg "20080825-conf-3")](http://kangzj.net/wp-content/uploads/images/200908/LiveWriterWordPress_A1DA/20080825conf3.jpg)

行啦：

![](http://img.wlxrs.com/G3rWlfynFkYmWhvRLOJNPg/zh-chs/overview.jpg)

可以发布啦，是不是跟WordPress的后台有点像呢，具体使用就不说了吧。

### 4\. Windows Live Writer的一些小技巧

1.  可以自动上传本地图片到ftp服务器，减少了如果图片服务器和网页服务器不在一起时候引起的不便，在Writer的工具-&gt;帐户-&gt;编辑帐户-&gt;图片中可设置ftp帐户信息。 还可以给图片自动生成缩略图、加些特效呢，比如说阴影——本文的图片就有啊~~（[zhukun关于Live Writer上传图片的详细设置](http://www.zhukun.net/archives/2603)）
2.  在编辑过程中点击“预览”按钮可以很方便的预览文章。
3.  有好多的插件可以使用，[点击这里查看](http://gallery.live.com/default.aspx?pl=8)。可以添加自定义表情、短网址……
4.  如果你有多个博客，添加多个帐户就可以了！
还在等什么，开始用Window Live Writer方便地撰写你的日志吧！