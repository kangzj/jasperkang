---
title: CSS实现表格单元格强制换行和强制不换行
tags:
  - css
id: 9
categories:
  - Web-Development
date: 2008-08-20 02:58:09
---

引用

用CSS实现表格单元格数据自动换行或不换行

1、自动换行：

&lt;style type="text/css"&gt;

.AutoNewline

{

  word-break: break-all;/*必须*/

}

&lt;/style&gt;

&lt;table&gt;

&lt;tr&gt;

  &lt;td class="AutoNewline"&gt;自动换行自动换行自动换行自动换行自动换行自动换行自动换行自动换行自动换行自动换行自动换行自动换行自动换行自动换行自动换行自动换行自动换行自动换行自动换行自动换行自动换行自动换行自动换行自动换行&lt;/td&gt;

&lt;/tr&gt;

&lt;/table&gt;

2、不换行：

&lt;style type="text/css"&gt;

.NoNewline

{

word-break: keep-all;/*必须*/

}

&lt;/style&gt;

&lt;table&gt;

&lt;tr&gt;

  &lt;td class="NoNewline"&gt;不换行不换行不换行不换行不换行不换行不换行不换行不换行不换行&lt;/td&gt;

&lt;/tr&gt;

&lt;/table&gt;