---
title: Squid 2.6反向代理加速
tags:
  - linux
  - squid
  - 反向代理
id: 47
categories:
  - Systems&amp;Servers
date: 2008-11-05 02:07:26
---

Squid系一个Linux专有超级反向代理正向代理+Web缓存软件.
好多大网站例如 163 shou 新浪....都会想全国各个服务器节点置立尼一个机制。
例如,北京用户访问163\. 首先会通过DNS轮询找到最近既服务器.然后读取内容。
而这一部服务器上的内容,会定时自动由广州既总服务器复制.就是这个系统会预先将网页内容
缓存下来.
<!--more-->

### 第一步安装

建议还是用 tar.gz 包装吧...RPM 的东西会烦死你.特别是找配置文件的时候.

#tar zxvf squid-2.6.STABLE4.tar.gz
#cd squid-2.6.STABLE4
#./configure --prefix=/usr/local/squid
#make
#make install

安装是很简单的.但接下类配就有点烦了.(跟我当年用tar装MySQl一样烦)

### 第二步配置

其实最关键就在配置上,要配置存放缓存的目录,PID文件的目录,log日志的目录
还要设置缓存大小...

#vi /usr/local/squid/etc/squid.conf

---------------------squid.conf------------------------
http_port 192.168.1.30:80 vhost vport
icp_port 0

#服务器IP 192.168.1.30
#监听服务器的80端口，透明代理，支持域名和IP的虚拟主机
#http_port 192.168.1.30:80 transparent vhost vport
#最新2.6使用http_port 192.168.1.30:80 vhost vport

#防止天涯盗链，转嫁给百度
#acl tianya referer_regex -i tianya
#http_access deny tianya
#deny_info http://www.baidu.com/logs.gif tianya

#防止被人利用为HTTP代理，设置允许访问的IP地址
#acl myip dst 192.168.1.1
#http_access deny !myip

#防止百度机器人爬死服务器
#acl AntiBaidu req_header User-Agent Baiduspider
#http_access deny AntiBaidu

#允许本地管理
#acl Manager proto cache_object
#acl Localhost src 127.0.0.1 192.168.1.1
#http_access allow Manager Localhost
#http_access deny Manager

#仅仅允许80端口的代理
#acl Safe_ports port 80 # http
#http_access deny !Safe_ports
#http_access allow all

#Squid信息设置
visible_hostname squid
cache_mgr AAAA@admin.com

#限制同一IP客户端的最大连接数
acl OverConnLimit maxconn 16
http_access deny OverConnLimit

#基本设置
cache_vary on
cache_mem 256 MB
#占用的物理内存大小
cache_dir ufs /data/squid/cache 10000 16 256
#硬盘上cache空间的路径(目录需要自己手动建)
cache_effective_user squid
cache_effective_group squid
tcp_recv_bufsize 65535 bytes

#2.6的反向代理加速配置(虚拟服务器)
#代理到本机的80端口的服务，仅仅做为原始内容服务器
#配置虚拟服务器的指向是最我这次研究Squid花时间最长的地方.所以也是本文的重点

cache_peer www.gznow.cn parent 80 0 no-query originserver login=PASS
cache_peer 59.42.255.86 parent 80 0 no-query originserver login=PASS

#上边这2行的意思,是概括地把所有请求指向另外一台服务器的IP。(域名跟IP都可以)
#而详细哪个域名指向哪个IP呢.就要在下边这2行中补充了.这里尤为重要.上下2部分缺一不可。
#如果启动时出现错误 No cache_peer 'xx.xxx.xx.xxx' 就证明是你上边跟下边的服务器地址没有对应上了。

cache_peer_domain www.gznow.cn blog.gznow.cn
cache_peer_domain 59.42.255.88 bbs.cdfeel.com

# 1,意思是.把 blog.gznow.cn 这个域名的请求反向链接到 www.gznow.cn(他会解析成ip地址) 的服务器上.
# 2,意思根上边一样.把 bbs.cdfeel.com 这个域名反向链接到 59.42.255.88 这台服务器上。
#就是说服务器的地址.可以是域名也可以是IP.

#如果你的虚拟主机有用户名和密码保护起来的目录必须设置login=PASS，否则认证会失效
#error_directory /data/squid/errors/Simplify_Chinese
emulate_httpd_log on
#打开emulate_httpd_log选项,将使Squid仿照Aapche的日志格式
logformat combined %&gt;a %ui %un [%tl] "%rm %ru HTTP/%rv" %Hs %#日志格式combined的设置(目录需要自己手动建)
pid_filename /data/squid/pid/squid.pid
cache_log /data/squid/log/cache.log
access_log /data/squid/log/null combined
#这里是设置pid和日志文件的位置，因人而异，同时日志格式是combined，awstats可以直接调用分析了
acl all src 0.0.0.0/0.0.0.0

