---
title: 不太好说出口的增加高质量外链的方法
tags:
  - pr
  - seo
  - 外链
  - 搜索引擎优化
id: 685
categories:
  - Blogging
date: 2009-08-12 08:00:08
---

经过“[我是该高兴还是该愤怒](http://kangzj.net/should-i-feel-happy-or-angry/ "Permanent Link to 我是该高兴还是该愤怒")”这件事之后，Kangzj严重地认识到了搜索引擎优化中PR的威力，也强烈地感觉到让自己博客的PR升上去的必要性。Kangzj除了自己摆弄个小博客之外，还是几个网站的“技术支持”，纯管技术，不干涉任何内容的事情。偷偷地说句，这几个网站的PR都在5以上，并且几乎没有外链。这不能不让Kangzj很动心哪:-)可是作为“技术支持”是没有权利给网站加链接的，于是Kangzj便想出了下面的坏点子：
<!--more-->
找个不显眼的版权声名之类的，找几个不显眼的字母加上Kangzj博客的链接。加上链接了，要是被发现了就不好了，于是就想办法，能不能让一不小心点到链接的人没有觉察呢，有啦！
到我的博客，打开index.php，加了这几行代码：
> &lt; ?php
> $referer = strtolower($_SERVER['HTTP_REFERER']);
> if(strpos($referer, 'xinqing100')!==FALSE  &amp;&amp; !preg_match("/(bot|crawl|spider|slurp|sohu-search|lycos|robozilla|ia_archiver|scooter)/i", strtolower($_SERVER['HTTP_USER_AGENT']))) {
>    echo '';
>    exit;
> }
> ?&gt;
判断一下来源，如果来自那个网站，并且不是BOT（我是安全起见，我猜BOT应该是不会提供referer的），则转到另一个网站。大家看不懂就算了，不是什么拿得出手的方法，哈哈~~
还有一种偷偷加链接的更绝的办法，不加评论，只写代码：
> &lt;script type="text/javascript"&gt;// &lt;![CDATA[
> // &lt; ![CDATA[
> document.write("
> &lt;div style="display:none;" mce_style="display:none;"&gt;");
> // ]]&gt;&lt;/script&gt;
> &lt;a href="http://www.ccc.com/qudou/"&gt;祛痘&lt;/a&gt;
> &lt;a href="http://www.bbb.net"&gt;QQ空间模块&lt;/a&gt;
> &lt;a href="http://www.aaa.com"&gt;信用卡&lt;/a&gt;
> &lt;script type="text/javascript"&gt;// &lt;![CDATA[
> // &lt; ![CDATA[
> document.write("&lt;/div&gt;
> ");
> // ]]&gt;&lt;/script&gt;
上面的不是我想出来的，是在 http://sird.bfsu.edu.cn/ 看到的，呵呵，这个网页里还隐藏着一个加隐藏链接的方法，大家找一找:-)(这个网站是应该是被黑客加的代码吧)
**PS：我的代码里有我加链接的网站的蛛丝马迹，谁要是能发现那个网站，并且找到我加的链接在哪里，再试试效果，我奖他一个正版Vista的序列号！**
**再PS：此非正路，我也就是做个实验而已，大家看看就罢了尽量不要去用。第一种方法还好，后面的方法很容易被搜索引擎惩罚。**
PS:WAP版本可以评论