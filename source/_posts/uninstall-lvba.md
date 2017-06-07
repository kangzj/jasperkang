---
title: 卸载/删除“绿坝-花季护航”
tags:
  - 卸载删除绿坝
  - 绿坝
  - 绿坝花季护航
id: 88
categories:
  - Software
date: 2009-06-11 11:11:08
---

    装上之后找卸载找了半天，愣是没有找到。后来发现，卸载选项在系统设置-&gt;日常维护-&gt;密码和卸载里面。当然，要进入到这里是需要输入密码的。怎么样才能不输入密码就卸载，下面有两种方法：

（1）在北邮人上看到的简单翻过绿坝的方法：
绿坝用了类似病毒的技术，至少三个进程相互守望着……
重命名以下文件，然后重启计算机，貌似绿坝就没啥效果了。
---------
C:WINDOWSMPSvcC.exe_
C:WINDOWSsystem32XNet2.exe_
C:WINDOWSsystem32XDaemon.exe_
C:WINDOWSsystem32FImage.dll_
C:WINDOWSsystem32IPGate.dll_
C:WINDOWSsystem32xcore.dll_
C:WINDOWSsystem32Xcv.dll_
C:WINDOWSsystem32Xtool.dll_
C:WINDOWSsystem32kwpwf.dll_
C:WINDOWSsystem32winet.dll_

（2）绿坝将密码用MD5算法转换后，以文本方式保存在system32目录下的kwpwf.dll文件中。以记事本打开该文件，以“D0970714757783E6CF17B26FB8E2298F”替换其内容后保存，即可将密码恢复为初始密码“112233”。就可以修改设置或者卸载/删除绿坝了。

参考文献：
1\. [http://zhh.pp.ru/?p=306](http://zhh.pp.ru/?p=306) 
2\. 绿坝-花季护航软件技术分析： [https://docs.google.com/View?id=afk7vnz54wt_12f8jzj9gw](https://docs.google.com/View?id=afk7vnz54wt_12f8jzj9gw)