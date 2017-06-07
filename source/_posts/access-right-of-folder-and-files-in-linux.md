---
title: Linux中文件和目录的权限问题
tags:
  - linux
  - nginx
  - php
  - shell
  - vps
  - 文件
  - 权限
  - 目录
id: 1445
categories:
  - Systems&amp;Servers
date: 2009-12-03 15:50:36
---

最近搞了几个VPS玩，VPS一般来说内存都不多，配置轻量级的Nginx+PHP，折腾当中权限问题搞了半天。

大家都知道，Linux中文件和目录都有自己的权限，分为rwx三种，分别代表读、写、执行的权限。但是目录和文件又不一样，不能被写和执行，文件rwx三种权限与目录的对比如下：
<table border="0" cellspacing="0" cellpadding="2" width="447">
<tbody>
<tr>
<td width="133" valign="top">权限</td>
<td width="43" valign="top">文件</td>
<td width="269" valign="top">目录</td>
</tr>
<tr>
<td width="133" valign="top">r</td>
<td width="43" valign="top">读</td>
<td width="269" valign="top">可以列表该目录中的文件</td>
</tr>
<tr>
<td width="133" valign="top">w</td>
<td width="43" valign="top">写</td>
<td width="269" valign="top">可以在该目录中创建或者删除文件</td>
</tr>
<tr>
<td width="133" valign="top">x</td>
<td width="43" valign="top">执行</td>
<td width="269" valign="top">可以搜索或者进入该目录</td>
</tr>
</tbody></table>
现在很多的博客代码都提供在线安装插件或者升级等方便的功能，但是如果权限设置的不正确就无法使用，比如《[WordPress“执行请求操作，连接信息必需提供”解决方法](http://kangzj.net/wordpress-link-info-required-to-proceed-your-request/)》中提到就是这样的问题。

<!--more-->我们假设目录的所有者为kk，执行fastcgi的用户为www-data，

www-data不能正常操作（创建和删除）文件是这种现象的根本原因。但是以上文中用的方法，把所有文件的所有都更改为www-data可以解决，但是并不完美，因为文件真正的所有者kk就不能正常操作文件了。

现在想了一个解决方法：

首先把www-data这个用户加入kk组，然后把所有文件及文件夹的属性设置为770，理论上应该可以啊，但是就没有实验成功。正在接着折腾，就不信了。折腾完之后向大家汇报。有明白我加我GT告诉我下哈：kangzj#kangzj.net。