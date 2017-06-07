---
title: WordPress插件制作(二)
tags:
  - php
  - wordpress
  - wordpress插件制作
  - 插件
  - 插件制作
id: 534
categories:
  - Blogging
date: 2009-07-27 14:20:25
---

### 3\. 开始编程实现你的插件

上面把流程交待得很清楚了，下面该让你的插件做点事情了。这一部分包含一些插件开发的基本的原则，教给你如何让你的插件完成几个不同的任务。

#### 3.1 WordPress插件钩子

很多插件通过连接一个或多个WordPress钩子来完成自己的功能。插件钩子工作的原理是，在WordPress运行的某些时刻，它会去检查是不是有插件注册了函数，如果有的话，就会运行这个插件的函数。这些函数改变了WordPress默认的功能。

<!--more-->

比如说，在WordPress输出页面的title之前，它会先检查一个是不是有插件注册了“the_title”的**“filter”钩子**。如果有的话，title的文本就会通过一个个的函数处理，最后再输出结果。所以，如果你的插件想改变title的话，注册一个“the_title”的filter钩子就可以了。

另外一种是**“action”钩子**，比如“wp_footer”。在HTML页面快要执行完的时候它会检查是不是有插件注册了“wp_footer”的“action”钩子，如果有的话，就一个一个地执行。

你可以在[Plugin API](http://codex.wordpress.org/Plugin_API)中找到更多的这种“filter”和“action”类型的钩子。如果你想在WordPress中的某一部分使用钩子，你也可以向开发者建议添加一个这样的钩子。

#### 3.2 模板标记

另外一种利用插件增强WordPress功能的方式是创建模板标记。使用你插件的人可以把这些标记加入到WordPress的模板里，可能放在sidebar等合适的地方。比如，一个地理位置的插件，定义一个放在sidebar里的geotag_list_states()，可以列所有这篇文章相关的“州”，点击这些“州”的时候，所有相关的文章会被列出来。

要定义一个模板标记，只要写一个PHP函数和文档，然后放在插件的主PHP文件中或者你插件的主页上举例一个例子说明应该往模板里加什么东西，怎样加，并在代码前后加上&lt;?php  ?&gt;。

#### 3.3 把插件的数据保存到数据库

大部分的WordPress插件需要保存一些数据，这些数据可以保存在WordPress的数据库里，这里有两种基本的、把插件数据保存到WordPress数据库的方法：

1.用WordPress的“option”机制（下面会详述）。这种方法可以保存较少量的、分散的数据，是那种一开始让用户输入的选项形式的，以后基本不会变的数据。

2\. Post Meta。对和单独文章、页面、附件相关的数据比较合适。可以查看：[post_meta函数示例](http://codex.wordpress.org/Function_Reference/post_meta_Function_Examples)。

3\. 新建一个数据表。这种方式适用于那些和文章、页面、评论等相关的数据，它们会随时间推移而增长。可以看一下这里“[用插件创制数据表](http://codex.wordpress.org/Creating_Tables_with_Plugins)”。

#### 3.4 WordPress的option机制

点击这里可查看怎么[创建可以自动地帮助你把插件的配制信息保存的插件管理面板](http://codex.wordpress.org/Creating_Options_Pages)。

WordPress有一套在数据库中保存、更改、读取独立的、有名字的数据（"options"）的机制。option的值可以是string, array或者php对象（在存储前会被序列化，或者转化成string）。option的名字是string类型，必须唯一，这样才能不和其它的WordPress插件冲突。

下面是你的插件调用WordPress需要用到了的主要的函数：

<pre lang="php">add_option($name, $value, $deprecated, $autoload);</pre>

"no"$name和$value当然就是你的option的名字和值啦；

$deprecated可选，WordPress已经不用了，可以传一个空值。

$autoload也是可选（'yes' or '），默认为yes，即会被<tt>get_alloptions函数自动加载。</tt>

<pre lang="php">get_option($option);</pre>

<tt>从数据库中读取$option的值。</tt>

<pre lang="php">update_option($option_name, $newvalue);</pre>

<tt>这个就不用解释了。</tt>

#### 3.5 插件设置页面

这部分将在以后文章中详述。

### 4. 国际化你的插件

做好了你的插件之后，你就可以考虑国际化了，让更多的人可以使用这个插件。在软件安装中，这叫做本地化，也就是把软件中使用的语言翻译成不同的语言。这里有相关的内容：[I18n for WordPress Developers](http://codex.wordpress.org/I18n_for_WordPress_Developers "I18n for WordPress Developers")。

### 5\. 插件开发建议

1.  WordPress的插件应该遵循“WordPress Coding Stardards”。也要考虑程序中的注释的标准。
2.  你插件中的函数名不能和WordPress核心的函数或者其它WordPress插件的函数有重名。可以通过给你的函数加一个前缀，也可以在类中定义你的函数来解决这个问题。
3.  代码中不要把WordPress前缀写死成“wp_”，要写成$wpdb-&gt;prefix。
4.  读数据库成本低，但是写却很高。所以尽量减少向数据写东西的次数。
5.  只“Select”你需要的字段。不要用“Select *”这样的语句，不要让你的插件把整个WordPress拖慢。
6.  把你插件中所有的错误修正，把PHP的Debug打开，在wp_config.php中添加<tt>define('WP_DEBUG', true)，找出所有的error和warning，并修改之。</tt>
<tt>本文翻译自：http://codex.wordpress.org/Writing_a_Plugin</tt>

<tt>PS: [ABitNo会做插件，让他教教你做插件:-)](http://abitno.linpie.com/abitno-wordpress-plugin.html)</tt>