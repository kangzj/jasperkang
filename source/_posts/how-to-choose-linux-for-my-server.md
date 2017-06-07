---
title: 我的服务器应该装什么版本的Linux?
tags:
  - linux
  - 服务器
id: 770
categories:
  - Systems&amp;Servers
date: 2009-08-24 20:09:26
---

Linux作为一个网络操作系统，其网络的性能是不用多说的，用它来做服务器也是再合适不过的，甚至有的人说Linux就是做服务器用的（虽然有点过分，但是不却突出了Linux的长处）。虽然现在Linux桌面应用已经十分成熟，但是相对于文本界面，图形界面始终都是更加浪费资源和不稳定的。

Linux有很多很多的发行版本，有名的也有十几种，到底选用哪个系统来做服务器应用呢？这里将我的一些体会和理解写出来，水平有限，讲的不对的地方再大家指正。

<!--more-->

### 1、第一梯队：SUSE Linux Enterprise Server（OpenSuSE）, RedHat Linux Entiprise Server（CentOS）

有的同学会问啦，为什么把这两个放在第一梯队？答案很简单，因为这两种发行版都是企业级的，更加稳定。所有软件都是经过大量的测试的。

[![800px-SuSE-logo.svg](http://blog.kangzj.net/wp-content/uploads/2009/08/800px-SuSE-logo.svg_.png "800px-SuSE-logo.svg")](http://blog.kangzj.net/wp-content/uploads/2009/08/800px-SuSE-logo.svg_.png)

SUSE Linux系统在高度可靠性、可扩展性和安全性等方面表现的还算不错，提供经济实惠、可互操作且易于管理开源平台，从而有助于提供企业关于高性能、关键任务业务服务。当然，对于安全<span>网络</span>基础设施、基本Web基础设施搭建做到恰到好处。OpenSUSE 是 Novell 公司发行的SUSE Linux 企业版的系统基础，是免费的。

[![logo_rh_home](http://blog.kangzj.net/wp-content/uploads/2009/08/logo_rh_home.png "logo_rh_home")](http://blog.kangzj.net/wp-content/uploads/2009/08/logo_rh_home.png) [![centos](http://blog.kangzj.net/wp-content/uploads/2009/08/centos.jpg "centos")](http://blog.kangzj.net/wp-content/uploads/2009/08/centos.jpg)

同样，RadHat企业版服务器也是十分稳定。CentOS 是 RHEL（Red Hat  Enterprise  Linux）源代码再编译的产物，是免费的，而且在 RHEL 的基础上修正了不少已知的 Bug ，相对于其他 Linux 发行版，其稳定性值得信赖。另外，由于  Fedora Core 计划也归根于 Red Hat 系，所以在绝大多数情况下，使用 Fedora  Core 的朋友，也同样能够通过本站介绍的各种 CentOS 方面相关的技巧、方法来完成服务器的构建和维护工作。

不知道大家注意到了没有，SuSE和RedHat的收费和免费版本的不同之处，我不说，大家找到了可以在留言里说下～～

另外说一句，虽然SuSE和RedHat的企业级服务器都是收费的，但是相对于Windows来说，还是比较便宜的，如果资金允许的话，大家可以购买下企业版，支持下他们，并且可以享受到技术支持和升级服务。

### 2、第二梯队：Debian Linux

[![debian](http://blog.kangzj.net/wp-content/uploads/2009/08/debian.jpg "debian")](http://blog.kangzj.net/wp-content/uploads/2009/08/debian.jpg)

虽然把Debian放在第二梯队，并不说Debian不如上面两个Linux系统。<span id="zoom">Debian 最早由Ian Murdock于1993年创建。可以算是迄今为止，最遵循GNU规范的Linux系统。</span>

<span id="zoom">Debian的Stable版本虽然软件版本很过时，但是却是经过大量的测试，十分稳定，非常适合于服务器使用。</span>

### <span>3、第三梯队：其它Linux发行版本的Server版</span>

<span>比如Ubuntu的Server版，红旗Server版等等。Server版相对于Desktop版本来说都是经过优化的，更加适合做Server（这句好像是废话）。</span>

### <span>4、第四梯队：其它Linux版本</span>

<span>虽说不如专门的Server版的稳定，也只是相对而言。如果跟Windows的Server比起来，那就是相当稳定了，不多说了。</span>

<span>最后需要说明的一点就是在选择的时候一定要注意支持的时间，比如Ubuntu 8.04 LTS提供长达五年的支持，而最新的Server9.04版本却没有这样的待遇，如果用Ubuntu的Server那肯定是这个8.04 LTS莫数了。最新的不一定是最好的，作服务器，稳定是第一位的。
</span>