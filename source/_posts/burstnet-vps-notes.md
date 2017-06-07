---
title: BurstNET VPS试用手记
tags:
  - burst.net
  - BurstNET
  - ddos
  - OpenVPN
  - OpenVZ
  - ping
  - vps
  - 合租
  - 测评
  - 独立IP
  - 试用
id: 1354
categories:
  - Systems&amp;Servers
date: 2009-11-12 12:11:09
---

<span style="color: #ff0000;">UPDATE: </span>**有同学反应，部分地区ping有丢包现象，请大家参考。**

BurstNET机房位于宾夕法尼亚东北部，从1991建立，开始时以计算机软硬件服务为主，后来开始做IDC服务，有很多的Reseller。他有自己的机房，面积超过11000平方公尺。做为一个老牌的IDC，在这不太景气的年头里也出来和一些Reseller抢饭碗，推出了几款非常超值的VPS：

最低配置的一款只需要$5.95/mon，而配置为：[基于OpenVZ、1G CPU、512M内存、1000G的带宽、2个IP地址](https://service.burst.net/aff.php?aff=268 )，性价比相当之高，本人就购买了一款，试用了下，给大家参考：

**（1）Ping延迟300ms以下**

从北京电信Ping该服务器，延迟在260ms左右，没有丢包；广东Ping延迟在240ms左右，没有丢包。Ping延迟比加州这边多不到100ms。但是Ping延迟说明不了多少问题，只是个延迟而已，只要不丢包就没什么问题。

[![image](http://kangzj.net/wp-content/uploads/images/200911/BurstNET5.95VPS_9617/image_thumb.png "image")](http://kangzj.net/wp-content/uploads/images/200911/BurstNET5.95VPS_9617/image.png)

**（2）上传速度很快**

<!--more-->最快可以跑到2MB/s，最慢也是稳定在200KB/s，下面是用FTP上传文件的截图（我还是通过代理上的）：

[![image](http://kangzj.net/wp-content/uploads/images/200911/BurstNET5.95VPS_9617/image_thumb_3.png "image")](http://kangzj.net/wp-content/uploads/images/200911/BurstNET5.95VPS_9617/image_3.png)** （3）下载速度也不错**

好像是被单线程限速了，每个线程下载最快也只能到50K/s左右，平均在30K/s左右。但是如果用迅雷等多线程下载工具下载时，速度可以达到300K以上，有图（平均速度187K/s）：

[![image](http://kangzj.net/wp-content/uploads/images/200911/BurstNET5.95VPS_9617/image_thumb_4.png "image")](http://kangzj.net/wp-content/uploads/images/200911/BurstNET5.95VPS_9617/image_4.png)** （4）有vePortal面板**

可以方便的重启、重装系统，备份、恢复系统，而不用联系客服，相当方便。有多种的系统可供选择，CentOS，Ubuntu，Debian等等32或64位的系统。

[![image](http://kangzj.net/wp-content/uploads/images/200911/BurstNET5.95VPS_9617/image_thumb_5.png "image")](http://kangzj.net/wp-content/uploads/images/200911/BurstNET5.95VPS_9617/image_5.png)**（5）有硬件DDOS防护**

CISCO™ GUARD，这是绝大多数便宜的VPS都无法提供的功能，虽然性能不太清楚，但是CISCO应该还是不错的。

**（6）老牌公司，值得相信**

在WHT上逛的时候，碰上有人怀疑这么便宜的VPS会不会超售，有人回答就说：“BurstNET有成千上万的服务器，我还是相信BurstNET能够做到这个价位的。”BurstNET自己官方的人更是出来调侃：“We are good people here!”（我们这里都是好人）。我还是比较相信BurstNET的，至少用的这几个周感觉都不错。

Tickets系统比较完善，工作日一般三个小时内会有答复（上班时间内）。

**（7）2个IP**

5-6美元的VPS几乎没有配备两个IP的，这相当难得。如果两个人合租，正好一人一个，挺爽。一般的Shared Hosting，配备独立IP，每个每月至少都要$1。

**（8）支持OpenVPN**

只要联系客服帮你开启TUN/TAP即可，安装方式与正常的机器一样。我安装成功了，但还没有调试成功，谁会配置，帮帮我的忙，呵呵。

**（9）年付优惠两个月**

月付是$5.95，年付只要$59.5，免两个月，还是相当合算的。算下来只一年只要420RMB左右。

**（10）购买地址**

能看到这里，说明你对这个VPS还真是有兴趣。希望想买的同学可以用下我的推广链接，你不损失什么，而我可以挣点钱：[https://service.burst.net/aff.php?aff=268](https://service.burst.net/aff.php?aff=268 "https://service.burst.net/aff.php?aff=268") 。如果在购买中遇到什么问题，可以问我，也可以找我帮你代购，代购汇率转换与[久酷同学](http://www.jiucool.com/us-dollar-payment-for-free/)相同。

喜欢折腾Linux的同学可以买个玩，没有Linux常识的同学还是不要买了，美国黑客相当的多，搞不好就被黑掉了。黑掉还好说，重装下就行，糟糕的是这些个黑客会在你的VPS装些钓鱼网站啊啥的，有可能使你违反TOC而被服务商停止服务，还不退款。

**最后广告下：**

欢迎来参加我的**独立IP**主机合租，100/年：[http://kangzj.net/dedicate-ip-visual-host/](http://kangzj.net/dedicate-ip-visual-host/)，目前只差三人了！！要的赶快来吧！！

来得越早，用的时间越长，总共买了13个月的服务^^