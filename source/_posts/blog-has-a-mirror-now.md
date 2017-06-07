---
title: 小博增加了一个海外镜像
tags:
  - dns
  - dnspod
  - host1plus
  - mysql
  - 镜像
id: 85
categories:
  - Systems&amp;Servers
date: 2009-06-06 18:32:32
---

    完全是实验着玩的，其实没有必要这样做，记录下来吧。

    总共有三台服务器：
    Web服务器A，B；数据库服务器C。
    B是“12同学”提供的英国免费主机，A、C是有电信和教育网双线主机。A、B共用C的数据库（这里提示一下，如果用的mysql数据库，需要修改下设置skip-name-resovle，即关掉反向解析，否则查询会非常慢）。数据库还是放在国内，放在身边比较放心一点。<!--more-->

    DNS用的是Dnspod的智能解析，把kangzj.net.ru做了三个cname，这三个cname的值指向各个服务器：
    电信：ct.kang.pp.ru   =&gt;  B
    网通：cnc.kang.pp.ru    =&gt; B
    教育网：edu.kang.pp.ru    =&gt; A

    这样的话就把教育网的流量导向了服务器A，把网通、电信及其它所有的流量导向了海外的镜像。由于dnspod提供的智能dns不能识别海外的访问，把除了这三种外的所有流量全部识别为电信线路，所以，要想海外用户能访问海外的镜像B的话，电信线路一定要解析到B。

    然后把两个主机放上不同的统计代码，就可以看到效果了。

    最后谢谢12提供空间~~

EOF