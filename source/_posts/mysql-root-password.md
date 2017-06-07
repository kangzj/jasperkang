---
title: MySQL更改/修改root密码的三种方法
tags:
  - mysql
id: 16
categories:
  - Systems&amp;Servers
date: 2008-07-23 03:52:21
---

第一种：

mysql&gt;UPDATE user SET Password=PASSWORD('new_password') WHERE user='root'; 

mysql&gt;FLUSH PRIVILEGES;

第二种：

mysql&gt;SET PASSWORD FOR root=PASSWORD('new_password');

第三种：

shell&gt;mysqladmin -u root password new_password;