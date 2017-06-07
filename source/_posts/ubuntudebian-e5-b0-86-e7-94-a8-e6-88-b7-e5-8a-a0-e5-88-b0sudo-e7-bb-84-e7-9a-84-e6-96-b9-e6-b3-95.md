---
title: Ubuntu/Debian将用户加到sudo组的方法
tags:
  - debian
  - sudo
  - ubuntu
id: 1657
categories:
  - Systems&amp;Servers
date: 2010-03-08 09:33:45
---

这个问题虽然简单，但是确是经常被问到的问题。因为只有加到sudo list的用户才能使用sudo命令拿到root权限。下面把怎么做写出来，也算是给自己备忘一下：

1.  打开一个终端，输入：
sudo visudo
2.  找找已经存在的用户：
root ALL=(ALL) ALL
3.  照葫芦画瓢，加入你想加的用户:
user ALL=(ALL) ALL
4.  按Ctrl+x，再按y保存退出