---
title: C++中成员函数的连续调用
tags:
  - const
  - cpp
  - 对象
  - 引用
  - 类
  - 连续调用
id: 1033
categories:
  - Programming
date: 2009-10-05 03:27:30
---

首先说下什么是我所谓的_连续调用_，假设有一个类person：
<div>
<table border="0" width="100%">
<tbody>
<tr id="p10661">
<td id="p1066code1">
<pre style="FONT-FAMILY: monospace">person a<span style="COLOR: #008080">;</span>
a.<span style="COLOR: #007788">set</span><span style="COLOR: #008000">(</span><span style="COLOR: #ff0000">"kangzj"</span><span style="COLOR: #008000">)</span>.<span style="COLOR: #007788">get</span><span style="COLOR: #008000">(</span><span style="COLOR: #008000">)</span>.<span style="COLOR: #007788">set</span><span style="COLOR: #008000">(</span><span style="COLOR: #ff0000">"abc"</span><span style="COLOR: #008000">)</span><span style="COLOR: #008080">;</span></pre>
</td>
</tr>
</tbody></table>
</div>
加红的部分即为本文要说的_连续调用_。

怎么实现呢，很简单，只要让成员函数返回一个指向当前对象的_引用_即可，于是，我这样定义这个类：

<span id="more-1066"> <!--more--></span>
<div>
<table border="0" width="100%">
<tbody>
<tr id="p10662">
<td id="p1066code2">
<pre style="FONT-FAMILY: monospace"><span style="COLOR: #0000ff">class</span> person<span style="COLOR: #008000">{</span>
<span style="COLOR: #0000ff">private</span><span style="COLOR: #008080">:</span>
	string name<span style="COLOR: #008080">;</span>
<span style="COLOR: #0000ff">public</span><span style="COLOR: #008080">:</span>
	<span style="COLOR: #0000ff">const</span> person<span style="COLOR: #000040">&amp;</span> get<span style="COLOR: #008000">(</span><span style="COLOR: #008000">)</span> <span style="COLOR: #0000ff">const</span><span style="COLOR: #008080">;</span>
	person<span style="COLOR: #000040">&amp;</span> set<span style="COLOR: #008000">(</span>string n<span style="COLOR: #008000">)</span><span style="COLOR: #008080">;</span>
<span style="COLOR: #008000">}</span><span style="COLOR: #008080">;</span>
<span style="COLOR: #0000ff">const</span> person<span style="COLOR: #000040">&amp;</span> person<span style="COLOR: #008080">::</span><span style="COLOR: #007788">get</span><span style="COLOR: #008000">(</span><span style="COLOR: #008000">)</span><span style="COLOR: #008000">{</span>
	<span style="COLOR: #0000dd">cout</span><span style="COLOR: #000080">&lt;&lt;</span>name<span style="COLOR: #008080">;</span>
	<span style="COLOR: #0000ff">return</span> <span style="COLOR: #000040">*</span><span style="COLOR: #0000dd">this</span><span style="COLOR: #008080">;</span>
<span style="COLOR: #008000">}</span>
person<span style="COLOR: #000040">&amp;</span> person<span style="COLOR: #008080">::</span><span style="COLOR: #007788">set</span><span style="COLOR: #008000">(</span>string t<span style="COLOR: #008000">)</span><span style="COLOR: #008000">{</span>
	name<span style="COLOR: #000080">=</span>t<span style="COLOR: #008080">;</span>
	<span style="COLOR: #0000ff">return</span> <span style="COLOR: #000040">*</span><span style="COLOR: #0000dd">this</span><span style="COLOR: #008080">;</span>
<span style="COLOR: #008000">}</span></pre>
</td>
</tr>
</tbody></table>
</div>
Ok，可以使用了。这样的句子还是编译不会成功：
<div>
<table border="0" width="100%">
<tbody>
<tr id="p10663">
<td id="p1066code3">
<pre style="FONT-FAMILY: monospace">a.<span style="COLOR: #007788">set</span><span style="COLOR: #008000">(</span><span style="COLOR: #ff0000">"kangzj"</span><span style="COLOR: #008000">)</span>.<span style="COLOR: #007788">get</span><span style="COLOR: #008000">(</span><span style="COLOR: #008000">)</span>.<span style="COLOR: #007788">set</span><span style="COLOR: #008000">(</span><span style="COLOR: #ff0000">"abitno"</span><span style="COLOR: #008000">)</span><span style="COLOR: #008080">;</span></pre>
</td>
</tr>
</tbody></table>
</div>
因为调用const型成员函数的this指针是const型，指向的对象也是const型，无法改变对象的成员变量。也就是说没法执行set操作，而出错。
怎样来解决这个问题呢？把get()重载，在单独调用get的时候调用const型的方法，在连续调用的时候调用非const的方法（当然都是自动的），基于这种思想可以这样来设计类（下面代码可以直接编译运行）：
<div>
<table border="0" width="100%">
<tbody>
<tr id="p10664">
<td id="p1066code4">
<pre style="FONT-FAMILY: monospace"><span style="COLOR: #339900">#include &lt;iostream&gt;</span>
<span style="COLOR: #339900">#include &lt;string&gt;</span>

