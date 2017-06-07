---
title: 2Mbps的ADSL跑出7MB/s的下载速度？！
tags:
  - gzip
  - 主机
  - 离谱
id: 1454
categories:
  - Systems&amp;Servers
date: 2009-12-04 02:43:54
---

[![222](http://blog.kangzj.net/wp-content/uploads/2009/12/222_thumb.jpg "222")](http://blog.kangzj.net/wp-content/uploads/2009/12/222.jpg)国内主机服务形势日趋严峻，众多网站移居国外。美国主机价廉物美受到广大站长的追捧，但是也有一些无良的主机商很离谱，比如下面要说的这位。在说之前，请你先测试下这们主机商的下载速度：

[http://www.kualo.com/img/100meg.file](http://www.kualo.com/img/100meg.file)

速度怎么样？如果你是2M的ADSL上网，下载速度可能会超过**7M/s**（极限速度是256KB/s）。而像我这样用100M端口的呢，看右图：**30.7M/s**(极限速度12.5M/s)，都超过了的极限速度。

<!--more-->

这是为什么呢？

看他的curl：
> xq@xinqing100:~$ curl --head [http://www.kualo.com/img/10meg.file](http://www.kualo.com/img/10meg.file)
> HTTP/1.1 200 OK
> Date: Thu, 03 Dec 2009 18:15:16 GMT
> Server: Apache
> Last-Modified: Tue, 01 Sep 2009 13:40:15 GMT
> ETag: "2c738c9-a00000-472844a524dc0"
> Accept-Ranges: bytes
> Content-Length: 10485760
> Vary: Accept-Encoding,User-Agent
> <span style="color: #ff0000;">Content-Type: text/plain</span>
[![444](http://blog.kangzj.net/wp-content/uploads/2009/12/444_thumb.jpg "444")](http://blog.kangzj.net/wp-content/uploads/2009/12/444.jpg)**注意Content-Type是text/plain**，也就是说只要对text/plain类型开启gzip的话，那么这个100M的文件就会被压缩！

好，我们来看看text/plain格式是否开启了gzip压缩（右图），果然开启了……

很清楚了，该主机商把这个100M的文件用了gzip压缩，实际传输的流量只有几百K，甚至几十K，把这几十K传输到本地之后，浏览器会自动把它解压，然后就生成了这个100M的文件！

就算你是56K的拨号上网，估计也会有个几M的速度。这个主机商太牛了、太离谱了~把大家白痴化了...不过我们并不比他傻，吼吼~~

下载速度超过了极限，让人一眼就看出，不管是什么问题，但是一定有问题。大家想啊，要是调节这100M文件的复杂程度，适度地“增加”下下载速度的话是根本无法觉察的！你还以为速度挺快呢！

大家选主机的时候一定擦亮眼，买之前多打听一下，找找小白鼠先，尽量自己不要当小白鼠^ ^

不过话说回来，这家主机还是不错的，在linux下用wget下载，速度可以到700K/s，平均400+K/s。但是搞出来这样的东东，谁还敢买？

从这个事情中也能看出gzip的能力，压缩传输的内容，其实也是变相地给你增加了带宽，不是吗？