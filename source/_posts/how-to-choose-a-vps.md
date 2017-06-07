---
title: 如何选择国外VPS
tags:
  - OpenVZ
  - vps
  - VPS内存
  - VPS性能
  - Xen
  - 美国VPS
  - 虚拟技术
  - 选择VPS
  - 酷胖
id: 1528
categories:
  - Systems&amp;Servers
date: 2010-01-12 00:22:17
---

国内网络环境日益恶劣，众多站长将站“移民”海外。选择一款优质高速的主机十分重要。由于虚拟主机的主机资源、支持环境等种种的限制，很多站长选择VPS（Visual Private Server），这篇文章，我们就来一起说说如何选择国外VPS。

*   本文只讨论Linux VPS，Windows的不在讨论范围内；
*   本文下载速度与ping延迟都是用北京电信网络测试的。

### 1\. 选择哪国的VPS？

除去像[showfom](http://zou.lu)小朋友这样追求FlagFox那个小旗子癖之外呢，大部分同学追求的不过是有两点，一点是速度，另一点便是稳定。周边向个国家和地区的速度都不错，但是由于价格过高以及语言上沟壑，买的人并不多。其中日本和香港服务器是购买的比最多的，其它都比较少了。

我国周边速度一般来说是：香港&gt;台湾&gt;日本&gt;韩国&gt;新加坡&gt;马来西亚，不是绝对的，距离有远近，速度有不同。除去我国周边的国家，速度还不错的，首选的就是美国了。08年投入使用的TPE光缆，带宽达5T多，使美国的主机不再慢。再除去美国，加拿大的西部的主机也是可以考虑的。

<!--more-->

速度说完了，该说下价格，我国及我国周边的VPS都是差不多，就一个字——“贵”。美国的是全球互联网的中心，主机业务十分发达，机房超多，VPS商更是多如牛毛，价格自然是很便宜了。最便宜的每月$5左右就可以拿下，这也是众多站长“移民”美国的重要原因。

### 2\. 怎样选择VPS商？

#### 2.1 看口碑

选主机商，首先看口碑(down机频率、ticket处理是否及时、是否丢失过客户数据等等)，这个我不多说，人肉下主机商即可，有个地方可以去看看，那就是WHT([WebHostingTalk](http://www.webhostingtalk.com))，一个超级热闹的地方，Kangzj就不多说了。

#### 2.2 一ping，二whois，三测试下载

很多VPS商会提供测试IP，首先ping下，看延迟怎么样。一般说来，美国主机ping都在160ms以上，最最极品160ms多一点的算是极品了。下表简单地说了下，并不精确：
<table style="height: 82px;" border="0" cellspacing="0" cellpadding="2" width="305">
<tbody>
<tr>
<td width="97" valign="top">延迟(ms)</td>
<td width="206" valign="top">位置(美国)</td>
</tr>
<tr>
<td width="97" valign="top">160-220</td>
<td width="206" valign="top">西岸（以LA为代表）</td>
</tr>
<tr>
<td width="97" valign="top">220-240</td>
<td width="206" valign="top">中部（以Dallas为代表）</td>
</tr>
<tr>
<td width="97" valign="top">250以上</td>
<td width="206" valign="top">东岸（以WDC为代表）</td>
</tr>
</tbody>
</table>
ping并不能代表什么，只能说明服务器反应速度，几十毫秒人类根本觉察不到。ping并不是选择服务器的第一标准。香港的ping可以说是所有国外主机当中最好的，可以在10ms以内（广东），但是香港的国际出口小得可怜，有的时候ping再好，带宽太小，也不能买。

通过IP Whois可以查到IP是哪个机房的，那个机房的速度、稳定性等的评价，在网上评论肯定比那个VPS商要多。通过这种方法还可以找到测试下载，即使VPS商没有提供测试下载，也能体验下载的速度怎么样。对国内友好的机房汇总：[http://www.whcoupon.com/48.html](http://www.whcoupon.com/48.html) 。

### 3\. 选何种虚拟技术的VPS？

虚拟技术用得最多的是Xen和OpenVZ。据Rashost讲“基于XEN的Linux VPS(Para-virtualized VPS, 半虚拟化VPS)的性能要优于其他虚拟化技术”，而在一些论坛上也听到过OpenVZ比Xen性能好的讲法，一时分不清谁对谁错。

然而，就我使用经验来看，Xen性能一般来说要比OpenVZ的好。至于最主要的原因，我想，并不是因为Xen本身的性能有多好，而是Xen不容易超卖（基于Xen的VPS会像真机器一样用内存Cache磁盘，而OpenVZ的VPS不会）。

还有一点要注意的是，Xen的VPS一般来说可以直接开pptpd和OpenVPN的VPN，而OpenVZ的VPS只能开OpenVZ的VPN（如果默认没开，需联系客服开通tap/tun和IPtable）。

Virtuozzo、VMWare是两种收费的虚拟技术，性能上不好评价，价格上多是比前两种贵。还有一种新兴的虚拟技术叫做KVM，据说VPS之间隔离做得特别好，性能也很不错，不过尚不很成熟。

### 4\. 什么VPS控制面板好用？

这里说的控制面板可不是主机的控制面板，而是控制VPS的面板，用来重装、重启和进行一些高级设置的面板。在Kangzj看来，面板有就行，VePortal、SolusVM、Parallel等等或者VPS商自己开发的，功能也就那么几种而已，不会太出奇（Linode的控制面板除外，做得太好了，功能超级超级强大）。但是话说回来，这面板没有的话，还真是不行，连死机重启都要发ticket，太不方便。

### 5\. 多少内存够用？

这个很不好说，就以一个PHP网站为例。可以按PV来估算需要内存的大小。一般说来，每天几百IP的网站，128M内存就可以勉强应付。优化设置可以参考张宴：[http://blog.s135.com/post/375/](http://blog.s135.com/post/375/ "http://blog.s135.com/post/375/") 。

### 6\. 多少带宽够用？

说实话，只要内存够用，配置的流量一般够用。不要去贪什么不限流量，那都是幻影。万一遇上一个流量大户（很有可能，因为不限流量最吸引大户的眼光），总是占据带宽，就等着郁闷死吧。一句话，流量不在多，够用就行。至于怎么计算自己的网站大约能消耗多少流量，可以参考这篇文章：[http://kangzj.net/how-many-gigabits-do-i-need/](http://kangzj.net/how-many-gigabits-do-i-need/ "http://kangzj.net/how-many-gigabits-do-i-need/")。

### 7\. 月付还是年付？

虽然一般来说年付会有优惠，但是仍十分建议月付。为什么，原因有三：

*   凡是国外主机，IP总有被封的危险。如果被封，加IP又是一笔费用，如果不能加IP，那这VPS基本上就废了（我用过一家的VPS，就是不允许加或者换IP）。
*   现在速度快，一年之中不一定都快。Linode Fremont机房就是活生生的例子，当然Linode可以免费换机房倒还好说。
*   VPS商携款潜逃也说不定。这样的事情也不是没有先例，虽然是极其少数，但不是没有的，万一人品就到那个份上了……
总之，一句话，这一年之中可能发生很多你想不到的事，你有可能损失掉这笔钱。一个月一个月的用，感觉不满意了马上换，多舒坦。

### 8\. VPS的CPU限制方式？

虽然最后一个提，但这并不说明这一项不重要，CPU是最容易忽视，但是十分重要的方面。

据我观察，大约有两种CPU的共享方式，一种是Equal Share，按字面意思，就是大家平分使用（当然也存在可能遇到大户的危险）；另一种，限制核数和频率。

限制频率有两种方式，一种是限制单核，给一个频率（比如500MHz）；另一种是给多个核，每个核给一个频率，然后相加（比如，给5个核，每个给100MHz），表面上说起来是一样的。

孰好孰赖，不是很好比较，大家各自想清楚就O了。

_暂时就这么多，谁想到还有什么问题，请留言。_

最最后再人肉广告下：我的新站改名了，由“WebHosting Coupon”改为“**<span style="text-decoration: underline;">酷胖</span>优惠码**”了。欢迎大家常去踩踩，一个**不加推介码**的专门介绍主机、域名优惠的小站：[http://www.whcoupon.com](http://www.whcoupon.com) 。

全文完，欢迎批评指正。