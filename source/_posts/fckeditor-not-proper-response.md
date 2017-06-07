---
title: 'FCKEditor: The server didn''t send back a proper XML response解决方法'
tags:
  - fckeditor
  - php
id: 80
categories:
  - Web-Development
date: 2009-05-06 06:29:43
---

> The server didn't send back a proper XML response. Please contact your system administrator.
> 
> XML request error: OK (200)
所有配置均正确，而会有上面这样的错误。是因为不支持浏览中文文件名导致，解决方法：<!--more-->
将FCKEditor设置的Upload目录下面的中文文件全部删掉，OK，解决了！

    可以让用户不要上传中文文件名的文件，或者稍微修改一下fckeditor的源文件使上传的文件自动改名就可以解决了，[修改FCKeditor/editor/filemanager/upload/php/upload.php](http://kangzj.net.ru/php-fckeditor-upload-file-change-name/)即可，[详细请看这里](http://kangzj.net.ru/php-fckeditor-upload-file-change-name/)。