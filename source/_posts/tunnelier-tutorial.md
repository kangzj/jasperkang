---
title: Tunnelier使用教程
tags:
  - Bitvise
  - putty
  - tunnel
  - Tunnelier
  - Xshell
  - 凸墙
id: 1694
categories:
  - Systems&amp;Servers
date: 2010-03-19 15:42:44
---

Tunnelier是Bitvise团队开发的一个ssh客户端，功能包括ssh客户端、sftp客户端、端口转发功能（tunnel）。其中他的tunnel功能做的十分高效，比基于plink的MyEntunnel速度快很多，使ssh凸墙不再慢。并且<span style="color: #339966;">**个人使用免费**</span>，最近不少人都在推荐。下面讲讲怎么配置tunnelier来建立tunnel，高手直接飘过就好了。

### Tunnelier下载地址

安装版：[http://dl.bitvise.com/Tunnelier-Inst.exe](http://dl.bitvise.com/Tunnelier-Inst.exe "http://dl.bitvise.com/Tunnelier-Inst.exe")

绿色版：[http://tp.vbap.com.au/download](http://tp.vbap.com.au/download "http://tp.vbap.com.au/download")

### 使用方法

<!--more-->

[![tunnelier1](http://blog.kangzj.net/wp-content/uploads/2010/03/tunnelier1_thumb.jpg "tunnelier1")](http://blog.kangzj.net/wp-content/uploads/2010/03/tunnelier1.jpg) [![tunnelier2](http://blog.kangzj.net/wp-content/uploads/2010/03/tunnelier2_thumb.jpg "tunnelier2")](http://blog.kangzj.net/wp-content/uploads/2010/03/tunnelier2.jpg)

点击login即可建立tunnel，会跳出来一个终端和图形化的sftp界面（如果服务器关闭了sftp或shell则不会出现）。

如果想下次自动登录，点击[![image](http://blog.kangzj.net/wp-content/uploads/2010/03/image_thumb.png "image")](http://blog.kangzj.net/wp-content/uploads/2010/03/image.png) 保存起来即可。下次登录的时候，[![image](http://blog.kangzj.net/wp-content/uploads/2010/03/image_thumb1.png "image")](http://blog.kangzj.net/wp-content/uploads/2010/03/image1.png) 再login即可，十分方便。

而且这玩意儿牛逼的地方在于，不需要重新登录或验证，只要右下角图标没有关，维持 这**一个**ssh连接，就可以随时新建一个terminal或sftp窗口，而**不需要**重 新登录。这样连`screen`命令也省了。要多少个窗口开多少个就OK了。由于使用的是cmd作为终端，所以中文字符编码也不成问题了～～～～   ([via](http://blog.est.im/archives/1714))

Tunnelier还有个好用的功能就是设置Proxy（Socket4, Socket5, HTTP），这是plink不具备的，十分好用。

可以和Putty, Xshell, 收费的SSH _Secure Shell_ Client说886~~