---
title: php发送电子邮件
tags:
  - mail
  - php
  - php-email
  - sendmail
  - smtp
  - socket
id: 149
categories:
  - Web-Development
date: 2009-06-15 17:01:34
---

    配置php发送电子邮件(email)有两种方式：

    第一种是利用php中的mail函数。这里又分两种（[利用本机sendmail发送](http://kangzj.net/php-send-email-using-local/)，[利用smtp服务器发送](http://kangzj.net/php-send-email-using-remote-smtp/)），配置好了之后，操作就完全相同了，比如下面的php代码就发送了一封电子邮件：

<!--more-->

$to = "recipient@abc.com";
$subject = "Hello";
$body = "Hi,nnHow are you?";
if (mail($to, $subject, $body)) {
     echo("Message successfully sent!");
}
else {
     echo("Message delivery failed...");
}

    第二种是[利用php socket编程，连接smtp服务器，然后发送邮件](http://kangzj.net/php-socket-send-email-smtp/)。有一些开源的smtp的类可以用，我做的一个群发邮件的例子：[点击下载](http://blog.kangzj.net/wp-content/uploads/2009/06/email.rar) ，下面是其中关键部分（用了两种发送方式，可以选择smtp方式和mail函数的方式）：
<pre lang="php">//设置smtp服务器的相关信息----------------------------------------
$smtpserver         = "smtp.gmail.com"; //SMTP服务器
$smtpserverport = 25; //SMTP服务器端口
$smtpusermail     = "webmaster@gmail.com"; //SMTP服务器的用户邮箱
$smtpuser         = "webmaster"; //SMTP服务器的用户帐号
$smtppass         = "000000"; //SMTP服务器的用户密码
$mailtype='HTML';
//////////////////////////----------------------------------------

//设置群发的密码，这里是一个字符 y
if($_POST['password']!='y'){
	exit('Incorrect Password, Access Denied!');
}
//设置邮件列表和文件正文上传的路径
$uploaddir = '/usr/local/ygbweb/htdocs/xq100/';
$uploadfile = $uploaddir . 'maillist.txt';
//上传邮件列表，文本格式，压缩包里有实例
if (move_uploaded_file($_FILES['maillist']['tmp_name'], $uploadfile)) {
    echo "Maillist is valid, and was successfully uploaded.n
";
	flush();
} else {
    echo "Possible file upload attack!n";
	exit(0);
}
//html格式的邮件正文
$uploadfile = $uploaddir . 'message.html';

if (move_uploaded_file($_FILES['message']['tmp_name'], $uploadfile)) {
    echo "Message is valid, and was successfully uploaded.n
";
	flush();
} else {
    echo "Possible file upload attack!n";
	exit(0);
}

$lines=file("maillist.txt");

//loop through array using foreach
$method=$_POST['method'];
$subject=$_POST['subject'];
$message = file_get_contents($uploaddir . 'message.html');

//包含smtp类
require_once "smtp.class.php";

$smtp = new smtp($smtpserver, $smtpserverport, true, $smtpuser, $smtppass);
//这里面的一个true是表示使用身份验证,否则不使用身份验证.
$smtp-&gt;debug = true;
//是否显示发送的调试信息

foreach($lines as $line_num =&gt; $line)
{
	if($method=='direct'){
		xqmail($line, $subject, $message);
	}elseif($method=='smtp'){

		$smtp-&gt;sendmail($line, $smtpusermail, $subject, $message, $mailtype);
	}

}

function xqmail($to, $subject, $message){
//$to      = '';
//$subject = 'the subject';
//$message = 'hello';
$headers = 'From: webmaster@xinqing100.net' . "rn" .
    'Reply-To: xinqing100@bnu.edu.cn' . "rn" .
	'Content-type: text/html; charset=gb2312' . "rn";
if(mail($to, $subject, $message, $headers)){
		echo "$to 发送成功
";
}

}</pre>