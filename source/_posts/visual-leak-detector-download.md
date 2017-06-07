---
title: Visual Leak Detector下载
tags:
  - cpp
  - vc
  - vc6
  - visual leak detector
  - vld
  - 内存泄露检测
id: 1149
categories:
  - Programming
date: 2009-10-16 03:30:55
---

> Visual Leak Detector (VLD) 1.9h (Beta)，点[这里](http://files.brothersoft.com/development/misc_web_development/vld-1.9h-setup.exe)开始下载！
Visual C++内置内存泄露检测工具，但是功能十分有限。VLD就相当强大，可以定位文件、行号，可以非常准确地找到内存泄漏的位置，而且还**免费、开源**！

在使用的时候只要将VLD的头文件和lib文件放在工程文件中即可。

也可以一次设置，新工程就不用重新设置了。只介绍在Visual Studio 2003/2005中的设置方法，VC++ 6.0类似：

1.  打开Tools -&gt; Options -&gt; Projects and Solutions -&gt; VC++ Directories；
2.  然后点击include files下拉列表，在末尾把VLD安装目录中的include文件夹添加进来；
<!--more-->3.  同样点击lib下拉列表，把VLD的lib也添加进来；
4.  在需要检测内存泄漏的源文件中添加

<pre lang="cpp">#include “vld.h”</pre>顺序无所谓，但是一定不能在一些预编译的文件前（如stdafx.h）。我是加在stdafx.h文件最后。5.  把安装目录下dll文件夹中的所有dll文件拷贝到工程Debug目录，也就是Debug版.exe生成的位置。点击Debug –&gt; Start Debugging 调试程序，在OUTPUT窗口中就会显示程序运行过程中的内存泄漏的文件、行号还有内容了。
检测结果示例：

<pre lang="code">
---------- Block 2715024 at 0x04D8A368: 512 bytes ----------
  Call Stack:
    d:kangzjdocumentsvisual studio 2005projectsrsip.rootreadtiffreadtiffsegmentflag.cpp (56): CSegmentFlag::GetFlagFromArray
    d:kangzjdocumentsvisual studio 2005projectsrsip.rootreadtiffreadtiffwholeclassdlg.cpp (495): segmentThreadProc
    f:ddvctoolsvc7libsshipatlmfcsrcmfcthrdcore.cpp (109): _AfxThreadEntry
    f:ddvctoolscrt_bldself_x86crtsrcthreadex.c (348): _callthreadstartex
    f:ddvctoolscrt_bldself_x86crtsrcthreadex.c (331): _threadstartex
    0x7C80B729 (File and line number not available): GetModuleFileNameA
  Data:
    3C 3C 3C 3C    3C 3C 3C 3C    3C 3C 3C 45    45 45 45 45     < <<<<<<< <<<eeeee
    45 45 45 3C    3C 3C 3C 3C    3C 3C 3C 3C    3C 3C 3C 3C     EEE<<<<< <<<<<<<<
    3C 3C 3C 3C    3C 3C 45 45    45 45 45 45    45 45 45 45     <<<<<<ee EEEEEEEE
    3C 3C 3C 3C    3C 3C 3C 3C    3C 3C 3C 3C    3C 3C 3C 3C     <<<<<<<< <<<<<<<<
    3C 3C 3C 3B    3B 3B 3B 3B    3B 3B 3B 42    42 42 3B 3B     <<<;;;;; ;;;BBB;;
    3B 3B 3B 3B    3B 3B 3B 3B    3B 3B 3B 42    42 38 38 38     ;;;;;;;; ;;;BB888
    38 38 38 38    38 38 38 38    38 38 38 38    38 38 38 38     88888888 88888888
    38 38 38 38    38 38 38 38    38 38 3E 3E    3E 3E 3E 3E     88888888 88>>>>>>
    3E 3E 3E 3E    3E 3E 3E 3E    3E 3E 3E 3E    3E 3E 3E 3E     >>>>>>>> >>>>>>>>
    3E 3E 3E 3E    3E 38 38 38    38 2B 2B 2B    2B 12 12 12     >>>>>888 8++++...
    12 12 12 12    12 12 12 12    12 12 12 2B    2B 2B 2B 2B     ........ ...+++++
    2B 2B 2B 2B    2B 2B 2B 37    37 37 37 37    37 37 37 37     +++++++7 77777777
    37 37 37 37    37 37 37 37    37 37 37 37    37 37 37 37     77777777 77777777
    37 37 37 37    37 37 37 37    37 37 21 21    21 21 21 21     77777777 77!!!!!!
    29 29 29 29    3A 3A 3A 3A    3A 3A 3A 3A    3A 3A 3A 3A     )))):::: ::::::::
    3A 3A 3A 3A    3A 3A 3A 44    44 44 44 44    44 44 44 44     :::::::D DDDDDDDD
    41 41 41 41    44 44 44 44    44 44 44 44    44 44 41 41     AAAADDDD DDDDDDAA
    41 41 41 41    41 41 3D 3D    3D 3D 3D 3D    3D 3D 3D 3D     AAAAAA== ========
    3D 3D 3D 3D    3D 3D 3D 3D    3D 3D 3D 3D    3D 3D 3D 3D     ======== ========
    3D 3D 3D 3D    3D 3D 3D 3D    3D 3D 3D 3D    3D 3D 3D 3D     ======== ========
    3D 3D 3D 3D    3D 3D 29 29    29 29 29 29    35 35 35 35     ======)) ))))5555
    35 35 35 35    35 35 35 35    35 35 35 35    35 35 35 35     55555555 55555555
    35 35 35 35    35 35 35 35    35 35 35 35    35 35 29 29     55555555 555555))
    29 29 29 29    32 32 32 32    32 32 32 32    32 32 32 32     ))))2222 22222222
    32 32 32 32    32 32 32 32    32 32 32 43    43 32 32 32     22222222 222CC222
    43 43 43 43    43 43 43 43    43 43 43 43    43 43 43 43     CCCCCCCC CCCCCCCC
    43 43 43 43    43 43 43 43    43 43 43 43    43 43 43 43     CCCCCCCC CCCCCCCC
    3F 3F 3F 3F    3F 3F 3F 3F    3F 3F 3F 3F    3F 3F 3F 3F     ???????? ????????
    3F 3F 3F 3F    3F 3F 3F 1C    1C 1C 1C 1C    46 46 46 46     ???????. ....FFFF
    46 46 46 46    46 46 40 40    40 40 40 40    40 40 40 40     FFFFFF@@ @@@@@@@@
    40 40 40 40    40 40 40 46    46 40 40 40    40 40 40 40     @@@@@@@F F@@@@@@@
    40 40 40 40    40 40 40 40    40 40 40 40    40 40 40 40     @@@@@@@@ @@@@@@@@
</pre>

安装程序中有更详细的使用说明。