---
title: Fckeditor上传文件自动改名-php配置(可以解决Fckeditor上传中文文件名出错的问题)
tags:
  - fckeditor
  - php
  - 上传中文文件名图片
  - 中文文件名
  - 自动改名
id: 192
categories:
  - Web-Development
date: 2009-06-17 14:31:01
---

Fckeditor 2.4不支持插入中文文件名的图片，但是是可以上传的，但是，上传之后却不能浏览服务器了，会产生[The server didn't send back a proper XML response](http://kangzj.net/fckeditor-not-proper-response/)的错误。怎么解决呢，其实很简单，只要将上传的文件自动改名就行了啊，中文的文件名不建议用。下面是修改Fckeditor的方法：
<!--more-->
找到FCKeditor/editor/filemanager/upload/php/upload.php文件：
1\. 找到:
> while ( true )
> 
> 在前面添加：
> 
> $rFileName = time() . '.' . $sExtension; //即是用当前的时间来代替文件名
2.找到：
> $sFilePath = $sServerDir . $sFileName ;
> 
> 修改成：
> 
> $sFilePath = $sServerDir . $rFileName ;
3.找到：
> $sFileUrl = $Config["UserFilesPath"] . strtolower($sType) . '/' . $sFileName ;
> 
> 把其中的$sFileName改成$rFileName
4.找到：
> $sFileUrl = $Config["UserFilesPath"] . $sFileName
> 
> 把其中的$sFileName改成$rFileName
好了，成功了，现在你的Fckeditor可以上传中文文件名的图片或者其它文件啦，下面是效果：

[gallery link="file"]