---
title: Html+Asp+Php+Jsp禁止浏览器缓存的方法
tags:
  - asp
  - html
  - jsp
  - php
  - 禁止缓存
id: 11
categories:
  - Web-Development
date: 2008-07-30 13:21:11
---

HTTP:
&lt;META HTTP-EQUIV="pragma" CONTENT="no-cache"&gt;
&lt;META HTTP-EQUIV="Cache-Control" CONTENT="no-cache, must-revalidate"&gt;
&lt;META HTTP-EQUIV="expires" CONTENT="Wed, 26 Feb 1997 08:21:57 GMT"&gt;
&lt;META HTTP-EQUIV="expires" CONTENT="0"&gt;

ASP
response.expires=0
response.addHeader("pragma","no-cache")
response.addHeader("Cache-Control","no-cache, must-revalidate")

PHP
header("Expires: Mon, 26 Jul 1997 05:00:00 GMT");
header("Cache-Control: no-cache, must-revalidate");
header("Pragma: no-cache");

JSP：
response.addHeader("Cache-Control", "no-cache");
response.addHeader("Expires", "Thu, 01 Jan 1970 00:00:01 GMT");