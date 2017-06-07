---
title: 关于“永久链接”/“固定链接”和301重定向
tags:
  - 301重定向
  - permanent link
  - php
  - rewrite
  - sablog
  - wordpress
  - 固定链接
  - 永久链接
id: 133
categories:
  - Blogging
date: 2009-06-15 00:18:05
---

    看到一篇关于“**永久链接**”的文章，觉得写得不错，这里介绍给大家，并且把我应用中的一些问题也给写一下。

    这个是原文：[http://blogunion.org/wordpress/wordpress-tips/url-setting-tips.html](http://blogunion.org/wordpress/wordpress-tips/url-setting-tips.html)，主要写了这几点：
	<li>     (1) 不要让日期出现在**永久链接**里面;</li>
	<li>     (2) 不要让分类的链接出现在**永久链接**里面;</li>
	<li>     (3) **永久链接**不要过深;</li>
	<li>     (4) 不要让中文字符出现在**永久链接**里面;</li>
	<li>     (5) 好的**永久链接**形式是:域名/文章名;</li>
<!--more-->

    原来我不是很理解“**永久链接**”的意思，在转换了博客的程序之后，就完全理解了：**永久链接**也叫**固定链接**就是在你的网站程序发生了变化之后，只要保证**永久链接**不变，大家还能通过搜索引擎或者超链接访问到你的文章。

    以我的博客为例，我之前用的程序是sablog开启了**永久链接**，每篇文章都有一个**永久链接**，在转换数据的时候，把这个**永久链接**也加入了wordpress的数据库，这样就保证了文章的地址不变，不会影响原有文章的访问。

    但是sablog的archiver的文章的url是 http://kangzj.net.ru/archiver/?xxx.html 的形式而不是 http://kangzj.net.ru/xxx/ 的形式，如果用这样的地址来访问新网站，自然会得到一个“404”。怎么办呢——还好，我们的wordpress开启了rewrite，也就是所有的请求都是交给index.php来处理的，这就好办了，通过判断访问的URI把访问较多的文章用“**301重定向**”定到该文章的**固定链接**地址就OK了，比如：
<pre lang="php">$request_uri=$_SERVER[''REQUEST_URI];
switch($request_uri)
{
    case '/achiver/?xxxx.html':
      $request_uri='/abc/';
      break;
    default:
      .....;
}
header('HTTP/1.1 301 Moved Permanently');
header('Location: http://kangzj.net.ru'.$request_uri);
exit;</pre>
    下面是我的网站正在用的（因为网站之前还用过别的域名，所以还加了域名的**301重定向**），加在wordpress的index.php最前面的代码，把以前网站的好多有流量的但是现在丢失了的链接给“**301重定向**”到新的“**永久链接**”：
<pre lang="php">//如果是别的域名，永久转向kangzj.net.ru
$host = $_SERVER['HTTP_HOST'];
$request_uri = isset($_SERVER['REQUEST_URI']) ? $_SERVER['REQUEST_URI'] : '';
$flag=0;
switch ($request_uri)
{
	case '/read.php/65.html':
		$request_uri = '/linux-start-on-boot/';
		break;
	case '/read.php/65.htm':
		$request_uri = '/linux-start-on-boot/';
		break;
	case '/read.php/76.htm':
		$request_uri = '/fckeditor-not-proper-response/';
		break;
	case '/archiver/?article-55.html':
		$request_uri = '/asus-x81-ar2009-ar928x-driver/';
		break;
	case '/archiver/?article-63.html':
		$request_uri = '/different-copiler-error/';
		break;
	case '/archiver/?article-72.html':
		$request_uri = '/zoj-1002/';
		break;
	case '/archiver/?article-59.html':
		$request_uri = '/fckeditor-not-proper-response/';
		break;
	case '/archiver/?article-51.html':
		$request_uri = '/linux-for-human/';
		break;
	case '/archiver/?article-47.html':
		$request_uri = '/squid-reverse-proxy/';
		break;
	case '/archives/65/':
		$request_uri = '/dynamic-ip-as-server/';
		break;
	case '/archives/46/':
		$request_uri = '/apache-ipv6-proxy-3/';
		break;
	case '/archives/45/':
		$request_uri = '/iis6-ipv6/';
		break;
	case '/archives/44/':
		$request_uri = '/apache-ipv6-proxy-2/';
		break;
	case '/date/200906/':
		$request_uri = '/2009/06/';
		break;
	case '/archives/73/':
		$request_uri = '/poj-2000/';
		break;
	default:
		$flag=1;
		break;
}

if($host!='kangzj.net.ru' || $flag==0)
{

	header('HTTP/1.1 301 Moved Permanently');
	header('Location: http://kangzj.net.ru'.$request_uri);
	exit;
}
//--------------------------------------</pre>
    做完之后才发现，有一个链接竟然很火，这一天从百度就来了将近40个IP，嗯，多亏做了下，要不损失大了。