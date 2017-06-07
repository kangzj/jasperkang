---
title: 利用php-imagick制作动态显IP论坛图片签名
tags:
  - php
  - php-imagick
  - php图像处理
  - 签名
id: 86
categories:
  - Web-Development
date: 2009-06-09 15:12:07
---

imagick是专门设计给php用的模块，虽说不如直接在命令行的效率高，但据说效率上比

gd2要快，并且可以做很多高级的操作，支持100+的图像类型，非常之强大，这里仅用它来显

示IP及来源，也就是往图片上“写字”，可以说是大材小用了。ip数据库请自行查找配置，只

要会点php应该就很容易改。如果不想显示ip的来源，只要把源码中的相应部分注释掉即可：<!--more-->

<span class="comment"><span style="color: #008200;">/*如果不显IP来源，注释开始</span></span>

*/

<span class="comment"><span style="color:#008200;">……………………
</span></span>

<span><span class="comment"><span style="color: #008200;">/*如果不显IP来源，注释结束*/</span></span><span> </span></span>

![picout](http://kangzj.net.ru/wp-content/uploads/2009/06/ac5041e8d77f634537ad9f543e88a3c2.png "picout")

<span><span>关于使用，这里也提一下吧，多数的论坛程序提供UBB的签名方式：</span></span><span><span>[img]http://x.x.x.x/sign.php[/img]就行了！</span></span>

<pre lang="php">//连接数据库，这里用的是discuz!的数据库类

//config.inc.php中存储了数据库的相关配置

/*如果不显IP来源，注释开始*/

include './config.inc.php';

include './db_mysql.class.php';

$db = new dbstuff;

$db-&gt;connect($dbhost, $dbuser, $dbpasswd, $dbname, 0, TRUE, $dbcharset);

//数据库的名字叫signpic，其中存了ip数据库

$db-&gt;select_db('signpic');

/*如果不显IP来源，注释结束*/

//字体文件的路径，我用的是微软雅黑

$font="./MSYHBD.TTF";

//用来当做背景的图片

$imgpath = 'chuanglian.png';

//图片上显示的文字

$word = '我就是显示IP而已,没有别的意思~';

//文字大小

$fontsize = 20;

//文字颜色，这个根据你的图片而定，不然看不到字了

$color = "black";

/*如果不显IP来源，注释开始*/

//获取用户的IP地址

$ip = $_SERVER['REMOTE_ADDR'];

//将IP地址转化为十进制，便于进入数据库查询

$iparray=explode('.',$ip);

$ipint=($iparray[0] * 256*256*256) + ($iparray[1]*256*256) + ($iparray[2]*256) +

$iparray[3];

//查数据库，得到IP的来源存在$from变量中

$sql = "select province, city, subcity from sp_ipaddress where $ipint&gt;start and

$ipintfetch_first($sql);

/*如果不显IP来源，注释结束*/

if($row=="")

{

    $from = "来源未知";

}else

{

//这是查出来的三个项，省，城市，县——这个根据你的IP数据库的情况自己确定

    $from = $row['province'].'.'.$row['city'].'.'.$row['subcity'];

}

//读取用户是什么浏览器

$useragent = $_SERVER["HTTP_USER_AGENT"];

//只识别两种MSIE和FirFox

if(stripos($useragent,"firefox")){

    $browser="FirFox";

}elseif(stripos($useragent,"MSIE")){

    $browser="MSIE";

}

//生成显示文字，包含IP，来源和加的话

$text = "你的IP: $ip 浏览器: $browsern来自: $fromn".$word;

//读入背景图片

$image = new Imagick( $imgpath  );

$image-&gt;setImageFormat( "png" );

//生成画笔

$draw = new ImagickDraw();

//设置对齐方式，这里是居中对齐

$draw-&gt;setGravity( Imagick::GRAVITY_CENTER );

//设置字体

$draw-&gt;setFont( $font );

//设置字体大小

$draw-&gt;setFontSize( $fontsize );

//设置文字颜色

$textColor = new ImagickPixel( $color );

$draw-&gt;setFillColor( $textColor );

//往图片上写文字

$image-&gt;annotateImage( $draw, 0, 0, 0, $text );

//输出最后的结果

//header来表明MIME

header( "Content-Type: image/png" );

echo $image;</pre>