acl QUERY urlpath_regex cgi-bin .php .cgi .avi .wmv .rm .ram .mpg .mpeg .zip .exe
cache deny QUERY
#设置不想缓存的目录或者文件类型

refresh_pattern -i . 1440 50% 10080 override-expire override-lastmod reload-into-ims ignore-reload ignore-no-cache ignore-private

acl picurl url_regex -i .bmp$ .png$ .jpg$ .gif$ .jpeg$ .js$ .css$ .htm$ .html$ .xml$

#acl mystie1 referer_regex -i aaa
#http_access allow mystie1 picurl

#no_cache allow picurl
#http_access allow picurl
#设置防图片盗链的，其中aaa,和bbb分别是虚拟主机的域名，referer中必须包含有aaa或者bbb的域名才能访问图片
#acl nullref referer_regex -i ^$
#http_access allow nullref
#acl hasref referer_regex -i .+
#http_access deny hasref picurl
#设置允许直接访问图片和拒绝referer中没有包含aaa或着bbb的访问图片

-------------------end------------------------

自己把上边这东西覆盖原来的conf也可以运行了.(就是http_port 的ip改改)

第三步,初始化+运行

首先就是要按照上边 conf 配置中的 cache 路径建 目录.并且赐予其777 权限 跟把用户属组调至 "squid"这简单的步骤我就不详写了.用mkdir 跟 chmod 777 chown squid

cache_dir ufs /data/squid/cache
#硬盘上cache空间的路径

目录建好之后,使用 squid -z 命令初始化目录,建缓存.
#/usr/local/squid/sbin/squid -z

然后就可以开始运行了.有好几个运行参数

#/usr/local/squid/sbin/squid --NCd1 (前台正式运行,用于调试非常好.)
#/usr/local/squid/sbin/squid        (后台运行)
# /usr/local/squid/sbin/squid -k reconfig (更新配置文件后更新)

然后,自己建立一个 squid 执行脚本放在 /etc/rc.d/init.d 里边(记得要赐予运行权限哦)

然后用Linux自带的工具检测一下Http头看Cache生效没
#curl -I http://192.168.1.30/
如信息中出现有以下这一行就代表缓存生效了。
X-Cache: HIT from squid
如果是
X-Cache: MISS from squid
就代表缓存还没储存,或者是没生效.

--------------------squid---------------------

#!/bin/sh
# if ! PREFIX=$(expr $0 : "(/.*)/etc/rc.d/$(basename $0)$"); then
# ..echo "$0: Cannot determine the PREFIX" &gt;&amp;2

# ..exit 1

# fi

case "$1" in

start)
if [ -x /usr/local/squid/sbin/squid -a -f /usr/local/squid/etc/squid.conf ]; then
(cd /usr/local/squid/var/logs; /usr/local/squid/sbin/squid &gt;/dev/null 2&gt;&amp;1 &amp;) ; echo -n ' squid'

fi

;;

stop)

/usr/local/squid/sbin/squid -k shutdown 2&gt;&amp;1

# Uncomment this if you'd like the system to (attempt to

# wait for) squid to shut down cleanly

#echo "Sleeping for 45 seconds to allow squid to shutdown.."

#sleep 45

;;

*)

echo "Usage: basename $0 {start|stop}" &gt;&amp;2

;;

esac

exit 0

----------------------end-------------------------

PS: 上个星期还试了一下最新的 squid 3.0 出了个怪问题.

配置文件在 2.6 上完全正确的,虽然移到 3.0 上有个别参数不兼容.但能启动.

不过就只能发挥 proxy 功能, cache 就死活不肯生效。
用 curl -I 命令...测了N遍缓存都还是 MISS.

上网看了很多 Squid 的配置详解.http://www.visolve.com/squid/squid30/contents.php

改了好几次配置,都还是不行.

最后还是高手刘冬出马...
原来是我建给 squid 用于做 cache 的目录权限有错.
尽管我把自己建的目录 /data/squid/cache 权限设成了 777 但因为他属主还是 root
而我在 squid 上设置的运行属主是 "squid" .所以导致了 squid 拿不到缓存了.
怪啊怪...因为之前我在 2.6 上也同样是 777 的, 都没这个问题..3.0 恐怕是安全方面设严了.