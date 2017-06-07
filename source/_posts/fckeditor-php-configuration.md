---
title: FCKEditor 2.x在php环境下的配置
tags:
  - fckeditor
  - php
id: 30
categories:
  - Web-Development
date: 2007-11-20 01:04:00
---

来源：未知

下载地址:
http://www.fckeditor.net/download
效果演示:
http://www.fckeditor.net/demo

<!--more-->

一:修改文件上传语言为PHP    
    打开fckconfig.js    
    找到:
    var _FileBrowserLanguage = 'asp'
    var _QuickUploadLanguage = 'asp'    
    改成:
    var _FileBrowserLanguage = 'php'
    var _QuickUploadLanguage = 'php'

二:启用PHP文件上传

    1:启用FileBrowser:
        打开fckeditor/editor/filemanager/browser/default/connectors/php/config.php
        启用文件上传:

        找到:
        $Config['Enabled'] = false

        改成:
        $Config['Enabled'] = true

        设置上传存放目录:

        找到:
        $Config['UserFilesPath'] = '/userfiles/'
        改成:
        $Config['UserFilesPath'] = '你自己的项目路径'

    2:启用QuickUpload
        打开fckeditor/editor/filemanager/upload/php/config.php
        启用文件上传:

        找到:
        $Config['Enabled'] = false
        改成:
        $Config['Enabled'] = true

        设置上传存放目录:

        找到:
        $Config['UserFilesPath'] = '/userfiles/'
        改成:
        $Config['UserFilesPath'] = '你自己的项目路径'

实例：
        &lt;?php
$fck = $_POST["FCKeditor1"];
if ($fck != "")
{
echo htmlspecialchars($fck);
}
?&gt;

&lt;html&gt;
&lt;head&gt;
&lt;title&gt;fck测试&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;form action="index.php" method="POST"&gt;
&lt;?php
include("fckeditor/fckeditor.php") ; //加载文件
$oFCKeditor = new FCKeditor('FCKeditor1') ; //创建一个FCKeditor对象 ID为FCKeditor1
$oFCKeditor-&gt;BasePath = "/fck/fckeditor/" ; //设置FCKeditor路径
$oFCKeditor-&gt;Value = '' ; //设置默认值
$oFCKeditor-&gt;Create() ; //创建
?&gt;
&lt;input type="submit" value="提交"&gt;
&lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;