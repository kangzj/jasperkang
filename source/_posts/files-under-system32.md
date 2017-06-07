---
title: System32下几乎所有文件的作用
tags:
  - system32
id: 20
categories:
  - Software
date: 2007-12-27 10:43:22
---

aclui.dll .....Security Descrīptor Editor，没有它，注册表编缉器会无法运行
ACTIVEDS.DLL .....(ADs 路由层 DLL). 没有它, 打开事件查看器会出错
ADSLDPC.DLL ......ADs LDAP 提供程序 C DLL
ADVAPI32.DLL .....(高级 Windows 32 基本 API)...这个 avicap32.dll 用于将从数码摄像头捕获的视频另存为 AVI 格式. 如果你正在录制视频或是正在视频聊天, 那么你将服务终止这个进程

<!--more-->
ADVPACK.DLL ......(Advpack Library). Windows 用它来验证 .inf 文件. 如果 advpack.dll 不可用, windows 将无法正常工作. (没有它, 打开系统属性会出错.)
ASYCFILT.DLL ....我所安装的一个程序 StatBar, 需要这个文件
ATL.DLL .......... Windows XP ATL 模块 (Unicode)
AUTHZ.DLL ........认证框架
BASESRV.DLL ......Windows NT BASE API Server DLL [separator]
BATMETER.DLL .....(电池助手 DLL). 打开电源选项需要这个文件
bootvid.dll .....VGA 启动驱动
BROWSELC.DLL .....外壳浏览器用户界面库
browser.dll .....Computer Browser Service DLL
BROWSEUI.DLL ..... 外壳浏览器用户界面库
browsewm.dll ...BrowseWM Player
CABINET.DLL ......(Microsoft® Cab 文件 API). 想要正常打开系统选项就要保留这个文件
CALC.EXE .......(计算器). Windows 自带的计算器程序
CFGMGR32.DLL ...配置管理转发器 DLL，没有它，无法在资源管理器中对磁盘进行格式化
clb.dll .....Column List Box，没有它，注册表编缉器会无法运行
CMD.EXE ....(命令行).可提供 Windows NT 下的命令行提示符 (MS-DOS 外壳解释程序)
comcat.dll .....Microsoft C 运行时库文件
COMCTL32.DLL .....通用控件库
COMDLG32.DLL .....通用对话框 DLL
console.dll ....控制面板控制台小程序
control.exe ....Windows 控制面板 (这个不是实际上的控制面板.)
CONVERT.EXE ....(转换). 用于将分区格式从 FAT 转为 NTFS 以及从 NTFSv4 转为 NTFSv5
CREDUI.DLL .......授权证书管理程序用户界面
crtdll.dll .....加密管理器
CRYPT32.DLL ......32 位加密 API
CRYPTDLL.DLL .....加密管理程序
CRYPTUI.DLL ......Microsoft 加密用户界面提供程序
CSRSRV.DLL .......客户端服务器运行时进程
CSRSS.EXE ........(客户端-服务器运行时服务器子系统). 用于维护Win32 系统环境控制台以及其它基本功能.
desk.cpl ......显示属性
deskmon.dll .... 高级显示监视器属性
devenum.dll ....设备枚举
devmgr.dll .....设备管理器 MMC 管理工具
diskcopy.dll ...Windows DiskCopy
dmintf.dll ..... 磁盘管理 DCOM 接口存根
dmutil.dll ..... 逻辑磁盘管理器工具库
DNSAPI.DLL .......DNS 客户端 API DLL
fmifs.dll ......FM IFS 工具 DLL
framebuf.dll ...帧缓冲显示驱动
GDI32.DLL ........GDI 客户端 DLL（含有XCMD设置字体的函数）
hal.dll ........(硬件抽象层). 隐藏 Windows 应用程序处理硬件问题的复杂性（启动之后可删除的文件）
hccoin.dll .....USB 协同安装程序
hotplug.dll ....用于安全移除硬件, 比如, U 盘
icaapi.dll ..... TermDD 设备驱动的 DLL 接口
ifsutil.dll ....IFS 工具 DLL
IMAGEHLP.DLL .....Windows NT 图像助手（IE显示图像需要）
imm32.dll ........(Windows XP IMM32 API 客户端 DLL). 用于正常打开系统属性
inetmib1.dll ...Microsoft MIB-II subagent
input.dll ......(文本输入 DLL). 语言和区域设置需要这个文件来显示相关对话框
IPHLPAPI.DLL .....IP 助手API
iyuv_32.dll ....Intel Indeo(R) Video YUV Codec (文件版本: 5.1.2600.2180)
kbdus.dll .....美国键盘布局
kdcom.dll .......内核调试程序硬件扩展 DLL（启动之后可删除的文件）
KERBEROS.DLL .....Kerberos 安全包
kernel32.dll .....Windows NT BASE API 客户端 DLL
LINKINFO.DLL .....Windows 卷目追踪
lpk.dll ........会话注销工具
LSASRV.DLL .......LSA 服务器 DLL
LSASS.EXE ........(LSA 安全服务). 本地安全认证服务器进程
main.cpl ......鼠标
MFC42.DLL ......MFCDLL 共享库
mfc42u.dll .....MFCDLL 共享库
MPR.DLL ..........多个提供程序路由 DLL
MPRAPI.DLL .......(Windows NT MP 路由管理DLL)
mprui.dll .......多个提供程序
MSASN1.DLL .......ASN.1 运行时 API
mscat32.dll ....MSCAT32 Forwarder DLL
mscms.dll ........(Microsoft 色彩匹配系统 DLL). 这个模块中包含了一些用于校正图像色彩,以及用于色彩映射, 色彩管理的函数
MSCTF.DLL ......MSCTF 服务器 DLL
msftedit.dll ..RTF 文本编辑控件, v4.1
MSGINA.DLL .......Windows NT 登录 GINA DLL
msh263.drv ....Microsoft H.263 ICM 驱动
msidntld.dll ...Microsoft 标识管理器
MSIMG32.DLL ......GDIEXT 客户端 DLL
MSIMTF.DLL .....Active IMM 服务器 DLL
msls31.dll .......(Microsoft 线性服务库文件). Internet Explorer 需要这个文件
msports.dll ....端口类别安装程序
MSPRIVS.DLL ......Microsoft 特权转换
msrle32.dll ....Microsoft RLE 压缩器
mssign32.dll ...Microsoft 受信赖签证 APIs
mssip32.dll ....MSSIP32 Forwarder DLL
msvcirt.dll ....Windows NT IOStreams DLL
MSVCP60.DLL ......Microsoft (R) C++ 运行时库文件
msvcrt40.dll ...VC 4.x CRT DLL (向后兼容 msvcrt.dll)
MSVCRT.DLL .......Windows NT CRT DLL
msvfw32.dll ...Microsoft Video for Windows DLL
msvidc32.dll ...Microsoft Video 1 压缩器
mydocs.dll .....我的文档文件夹用户界面
ncxpnt.dll .....Netork (不是 Network) 安装向导支持 DLL
NDDEAPI.DLL ......Network DDE 共享管理 APIs
NET1.EXE .......(Network). 与 NET.EXE 的功能相同(在使用net命令的时候需要调用net1,若不存在就无法完成操作)
NET.EXE ........(Network). 用于管理, 配置和查看与网络相关的信息, 例如 net use, net print, net user, 等等
NETAPI32.DLL .....Net Win32 API DLL
netrap.dll .....网络远程管理协议DLL
netui0.dll .....NT LM UI Common Code - GUI Classes (文件版本: 5.1.2600.2180)
netui1.dll .....NT LM UI Common Code - GUI Classes (文件版本: 5.1.2600.2180)
newdev.dll ....添加硬件设备库文件
NOTEPAD.EXE ......(记事本). 文本编辑工具
NTDLL.DLL ........NT Layer DLL
NTDSAPI.DLL ......(NT5DS Library) Windows 的目录服务需要这个ntdsapi.dll 库文件. 目录服务可令 Windows 能够更容易地定位设备以及网络上的资源
ntlanman.dll ...Microsoft® 局域网管理器
ntlsapi.dll ....Microsoft® 许可服务器接口 DLL
NTMARTA.DLL ......Windows NT MARTA 提供程序
NTOSKRNL.EXE ..(操作系统内核). Windows XP 操作系统内核, 启动画面就在这个文件中
ocmanage.dll ..可选组件管理库
ODBC32.DLL .......Microsoft Data Access - ODBC 驱动管理器
ODBCBCP.DLL ......(Microsoft BCP for ODBC). 没有这个文件的话, 当你打开电脑管理时会遇到一个错误. 但还是可以打开电脑管理. (我把电脑管理删掉了.)
ODBCINT.DLL ......Microsoft Data Access - ODBC 资源
OLE32.DLL ........Microsoft OLE for Windows
oleacc.dll .......(Active Accessibility 核心组件)
OLEAUT32.DLL ..... Windows 要用它执行OLE (对象链接和嵌入) 操作. OLE 允许将程序创建的对象嵌入到另一个程序的文档或对象中. 例如. 将一个 Excel 表格嵌入到 Word 文档中. Windows 应用程序要经常用到OLE, 因此一般你是无法将其删除的
OLECLI32.DLL ..... 对象链接和嵌入客户端库文件
OLECNV32.DLL .....Microsoft OLE for Windows
oledlg.dll .......(Microsoft Windows(TM) OLE 2.0 用户接口支持)
OLESVR32.DLL ..... 对象链接和嵌入服务器库
OLETHK32.DLL .....Microsoft OLE for Windows
perfctrs.dll ...性能计数器
powercfg.cpl ..电源选项
POWRPROF.DLL .....(电源配置助手 DLL). 如要正常打开设备管理器中的键盘属性, 需要保留这个文件
PROFMAP.DLL ......Userenv
PSAPI.DLL ........进程状态助手
pstorec.dll ..... 受保护存储的COM 接口
pstorsvc.dll .... 受保护存储服务器
REG.EXE ........(注册表控制台). 一个用于查询和修改注册表的命令行工具
REGAPI.DLL .......注册表配置 APIs
REGSVR32.EXE ...(注册服务器). 用于注册组件, DLL
riched20.dll ...RTF 编辑控件, v3.0 字符编辑器相关文件,Winrar查看功能缺该文件的话,显示空白;Restorator,QQ游戏需要
riched32.dll...字符编辑器相关文件
rnr20.dll ......Windows Socket2 命名空间 DLL
RPCRT4.DLL .......远程过程调用运行时
RPCSS.DLL ........分布式 COM 服务
RSAENH.DLL .......Microsoft 增强加密提供程序
rshx32.dll ....安全外壳扩展
rtipxmib.dll ...Microsoft Router IPX MIB subagent
RTUTILS.DLL ......路由工具
RUNDLL32.EXE ...(Run DLL). 用于运行 DLL 文件的命令行工具
RUNONCE.EXE ....(Run Once). 用于将要执行的任务添加定义到 RunOnce 注册表项中
SAMLIB.DLL .......SAM 库DLL
SAMSRV.DLL .......SAM 服务器 DLL
SCESRV.DLL .......Windows安全配置编辑器引擎
SCHANNEL.DLL .....TLS / SSL 安全提供程序
SECUR32.DLL ......安全支持提供程序接口
security.dll ...安全支持提供程序接口
services.exe .....(安全和控制程序). Windows XP 用它管理服务
SETUP.EXE ......(Setup). Windows 安装程序
SETUPAPI.DLL .....Windows Setup API
SFC.DLL ..........Windows 文件保护
SFC_OS.DLL .......Windows 文件保护
sfcfiles.dll .....Windows 2000 系统文件检查工具
SHDOCVW.DLL ...... 外壳文档对象和控件库
SHELL32.DLL ......Windows 外壳通用 Dll
shellstyle.dll ..Windows 外壳样式资源Dll
SHFOLDER.DLL .....(外壳文件夹服务). 若要正常打开系统属性, 需要保留此文件
shgina.dll .....Windows 外壳用户登录 &lt;-- 这个文件用于从你的桌面上重启电脑. 进一步讲, 一旦你将其删除或是将其从 system32 文件夹中移走, 那么即使你将其放回, 也照样无法从你的桌面重新启动
shimgvw.dll ......(Windows 图片和传真查看器). 我要用它看电脑上的图片
SHLWAPI.DLL ......外壳 Light-weight 工具库
sigtab.dll .....文件完整性设置(系统属性--&gt;硬件--&gt;驱动程序签名选项的对话框)
SMSS.EXE .........(会话管理器). 是个会话管理器, 用于在启动期间创建Windows XP 环境
snmpapi.dll ....SNMP 工具库
softpub.dll ....Softpub Forwarder DLL
softpub.dll ....Softpub Forwarder DLL
STOBJECT.DLL .....(Systray 外壳服务对象). stobject.dll 是个库文件, 包含了一些像是图标这样的资源 托盘音量图标 电池图标
[HKEY_LOCAL_MACHINESOFTWAREMicrosoftWindowsCurrentVersionShellServiceObjectDelayLoad]
"SysTray"="{35CEC8A3-2BE6-11D2-8773-92E220524153}"
[HKEY_CLASSES_ROOTCLSID{35CEC8A3-2BE6-11D2-8773-92E220524153}InProcServer32]
@=" stobject.dll"
由Explorer读取并加载

