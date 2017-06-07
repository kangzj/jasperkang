---
title: 正则表达式（Regular Expressions）学习
tags:
  - grep
  - linux
  - vi
  - 正则表达式
id: 84
categories:
  - Systems&amp;Servers
date: 2009-06-03 13:47:16
---

 1\. 简介

什么是正则表达式？一个正则表达式就是用来在一次搜索中匹配相同字符的一个字符模式。在大多数程序是，把一个正则表达式装在两个正斜杠里，即/love/的形式。
2\. 正则表达式元字符<!--more-->

^： 行开头定位 例：/^love/，该正则表达式表示 与所有love开头的行相匹配
$： 行末尾定位 例：/love$/，该正则表达式与所有love结尾的行相匹配
.：  匹配单个字符 例：/l..e/ ，该正则表达式可以代替单个的字符
<span style="color: #ff0000">*：  跟前驱的0个或多个字符相匹配 例：/*love/ <span style="color: #000000;">，</span><span style="color: #ff0000">该正则表达式跟</span>0个或多个空格后面跟love的模式相匹配
</span>[]： 与集中的一个相匹配 例：/[Ll]ove/，该正则表达式与Love和love相匹配
[x-y]： 与集中的一个范围内的一个字符想匹配 例：/[A-Z]ove/，该正则表达式不以A-Z开头的ove字符相匹配
[^]： 不…… 例：/[^L]ove/，该正则表达式不与Love相匹配
：  给元字符转义 例：/love./，该正则表达式表示"love."，给元字符.转义

另外许多用正则表达式的的linux/unix程序支持附加的元字符：

&lt;：词开头定位，例：/&lt;love/，该正则表达式表示一个以love开头的词(vi和grep支持)
&gt;：词结尾定位，例：/love&gt;/，该正则表达式表示一个以love结尾的词(vi和grep支持)
<span style="color: #ff0000">(..)：标志与以后用的字符相匹配，例：(love)able1er/，该正则表达式able可达9个标志，模式最左边用第一个标志开始。例，模式love保存做标志1,以后引用做1；在此例中，搜索模式包括后面跟lover的lovable(sed、vi和grep支持)</span>
x{m}或x{m,n}：字符x重复m次或m次与n次之间，例：o{5,10}，该正则表达式可匹配5-10个连续的o(vi和grep支持)

vi和grep都要用正则表达式，先小学一下做个基础。