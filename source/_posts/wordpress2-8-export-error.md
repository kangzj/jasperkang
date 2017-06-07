---
title: wordpress2.8中文版导出数据时错误解决方法
tags:
  - php
  - wordpress
  - 导出数据
id: 259
categories:
  - Blogging
date: 2009-07-09 17:07:51
---

> 错误说是找不到"../../../wp_config.php"和"../../../wp-settings.php"，出错脚本是：wp-content/plugins/wp-codebox/wp-codebox.php，下面就是一堆乱七八糟的东西。
<!--more-->
> 解决方法：找到wp-content/plugins/wp-codebox/wp-codebox.php，把其中的"../../../wp_config.php"和"../../../wp-settings.php"改成"../wp_config.php"和"../wp-settings.php"即可。
> 
>     出错原因是调用wp-codebox.php的脚本是：/wp-admin/export.php，相对于这个脚本，那两个文件是在上一级目录的，而不是原来那样的上三级。