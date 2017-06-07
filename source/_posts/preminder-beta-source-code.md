---
title: Preminder Beta后台程序源码
tags:
  - google
  - pagerank
  - php
  - php-cli
  - php-email
  - pr
  - preminder
id: 929
categories:
  - Web-Development
date: 2009-09-11 16:06:54
---

[Preminder](http://apps.kangzj.net/preminder/) Beta后台程序源码，用PHP-CLI写的（[什么是PHP-CLI?](http://kangzj.net/php-cli/)）加了些注释，大家可以看一下。最有意思就是HashURL时的$SEED，其实获取PR是不符合Google的服务条款的，很汗的吧……

写好脚本之后，在/etc/crontab里加入一条每小时执行的计划，就可以啦，[在这里可以看到PR检测日志](http://apps.kangzj.net/preminder/list.php)！
> 27 *    * * *   root    /usr/bin/php -f /home/kangzj/kang.php
<!--more-->
数据库的结构为：
> --
> -- 表的结构 logs
> --
> 
> CREATE TABLE logs (
>   ID int(11) NOT NULL auto_increment,
>   info varchar(150) NOT NULL,
>   utime bigint(11) NOT NULL,
>   PRIMARY KEY  (ID)
> ) ENGINE=InnoDB DEFAULT CHARSET=utf8 ;
> 
> --
> -- 表的结构 users
> --
> 
> CREATE TABLE users (
>   ID int(11) NOT NULL auto_increment,
>   email varchar(50) NOT NULL,
>   domain varchar(100) NOT NULL,
>   pr tinyint(2) NOT NULL,
>   lastcheck timestamp NOT NULL default CURRENT_TIMESTAMP on update CURRENT_TIMESTAMP,
>   PRIMARY KEY  (ID)
> ) ENGINE=InnoDB DEFAULT CHARSET=utf8;

<pre lang="php">
< ?
//随机取5个PR低的域名进行检测，如果有PR变化则继续检测所有域名，否则退出程序
//测试集的大小
$testSetSize = 5;

//connect to mysql
$conn  = mysql_connect('localhost','preminder','111') or die('error');
mysql_select_db('preminder');

$result = mysql_query("select email, domain, pr from users where pr<=3  order by RAND() limit $testSetSize");

//计数
$i=0;
while($row = mysql_fetch_array($result))
{
	$nowpr = intval(pagerank($row['domain']));
	// $nowpr.' '.$row['pr'];
	if($nowpr != $row['pr']){
		break;
	}
	$i++;
	sleep(1);
}

if($i == $testSetSize){
             //写日志
	mysql_query("INSERT OR REPLACE into logs (utime, info) values ('".time()."','No pr updates detected!')");
            //没有更新退出程序
	exit;//no updates
}

//and there's pr update
$up=0;
$down=0;
$same=0;
$logs="domaintfromtton";
$result = mysql_query('select email, domain, pr from users');

while($row = mysql_fetch_array($result))
{
        $nowpr = intval(pagerank($row['domain']));
	$email = $row['email'];
	$domain = $row['domain'];
	$pr = $row['pr'];
	if($nowpr != $pr)
	        mysql_query("update users set pr='$nowpr' where email='$email' and domain='$domain'");
 	$subject = '您的'.$domain.'的PR由'.$pr.'更新为'.$nowpr;
	$message = '亲爱的'.$email.',

&nbsp;&nbsp;您的域名'.$domain.'的pr由'.$pr.'更新为'.$nowpr;
	$headers = $headers = "MIME-Version: 1.0rnContent-type: text/html; rn    charset="utf-8"rn".'From: noreply@kangzj.net' . "rn" .
	    'Reply-To: kangzj@kangzj.net' . "rn" .
	    'X-Mailer: PHP/' . phpversion();
	if($nowpr>$pr)
	{
		$up++;
		$message.=',恭喜！';
	}elseif($nowpr< $pr)
	{
		$down++;
		$message.=',降低了...';
	}else
	{
		$same++;
		$message.=',没有变化哦。';
	}
	$message.='

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[http://kangzj.net](http://kangzj.net)敬上
';
	mail($email, $subject, $message, $headers);
	$logs .= "$domaint$prt$nowprtn";

	sleep(1);
}
$fname = './'.date("Y-m-d-H-i-s", time()).'.log';
//写文件更新日志，含所有域名PR变化情况
file_put_contents($fname, $logs);

//更新日志
mysql_query("INSERT OR REPLACE into logs (info, utime) values ('$up domains PR rose, $down domains PR dropped, $same domains PR remained the same.','" .time()."')");

//检测PR函数
/*
*encode the url
*/
function HashURL($url)
{$SEED = "Mining PageRank is AGAINST GOOGLE'S TERMS OF SERVICE. Yes, I'm talking to you, scammer.";
    $Result = 0x01020345;
    for ($i=0; $i<strlen ($url); $i++)
    {
        $Result ^= ord($SEED{$i%87}) ^ ord($url{$i});
        $Result = (($Result >> 23) & 0x1FF) | $Result < < 9;
    }
    return sprintf("8%x", $Result);
}

/*
*get pagerank
*/
function pagerank($domain)
{
	$StartURL = "http://www.google.com/search?client=navclient-auto&googleip=0;973&ie=UTF-8&oe=UTF-8&features=Rank&q=info:";

 	$GoogleURL = $StartURL.$domain. '&ch='.HashURL($domain);

	$fcontents = file_get_contents("$GoogleURL");

	$pagerank = substr($fcontents,9);
	return intval($pagerank);
}

?></strlen></pre>