---
title: Rewrite和Redirect的区别与联系
tags:
  - redirect
  - rewrite
id: 846
categories:
  - Web-Development
date: 2009-09-02 09:35:38
---

看到这个题目，希望大家不要头疼，呵呵，有点像政治里的简答题吧，呵呵，我故意的:-)

我们经常会用到这两个概念，大家对他们的功能已经很熟悉了，我罗嗦下，不过肯定有你不知道的地方哦：

**URL Rewrite**：写在.htaccess中（当然也可以写在Apache的主配置文件中），把不好看的、带一堆参数的URL利用正则表达式变成很友好的URL，WordPress的固定链接就是URL Rewrite实现的，可以参考我的URL:-)，下面是WordPress的.htaccess（意义：如果不是存在的文件或者目录，就Rewrite到index.php处理）：

<!--more-->
> # BEGIN WordPress
> &lt;IfModule mod_rewrite.c&gt;
> RewriteEngine On
> RewriteBase /
> RewriteCond %{REQUEST_FILENAME} !-f
> RewriteCond %{REQUEST_FILENAME} !-d
> RewriteRule . /index.php [L]
> &lt;/IfModule&gt;
> # END WordPress
**Redirect**：可以写在.htaccess中，也可以用动态语言（php,jsp等）来发送相关Header信息。多用于URL发生改变时，将旧的URL定位到新的URL。Redirect有三种：301，302，303。这几种信号对用户来说没有什么意义，他们看到效果只是一个跳转，浏览器中旧的URL变成了新的URL。所以它们主要是对搜索引擎的，告诉搜索引擎，这个跳转的含义是什么。
> 301：永久重定向。
> 
> 302：临时重定向（http 1.0）；Found(http 1.1)。
> 
> 303：对于POST请求，它表示请求已经被处理，客户端可以接着使用GET方法去请求Location里的URI。
> 
> 307：对于POST请求，表示请求还没有被处理，客户端应该向Location里的URI重新发起POST请求。
话说现在已经是普及http 1.1的时代了，所以，302已经不是大家常说的临时重定向的含义了，它表示Found，什么意思呢？——就是找到了相关的URL，然后给你定位到相应的URL。而我们平时说的临时重定向应该是303或者307了。下面是用php Redirect的例子：
> header('HTTP/1.1 303 See Other');
> header('Location: http://localhost/');
用.htaccess来Redirect的例子：
> Redirect /wordpress http://yourdomain.com/blog
这种情况默认是用302重定向的。

还有一种情况，用Rewrite这样写：
> RewriteRule ^wordpress(.*)$ /blog$1 [R=301,L]
奇怪吧，Rewrite也可以用来做Redirect。只不过这里Rewrite跟平时的Rewrite就不一样了，浏览器中URL会发生改变。

说了这么多，应该说清楚了，打完收工:-)

有问题请留言，说的不对的请指正。