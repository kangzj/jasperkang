---
title: cookie的作用域问题(php)
tags:
  - cookie
  - php
id: 7
categories:
  - Web-Development
date: 2008-07-25 17:00:53
---

php 中设置cookie 的代码：setcookie()
注意cookie的作用域：
setcookie("cookie名","值","作用域")
作用域“/”表示COOKIE作用在根目录下所有文件
作用域“/ROOT/”表示COOKIE作用在根目录下ROOT目录下的所有文件
还有cookie不能跨域~~
具体有空再研究一下