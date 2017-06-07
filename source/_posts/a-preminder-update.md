---
title: Preminder(PR更新提醒服务)小升级
tags:
  - pagerank
  - pr
  - preminder
  - PR更新
  - 升级
id: 1051
categories:
  - Blogging
date: 2009-10-07 21:17:07
---

> **<span style="color: #993300;">注意：PR尚未更新，本文是介绍我的“Preminder--PR更新提醒服务<strong><span style="color: #993300;">”</span>**程序升级而已。 </span></strong>
由于我的服务器放在学校机房，网络经常会短时的抽风(学校网络中心技术不太行)，[Preminder](http://apps.kangzj.net/preminder/)发出了几次PR更新误报（连接不到Google，于是得到的PR为0，于是发邮件通知PR变为0；等到网络恢复之后，[Preminder](http://apps.kangzj.net/preminder/)得到正确的PR便又会发出一封通知邮件）。在这里给收到误报邮件的同学道个歉，对不起啦。

光说对不起没用，要解决才行，Kangzj想了想，把程序完善了下，加了一段验证网络是否通畅的程序。如果网络通畅就检测PR，否则就等几分钟再进行下一次检测…总共进行6次。
代码如下：
<!--more-->
<pre lang="php">//以www.google.com为标准，如果它的PR为0，说明网络有问题
//等待200秒，再次检测；总共检测6次
for($j=0;$&lt;6;$j++){
        $ggpr=intval(pagerank('www.google.com'));
        if($ggpr==0){
                sleep(200);
        }else{
                break;
        }
}
//如果经过6次检测之后，网络还没有通畅，那么终止程序
//等到下次cron执行再说
if($j==6)exit;</pre>
这样的话，就不会因为网络问题而乱发邮件啦~~吼吼~~ 还没有用上的同学赶快来注册下吧：
[http://apps.kangzj.net/preminder/](http://apps.kangzj.net/preminder/)