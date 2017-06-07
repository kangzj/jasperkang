---
title: WordPress插件制作(一)
tags:
  - php
  - wordpress
  - wordpress插件制作
  - 插件
  - 插件制作
id: 473
categories:
  - Blogging
date: 2009-07-26 22:06:33
---

### 1\. 简介

WordPress插件使得WordPress变得扩展性强、易修改和个性化。不用修改WordPress的核心，你只要简单的加几个插件，很多功能就能够轻松实现。下面给出WordPress插件的定义：

**WordPress插件**：它是用PHP编写的一个程序或一个或者几个函数的组合，它利用WordPress提供的API和WordPress本身的一些调用点，给WordPress增加新的功能或者特性。

希望WordPress有新功能的或者想修改一下功它的某个功能？你所要做的第一件事就是从WordPress大量的插件中寻找，有没有人已经制作过这样的插件，如果有，直接用就好了。如果没有，这篇文章可以指导你做你自己的WordPress插件。
<!--more-->
_这篇文章假设你对WordPress的工作方式和PHP编程比较了解了。_

### 2\. 创建一个新的插件

这一部分会把插件制作的步骤都涉及到了，你只要跟着做就好了，同时也告诉你创建一个新的插件时应该考虑的东西。

#### 2.1 插件名、文件和文件存放的位置

##### 2.1.1 插件名

做插件的第一步当然是考虑清楚你的插件的功能，给你的插件起个名字。到WordPress官方网站和其它资源查找下有没有相同的名字，当然你也可以Google一下，以保证你的插件的名字是唯一的。很多插件的开发者以插件的功能给插件命名。比如说，一个跟“天气”相关的插件很有可能起一个含有"Weather"的名字。名字可由多个单词组成。

##### 2.2.2 插件的文件

下一步就是创建插件的PHP文件。例如，你的插件名字是“Fabulous Functionality”，你可以给你的PHP文件起一个名字“fabfunc.php”。和插件的名字一个道理，这个PHP文件也要起一个唯一的名字。用你插件的人会把你的文件放到plugin目录里，也就是/wp-content/plugins/，所以任何两个插件的PHP文件都不能有相同的名字，否则会引起冲突和误会。

上面是你的插件只有一个文件的情况。你也可以把你的PHP文件拆分成多个文件。你的WordPress插件应该至少含有一个PHP文件，也可以有JavaScript，Css，图像，语言等文件。如果有多个文件，就把他们全都放到一个目录下面，这个目录的名字也要是唯一的。告诉你的插件的使用者，把整个文件夹上传到/wp-content/plugins/就可以了。

_下面所提到的“插件的PHP文件”是指插件的主要的PHP文件，有可能在/wp-content/plugins/中，也有可以在这里面的一个子目录中。_

##### 2.2.3 Readme文件

如果你想把你的插件上传到[http://wordpress.org/extend/plugins/](http://wordpress.org/extend/plugins/)中，你应该按标准的格式创建一个Readme文件，放到你的插件文件中。这里介绍Readme文件的格式：[http://wordpress.org/extend/plugins/about/readme.txt](http://wordpress.org/extend/plugins/about/readme.txt "http://wordpress.org/extend/plugins/about/readme.txt")

#### 2.2 插件主页

为你的插件创建一个主页是很有用处的，你可以在这个主页上介绍如何安装你的插件，插件的功能，插件兼容的WordPress的版本，插件不同版本之间功能的变化，怎么使用插件等等。

#### 2.3 PHP文件的文件头信息

现在到了写点东西到你插件的PHP文件中的时候了。

##### 2.3.1 标准的插件信息头

你插件的主要的PHP文件的头部，必须写上**标准的插件信息**。这个插件信息头让WordPress找到你的插件，并把你的插件加入到插件管理中去，这样这个插件才能被激活、加载和运行。没有这个插件信息头，你的插件就不会被识别，也完全不会起任何作用。下面是插件信息头的格式：
<pre lang="php">
< ?php
/*
Plugin Name: Name Of The Plugin
Plugin URI: http://URI_Of_Page_Describing_Plugin_and_Updates
Description: A brief description of the Plugin.
Version: The Plugin's Version Number, e.g.: 1.0
Author: Name Of The Plugin Author
Author URI: http://URI_Of_The_Plugin_Author
*/
?></pre>
这些信息中，如果不写“Plugin Name”WordPress就无法识别插件。其它的几项信息在插件管理的页面会有显示。信息的顺序是没有要求的。

##### 2.3.2 授权信息

通常大家就直接用标准的授权信息当作自己的授权信息。很多的插件用得就是GPL。加入下面的文字，可以简要的说明GPL：
<pre lang="php">< ?php
/*  Copyright YEAR  PLUGIN_AUTHOR_NAME  (email : PLUGIN AUTHOR EMAIL)

    This program is free software; you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation; either version 2 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program; if not, write to the Free Software
    Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA
*/
?></pre>

### 3\. 编程实现你的插件

现在到了让你的插件做点实事的时候了。这部分包含一些开发当中的基本的常识，阐明了要完成你的插件应该做的几项工作。 

[继续阅读 =&gt;  WordPress插件制作(二) ](http://kangzj.net/wordpress-plugin-tutorial-2/)