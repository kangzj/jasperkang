---
title: 利用apache进行ipv6/ipv4环境下代理的架设与使用(2)
id: 46
categories:
  - Systems&amp;Servers
date: 2008-10-22 06:06:36
tags:
---

    大家都知道，设置代理是件非常容易的事情，但是对于不直接支持ipv6的IE6浏览器来说就不是那么简单了。如果直接将ipv6的地址写入IE6的局域网设置里，IE6会直接把这个ipv6地址忽略掉(这个很让人无语)~~但是,如果这个代理有个域名的话，情况就不一样了：将域名写入代理设置，OK，可以使用了！

    所以，只要将我们的代理服务器申请一个域名即可，比如说德国那个ipv6代理(proxy.ipv6.uni-leipzig.de)。但是除了自己做DNS服务器，一般的域名服务商的DNS都不支持IPV6的域名解析，据我所知，，这个只有高校的才会做了，大家可以上学校去问问，呵呵（可行性不大，最好是学校的下一级比较好说话，比如自己院里头有台DNS的，就好办了，呵呵）。

    如果上面的条件不具备的话，那么只能舍弃IE6了，IE7-8和FireFox是完全支持ipv6的浏览器，下载或者升级，然后进行设置代理，就行了，能用了~~

    注：ipv6地址要用[]包起来(IE中可以不用)，端口填入服务器的端口