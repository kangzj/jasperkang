---
title: 日本CentOS 5升级源
tags:
  - centos
  - linux
  - vps
  - yum
id: 1900
categories:
  - Systems&amp;Servers
date: 2012-01-16 15:34:01
---

VPS.net的日本服务器IP是归属是美国，故yum的fast mirror功能没法用，升级速度巨慢，于是找了个日本CentOS 5镜像，速度不错。<!--more-->

# CentOS-Base.repo
#
# The mirror system uses the connecting IP address of the client and the
# update status of each mirror to pick mirrors that are updated to and
# geographically close to the client.  You should use this for CentOS updates
# unless you are manually picking other mirrors.
#
# If the mirrorlist= does not work for you, as a fall back you can try the
# remarked out baseurl= line instead.
#
#

[base]
name=CentOS-$releasever - Base
baseurl=[http://ftp.tsukuba.wide.ad.jp/Linux/centos/](http://ftp.tsukuba.wide.ad.jp/Linux/centos/)$releasever/os/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5

#released updates
[updates]
name=CentOS-$releasever - Updates
baseurl=[http://ftp.tsukuba.wide.ad.jp/Linux/centos/](http://ftp.tsukuba.wide.ad.jp/Linux/centos/)$releasever/updates/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5

#additional packages that may be useful
[extras]
name=CentOS-$releasever - Extras
baseurl=[http://ftp.tsukuba.wide.ad.jp/Linux/centos/](http://ftp.tsukuba.wide.ad.jp/Linux/centos/)$releasever/extras/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5

#additional packages that extend functionality of existing packages
[centosplus]
name=CentOS-$releasever - Plus
baseurl=[http://ftp.tsukuba.wide.ad.jp/Linux/centos/](http://ftp.tsukuba.wide.ad.jp/Linux/centos/)$releasever/centosplus/$basearch/
gpgcheck=1
enabled=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5

#contrib - packages by Centos Users
[contrib]
name=CentOS-$releasever - Contrib
baseurl=[http://ftp.tsukuba.wide.ad.jp/Linux/centos/](http://ftp.tsukuba.wide.ad.jp/Linux/centos/)$releasever/contrib/$basearch/
gpgcheck=1
enabled=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5
<pre></pre>