---
title: Ubuntu 8.10 下 JAVA 中文显示(可用于CrossFTP中文显示问题)
tags:
  - crossftp
  - ftp
  - java
  - linux
  - ubuntu
id: 50
categories:
  - Systems&amp;Servers
date: 2008-11-14 07:29:20
---

1.
在:/usr/lib/jvm/java-6-sun/jre/lib/fonts下建立个目录 fallback
比如我这儿就是
mkdir /usr/lib/jvm/java-6-sun/jre/lib/fonts/fallback/

<!--more-->2.
在 fallback 里弄个中文字体
拷贝或链接都可以

比如我这就是
ln -s  /usr/share/fonts/truetype/wqy/wqy-zenhei.ttf  /usr/lib/jvm/java-6-sun/jre/lib/fonts/fallback/

3.
进入 /usr/lib/jvm/java-6-sun/jre/lib/fonts/fallback 执行 mkfontscale
再把 jre/lib/fonts/fonts.scale 的内容加到 jre/lib/fonts/fonts.dir

我这儿就是
cd /usr/lib/jvm/java-6-sun/jre/lib/fonts/fallback/
mkfontscale
cd ..
chmod +w fonts.dir
cat fallback/fonts.scale &gt;&gt; fonts.dir

<span style="color: #ff0000;">以上都要用root权限来做，即sudo。</span>

转自：linuxsir 作者：jhuangjiahua 略有修改。