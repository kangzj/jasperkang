---
title: wdlinux面板wdcp失效的问题
tags:
  - linux
  - wdcp
  - wdlinux
id: 1958
categories:
  - Systems&amp;Servers
date: 2013-11-15 10:23:51
---

前些日子帮一个朋友恢复wdcp的数据，恢复完成之后发现站点操作全部执行失败，仔细找了一天无果。后来将wdcp的wdapache、wdphp打开错误日志，看到了一个sudo相关的错误，本来就知道应该是权限导致的问题，现在sudo的错误提示更说明了这一点。

于是乎打开sudo的配置文件/etc/sudoers，发现home是有特殊权限的，于是将home分区重新加载到别的分区，然后在wdcp系统面板中更改了新分区，问题解决。

以前一直没想明白面板用户是怎样管理别的用户的文件的，我太傻了，可以sudo嘛，当然为了安全起见，最好在/etc/sudoer里指定用户可以执行的命令。