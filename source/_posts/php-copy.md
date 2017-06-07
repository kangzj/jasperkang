---
title: PHP中的拷贝
tags:
  - php
  - 对象
  - 拷贝
  - 类
id: 1907
categories:
  - Programming
date: 2012-02-08 17:47:03
---

对象用等号赋值，只是引用，是浅拷贝，除非使用_clone_关键字。

而基本类型，int、float、string、array几种类型<del>都是复制</del>也是引用，不过有copy-on-write机制控制，感觉好像是直接复制，但是效率却高一些。基本类型如果想传引用，需要加一个&amp;.

下面代码可以说明：<!--more-->
<pre>n = 2;

echo 'a=' . $a-&gt;n . "n";
echo 'b=' . $b-&gt;n;

$c = '11a';
$d = $c;
$c = '22b';

echo 'c=' . $c . "n";
echo 'd=' . $d;</pre>