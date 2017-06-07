---
title: php json_encode utf-8中文问题
tags:
  - json
  - php
  - 中文
  - 编码
id: 1905
categories:
  - Programming
date: 2013-05-29 09:47:43
---

utf-8字符json_encode为变成转成utf16编码，也就是介个样子：
> <pre>$ ./php/bin/php -r 'echo json_encode("中文");'
> "u4e2du6587"</pre>
可读性降低，最新的php 5.4的json_encode支持了UTF-8编码，可以把中文不编码直接输出。
那低版本怎么办呢？也有办法，封装成一个函数给大家分享一下：
> <pre>function my_json_encode($var) {
>     return preg_replace("/\u([a-f0-9]{4})/e", 
>       "iconv('UCS-4LE','UTF-8',pack('V', hexdec('U$1')))", json_encode($var));
> }</pre>