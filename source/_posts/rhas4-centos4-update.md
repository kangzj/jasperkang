---
title: RHAS4利用CentOS4的源进行升级
tags:
  - centos4
  - rhas4
  - update
id: 42
categories:
  - Systems&amp;Servers
date: 2008-10-17 09:00:05
---

**<span style="color: #ff0000;">已经失效.</span>**

可能是因为版权的关系,网上已经找不到可用的rhel的apt和yum源了.centos是一个根据rhel rebuild的版本,它的目录结构,文件命名,所有软件包都跟rhel是完全兼容的,因此,我们完全可以用centos的apt和yum源来进行系统和软件更新。

<!--more-->Apt下载：[http://rpm.pbone.net/index.php3/stat/4/idpl/1985014/com/apt-0.5.15cnc6-4.centos4.i386.rpm.html](http://rpm.pbone.net/index.php3/stat/4/idpl/1985014/com/apt-0.5.15cnc6-4.centos4.i386.rpm.html)
下载完以后用rpm -i apt-0.5.15cnc6-4.centos4.i386.rpm 进行安装
其实这时就可以用了,不过为了使更新更快,我们最好编辑一下下面这个文件
/etc/apt/sources.list.d/centos.list
修改其中的apt源为centos的中国镜像CODE:
### CentOS-4 APT repository
rpm http://mirror.be10.com centos/4/apt/i386 os addons updates extras
rpm http://mirror.be10.com centos/4/apt/i386 contrib centosplus [separator]

然后更新apt文件列表
apt-get update
升级所有文件
apt-get upgrade
也可以用下面命令来安装软件
apt-get install packagename
用apt可以升级我们大多数的软件,但要升级内核还需要用yum
先安装yum
apt-get install yum
这个时候需要导入一个GPG-KEY
rpm –import /usr/share/rhn/RPM-GPG-KEY
现在网上的文章出现了一个失误，还要修改一下/etc/yum.repos.d/CentOS-Base.repo
才可以yum升级，把/etc/yum.repos.d/CentOS-Base.repo的内容替换为：CODE:
[base]
name=CentOS-4 - Base
baseurl=http://mirror.be10.com/centos/4/os/i386/
gpgcheck=1
#released updates
[update]
name=CentOS-4 - Updates
baseurl=http://mirror.be10.com/centos/4/updates/i386/
gpgcheck=1
#packages used/produced in the build but not released
[addons]
name=CentOS-4 - Addons
baseurl=http://mirror.be10.com/centos/4/addons/i386/
gpgcheck=1
#additional packages that may be useful
[extras]
name=CentOS-4 - Extras
baseurl=http://mirror.be10.com/centos/4/extras/i386/
gpgcheck=1
#additional packages that extend functionality of existing packages
[centosplus]
name=CentOS-4 - Plus
baseurl=http://mirror.be10.com/centos/4/centosplus/i386/
gpgcheck=1
enabled=0
#contrib - packages by Centos Users
[contrib]
name=CentOS-4 - Contrib
baseurl=http://mirror.be10.com/centos/4/contrib/i386/
gpgcheck=1
enabled=0
#packages in testing
[testing]
name=CentOS-4 - Testing
baseurl=http://mirror.be10.com/centos/4/testing/i386/
gpgcheck=1
enabled=0

然后现在就可以进行升级了
yum update
yum升级完以后如果升级内核的话需要重新启动,使用
/sbin/shutdown -r now
重新启动以后再看看系统内核,已经是新版本的了
uname -a