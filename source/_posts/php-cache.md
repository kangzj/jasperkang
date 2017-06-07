---
title: php cache类(php数据缓存类)
tags:
  - php
  - php_kcache_class
  - php-cache
  - php缓存类
  - 缓存
id: 214
categories:
  - Web-Development
date: 2009-06-23 22:36:48
---

    php的执行效率很高，速度很快，但是连接数据库、查询数据库等还是比较耗时的。如果访问量大的话会给数据库造成很大的负担，所以对于变化不经常的内容要做好php 数据cache(缓存)是十分必要的，我做了一个简单的php“文件缓存”的类，希望对大家有所帮助。
<!--more-->
    思路是这样的：

1.  对于一般的变量，把该变量变成php语言的格式，写到文件中，用时只要include这个文件就相当于加载了cache了；
2.  对于array型的变量，把array转化为php语言定义array的字符串，写到文件中，用时也只要include就相当于加载了cache了；
3.  缓存cache时间上的控制，通过获取缓存文件的创建时间和现在的时间进行对比，如果没有到更新时间，直接读取缓存，如果到了更新时间，查询数据库，返回数据，再更新缓存。(尚未实现)
下面是我的php-kcache类(php_kcache_class.php)：
<span style="color: #ff0000;">注：如果是缓存字符串，请把转义字符多写一个''，即"n"要写成"n"。</span>
<pre lang="php">/*
//php-kcache class v_0.1
//Author: kangzj
//Email : kangzj@mail.bnu.edu.cn
//Blog  : http://kangzj.net.ru
//作者不保证本程序没有bug，对于使用本程序
//而引起的任何问题不担负任何责任。
*/
class php_kcache {
	//相对或者绝对目录，末尾不要加 '/'
	var $cache_dir = './cache';
	var $cache_extension = '.cache.php';

	function set_cache($name, $value){
		$pre = "&lt; ?n//Cache Created at: ".date('Y-m-d H:i:s')."n";
		if(!is_array($value)){
			$value = $value;
			$str = "$$name = '$value';";
		}else{
			$str = "$$name = " . $this-&gt;arrayeval($value) . ';';
		}
		$end = "n?&gt;";
		echo $cache = $pre . $str . $end;
		$cache_file = $this-&gt;cache_dir . '/' . $name . $this-&gt;cache_extension;

		if($fp = @fopen($cache_file, 'wb')) {
			fwrite($fp, $cache);
			fclose($fp);
			return true;
		} else {
			echo $cache_file;
			exit('Can not write to cache files, please check cache directory ');
			return false;
		}
	}

	//将array变成字符串, 来自discuz!
	function arrayeval($array, $level = 0) {

		if(!is_array($array)) {
			return "'".$array."'";
		}

		$space = '';
		for($i = 0; $i &lt; = $level; $i++) {
			$space .= "t";
		}
		$evaluate = "Arrayn$space(n";
		$comma = $space;
		if(is_array($array)) {
			foreach($array as $key =&gt; $val) {
				$key = is_string($key) ? '''.addcslashes($key, ''').''' : $key;
				$val = !is_array($val) &amp;&amp; (!preg_match("/^-?[1-9]d*$/", $val) || strlen($val) &gt; 12) ? '''.addcslashes($val, ''').''' : $val;
				if(is_array($val)) {
					$evaluate .= "$comma$key =&gt; ".arrayeval($val, $level + 1);
				} else {
					$evaluate .= "$comma$key =&gt; $val";
				}
				$comma = ",n$space";
			}
		}
		$evaluate .= "n$space)";
		return $evaluate;
	}
}</pre>
最简单的调用方法：
<pre lang="php">include './php_kcache_class.php';
$pc = new php_kcache;
$a = array('a', 'b', 'c');
$pc-&gt;set_cache('a', addslashes($a));</pre>
复杂的调用方法(加上缓存时间控制的)——稍后补上....to be continued...