<span style="COLOR: #0000ff">using</span> <span style="COLOR: #0000ff">namespace</span> std<span style="COLOR: #008080">;</span>
<span style="COLOR: #0000ff">class</span> person<span style="COLOR: #008000">{</span>
<span style="COLOR: #0000ff">private</span><span style="COLOR: #008080">:</span>
	string name<span style="COLOR: #008080">;</span>

<span style="COLOR: #0000ff">public</span><span style="COLOR: #008080">:</span>
	<span style="COLOR: #0000ff">const</span> person<span style="COLOR: #000040">&amp;</span> get<span style="COLOR: #008000">(</span><span style="COLOR: #008000">)</span> <span style="COLOR: #0000ff">const</span><span style="COLOR: #008080">;</span>
	person<span style="COLOR: #000040">&amp;</span> get<span style="COLOR: #008000">(</span><span style="COLOR: #008000">)</span><span style="COLOR: #008080">;</span>
	person<span style="COLOR: #000040">&amp;</span> set<span style="COLOR: #008000">(</span>string n<span style="COLOR: #008000">)</span><span style="COLOR: #008080">;</span>
<span style="COLOR: #008000">}</span><span style="COLOR: #008080">;</span>
<span style="COLOR: #0000ff">const</span> person<span style="COLOR: #000040">&amp;</span> person<span style="COLOR: #008080">::</span><span style="COLOR: #007788">get</span><span style="COLOR: #008000">(</span><span style="COLOR: #008000">)</span> <span style="COLOR: #0000ff">const</span><span style="COLOR: #008000">{</span>
	<span style="COLOR: #0000dd">cout</span><span style="COLOR: #000080">&lt;&lt;</span>name<span style="COLOR: #000080">&lt;&lt;</span><span style="COLOR: #ff0000">" -const<span style="COLOR: #000099; FONT-WEIGHT: bold">n</span>"</span><span style="COLOR: #008080">;</span>
	<span style="COLOR: #0000ff">return</span> <span style="COLOR: #000040">*</span><span style="COLOR: #0000dd">this</span><span style="COLOR: #008080">;</span>
<span style="COLOR: #008000">}</span>
person<span style="COLOR: #000040">&amp;</span> person<span style="COLOR: #008080">::</span><span style="COLOR: #007788">get</span><span style="COLOR: #008000">(</span><span style="COLOR: #008000">)</span><span style="COLOR: #008000">{</span>
	<span style="COLOR: #0000dd">cout</span><span style="COLOR: #000080">&lt;&lt;</span>name<span style="COLOR: #000080">&lt;&lt;</span><span style="COLOR: #ff0000">" -not const<span style="COLOR: #000099; FONT-WEIGHT: bold">n</span>"</span><span style="COLOR: #008080">;</span>
	<span style="COLOR: #0000ff">return</span> <span style="COLOR: #000040">*</span><span style="COLOR: #0000dd">this</span><span style="COLOR: #008080">;</span>
<span style="COLOR: #008000">}</span>
person<span style="COLOR: #000040">&amp;</span> person<span style="COLOR: #008080">::</span><span style="COLOR: #007788">set</span><span style="COLOR: #008000">(</span>string t<span style="COLOR: #008000">)</span><span style="COLOR: #008000">{</span>
	name<span style="COLOR: #000080">=</span>t<span style="COLOR: #008080">;</span>
	<span style="COLOR: #0000ff">return</span> <span style="COLOR: #000040">*</span><span style="COLOR: #0000dd">this</span><span style="COLOR: #008080">;</span>
<span style="COLOR: #008000">}</span>

<span style="COLOR: #0000ff">int</span> main<span style="COLOR: #008000">(</span><span style="COLOR: #008000">)</span>
<span style="COLOR: #008000">{</span>
	person a<span style="COLOR: #008080">;</span>
	a.<span style="COLOR: #007788">set</span><span style="COLOR: #008000">(</span><span style="COLOR: #ff0000">"kangzj"</span><span style="COLOR: #008000">)</span>.<span style="COLOR: #007788">get</span><span style="COLOR: #008000">(</span><span style="COLOR: #008000">)</span>.<span style="COLOR: #007788">set</span><span style="COLOR: #008000">(</span><span style="COLOR: #ff0000">"ddd"</span><span style="COLOR: #008000">)</span>.<span style="COLOR: #007788">get</span><span style="COLOR: #008000">(</span><span style="COLOR: #008000">)</span><span style="COLOR: #008080">;</span>
	a.<span style="COLOR: #007788">get</span><span style="COLOR: #008000">(</span><span style="COLOR: #008000">)</span><span style="COLOR: #008080">;</span>
	<span style="COLOR: #0000ff">const</span> person b<span style="COLOR: #008080">;</span>
	b.<span style="COLOR: #007788">get</span><span style="COLOR: #008000">(</span><span style="COLOR: #008000">)</span><span style="COLOR: #008080">;</span>
<span style="COLOR: #008000">}</span></pre>
</td>
</tr>
</tbody></table>
</div>
全文完，欢迎讨论。
参考资料：《C++ Primer(第三版)》