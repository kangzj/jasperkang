---
title: 自制Google PageRank查询工具(WordPress版)
tags:
  - google
  - pagerank
  - php
  - pr
  - pr查询制作
  - wordpress
id: 307
categories:
  - Blogging
date: 2009-07-17 12:27:34
---

自己做的Google PageRank查询工具已经挂的博客上挺长时间了，也不知道有没有人在用，或许就我自己在用吧，这里就把做的过程跟大家说一下，非常的简单。

首先找到一个php版的查询pr的接口，我用的是：http://www.pagerankcode.com/download.html ，下载下来之后我另存为：[pr.php](http://blog.kangzj.net/wp-content/uploads/2009/07/pr1.rar)

然后新建一个wordpress模板，代码：[pagerank.php](http://blog.kangzj.net/wp-content/uploads/2009/07/pagerank.php_.rar) 。

然后把这两个文件解压，放在当前主题目录下，比如我就放在：wp-content/themes/iblog2/
<!--more-->
到WordPress后台，点击“添加新页面”，模板选择PageRank，其它填好，就可以发布了。下面是添加页面示意图：
![](http://kangzj.net/wp-content/uploads/images/200907/20090717-pr-page-add.jpg "添加pr查询页面")
下面是效果的示意图：

![](http://kangzj.net/wp-content/uploads/images/200907/20070717-pr-page-xiaoguo.jpg "pr查询页面效果图")

链接：[http://kangzj.net/pagerank/](http://kangzj.net/pagerank/)
如有问题，请留言讨论。