---
title: 计算php运行时间（毫秒数）
tags:
  - php
  - 运行时间
id: 1755
categories:
  - Programming
date: 2010-09-08 10:37:48
---

非常简单，记录一下：
<pre lang="php">$t1 = microtime(true);

//php script here

$t2 = microtime(true);</pre>
<pre lang="php">echo (($t2-$t1)*1000).'ms';</pre>