---
title: SQL2000因程序挂起而无法安装问题的解决
tags:
  - sqlserver2000
id: 27
categories:
  - Software
date: 2007-11-17 12:06:35
---

来源：未知

    以前的某个程序安装已在安装计算机上创建挂起的文件操作 解决办法
    以前装过sql server，后来删掉。现在重装，却出现“以前的某个程序安装已在安装计算机上创建挂起的文件操作。运行安装程序之前必须重新启动计算机”错误。无法进行下去。

     步骤是：

1）添加/删除程序中彻底删除sql server。

2）将没有删除的sql server目录也删除掉。

3）打开注册表编辑器，在HKEY_LOCAL_MACHINESYSTEMCurrentControlSetControlSession Manager中找到PendingFileRenameOperations项目，并删除它。这样就可以清除安装暂挂项目。

4）删除注册表中跟sql server相关的键。

其实估计只要做第3步就可以搞定，这样就可以清除安装暂挂项目。自己是先走了1，2，4，最后做了3才搞定。所以估计3才是最关键的