streamci.dll ... 流设备类别安装程序
SVCHOST.EXE ...... Win32 服务的常规宿主进程
SXS.DLL ..........Fusion 2.5
sysdm.cpl .....系统属性
SYSTRAY.EXE ....(系统栏). 系统栏提供程序. 它能控制任务栏和系统栏. 但是, 没它的话, 也没有什么不正常的地方
TASKMGR.EXE ...(任务管理器). 平时使用的任务管理器
themeui.dll ......Windows 主题 API
timedate.cpl ..时间和日期
ufat.dll .......FAT 工具 DLL
ULIB.DLL .......文件工具支持 DLL
umdmxfrm.dll .....Unimodem 转换模块
umpnpmgr.dll .....用户模式即插即用服务
untfs.dll ......NTFS 工具 DLL
ureg.dll .......注册表工具 DLL
urlmon.dll ....... Win32 OLE32 扩展
usbui.dll ...USB 用户界面 Dll
user32.dll .......Windows XP 用户 API 客户端 DLL
userenv.dll ......用户环境
USERINIT.EXE ..(用户初始化). 在用户登录之后, 用于确定操作系统的环境
usp10.dll .....Uniscribe Unicode 脚本处理器
UXTHEME.DLL ......Microsoft UxTheme Library
VERSION.DLL ......版本检查和文件安装库
vga64k.dll .....32K/64K 色 VGASVGA 显示驱动
vga.dll .....VGA 16 色显示驱动
w32topl.dll ....Windows NT Topology 维护工具
WDIGEST.DLL ......Microsoft 采集访问
WIN32K.SYS .......多用户 Win32 驱动
WININET.DLL ......Internet 扩展
winipsec.dll ....Windows IPSec SPD Client DLL
WINLOGON.EXE .....Windows NT 登录应用程序
WINMM.DLL ........MCI API DLL
WINRNR.DLL .......LDAP RnR 提供程序 DLL
WINSPOOL.DRV ...Windows 缓冲池驱动
WINSRV.DLL .......Windows Server DLL
WINSTA.DLL .......工作站库文件
WINTRUST.DLL .....Microsoft 受信赖证书 APIs
WLDAP32.DLL ......Win32 LDAP API DLL
WMI.DLL ..........(WMI DC 和 DP 功能). 若要正常打开电脑管理, 则需要保留此文件
WS2_32.DLL .......Windows Socket 2.0 32 位 DLL
WS2HELP.DLL ......Windows Socket 2.0 助手
wshnetbs.dll ...Netbios Windows套接层助手DLL
WSOCK32.DLL ......(Windows 32 位套接层 DLL). 某些涉及到网络的软件会需要它
WTSAPI32.DLL .....Windows 终端服务器 SDK API
netid.dll -----(系统属性--&gt;计算机名)
fontview.exe －－字体查看器
fontext.dll －－与字体文件夹视图安装字体有关