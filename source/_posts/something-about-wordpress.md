---
title: 关于WordPress，这些也许你不知道
tags:
  - wordpress
  - wordpress注意事项
  - wordpress设置
id: 1491
categories:
  - Blogging
date: 2009-12-10 01:38:45
---

这篇文章是写给比我还菜的菜菜看的，WordPress老鸟请直接飘过即可。

### 1\. “WordPress 自动校正错误的 XHTML 代码”

位置：设置-&gt;撰写

这个功能很好呀，如果你手工写的标签没有关闭，WordPress会自动帮你补全，很方便。但是这个功能也有办错事的时候，比如，我要输入一些C代码的时候，可能会出现下面的效果：

[![strlen](http://blog.kangzj.net/wp-content/uploads/2009/12/strlen_thumb.jpg "strlen")](http://blog.kangzj.net/wp-content/uploads/2009/12/strlen1.jpg)

这个错误的演示地址：[http://kangzj.net/preminder-beta-source-code/](http://kangzj.net/preminder-beta-source-code/ "http://kangzj.net/preminder-beta-source-code/")

WordPress自动把我们代码里的东西给配对了，你到编辑器里去删除也无济于事，因为在你提交的时候WordPress又会勤快地帮你加上。所以，如果经常贴代码的同学最好禁用这个功能。不经常贴代码的同学，这个功能其实也没啥用，因为你可能都不会用Code模式的编辑器。综上所述，这个功能有点鸡肋，建议关闭，默认貌似是开启的。

### <!--more-->2\. &lt;!—more—&gt;

这个&lt;!—more—&gt;困扰了我好久，看到别人的首页能够显示摘要，而我的是全文，相当不爽，首页简直都有半米长了，俺也想显示摘要。找了半天才发现，只要在代码里加上&lt;!—more—&gt;（也有按钮），或者在可视化视图里点击某个按钮即可（自己找去吧，吼吼）。

### 3\. 留言分页与嵌套

位置：设置-&gt;讨论

以前一直在用一个插件，叫做WP Paged Comments，可以实现留言分页的功能。却不知道何时起WordPress自己就有了这个功能，只要在这里设置下就OK了。不过好像需要主题支持，我的主题没有问题，吼吼。嵌套同理。

### 4\. 后台首页加载慢

[![image](http://blog.kangzj.net/wp-content/uploads/2009/12/image_thumb.png "image")](http://blog.kangzj.net/wp-content/uploads/2009/12/image.png)WordPress后台首页加载了大量的RSS啥的，如果网速慢的话还真是得加载半天，大部分内容没有什么用，可点击右上角的显示选项来关闭。这个选项在好几个页面也有，以订制该页面的内容，十分方便。另外，可以启用Gears，点击在路上角的加速即有提示。

### 5\. 关于杂项

位置：设置-&gt;杂项

[![image](http://blog.kangzj.net/wp-content/uploads/2009/12/image_thumb1.png "image")](http://blog.kangzj.net/wp-content/uploads/2009/12/image1.png)

**默认上传路径**：可以选择保存图片等附件的位置，建议用相对目录或者就不要动它，否则一旦更换服务器又得重改。

**文件完整的URL地址**：就是访问这些附件的地址，建议设置另一个域名，这样可以减少Cookie的发送，给你的WordPress提速（参见大猫：[http://ooxx.me/cookie-free-domains-yslow.orz](http://ooxx.me/cookie-free-domains-yslow.orz "http://ooxx.me/cookie-free-domains-yslow.orz")，不过跟我的设置方法有不同）。

### 6\. “执行请求操作，连接信息必需提供”

《[WordPress“执行请求操作，连接信息必需提供”解决方法](http://kangzj.net/wordpress-link-info-required-to-proceed-your-request/)》中讲过了，不过还有种方法哦，更加简单些，但是要求有ftp或者sftp服务，详见大猫：[http://ooxx.me/connection-information.orz](http://ooxx.me/connection-information.orz "http://ooxx.me/connection-information.orz")