---
title: linux下用yum给php安装gd库
tags:
  - gd2
  - linux
  - php
id: 38
categories:
  - Systems&amp;Servers
date: 2008-10-07 04:02:55
---

[root@localhost ~]# yum install php-gd*
Setting up Install Process
Setting up repositories
base                      100% |=========================|  951 B    00:00
update                    100% |=========================|  951 B    00:00
<!--more-->

Reading repository metadata in from local files
Parsing package install arguments
Resolving Dependencies
--&gt; Populating transaction set with selected packages. Please wait.
---&gt; Downloading header for php-gd to pack into transaction set.
php-gd-4.3.9-3.22.9.i386\. 100% |=========================|  20 kB    00:00
---&gt; Package php-gd.i386 0:4.3.9-3.22.9 set to be updated
--&gt; Running transaction check
--&gt; Processing Dependency: php = 4.3.9-3.22.9 for package: php-gd
--&gt; Restarting Dependency Resolution with new changes.
--&gt; Populating transaction set with selected packages. Please wait.
---&gt; Downloading header for php to pack into transaction set.
php-4.3.9-3.22.9.i386.rpm 100% |=========================|  24 kB    00:00
---&gt; Package php.i386 0:4.3.9-3.22.9 set to be updated
--&gt; Running transaction check
--&gt; Processing Dependency: php = 4.3.9-3.22.5 for package: php-mysql
--&gt; Processing Dependency: php = 4.3.9-3.22.5 for package: php-ldap
--&gt; Processing Dependency: php = 4.3.9-3.22.5 for package: php-pear
--&gt; Restarting Dependency Resolution with new changes.
--&gt; Populating transaction set with selected packages. Please wait.
---&gt; Downloading header for php-pear to pack into transaction set.
php-pear-4.3.9-3.22.9.i38 100% |=========================|  34 kB    00:00
---&gt; Package php-pear.i386 0:4.3.9-3.22.9 set to be updated
---&gt; Downloading header for php-mysql to pack into transaction set.
php-mysql-4.3.9-3.22.9.i3 100% |=========================|  20 kB    00:00
---&gt; Package php-mysql.i386 0:4.3.9-3.22.9 set to be updated
---&gt; Downloading header for php-ldap to pack into transaction set.
php-ldap-4.3.9-3.22.9.i38 100% |=========================|  20 kB    00:00
---&gt; Package php-ldap.i386 0:4.3.9-3.22.9 set to be updated
--&gt; Running transaction check

Dependencies Resolved

=============================================================================
Package                 Arch       Version          Repository        Size
=============================================================================
Installing:
php-gd                  i386       4.3.9-3.22.9     update             99 k
Updating for dependencies:
php                     i386       4.3.9-3.22.9     update            1.3 M
php-ldap                i386       4.3.9-3.22.9     update             35 k
php-mysql               i386       4.3.9-3.22.9     update             36 k
php-pear                i386       4.3.9-3.22.9     update            268 k

Transaction Summary
=============================================================================
Install      1 Package(s)
Update       4 Package(s)
Remove       0 Package(s)
Total download size: 1.7 M
Is this ok [y/N]: y
Downloading Packages:
(1/5): php-pear-4.3.9-3.2 100% |=========================| 268 kB    00:00
(2/5): php-mysql-4.3.9-3\. 100% |=========================|  36 kB    00:00
(3/5): php-gd-4.3.9-3.22\. 100% |=========================|  99 kB    00:00
(4/5): php-4.3.9-3.22.9.i 100% |=========================| 1.3 MB    00:01
(5/5): php-ldap-4.3.9-3.2 100% |=========================|  35 kB    00:00
Running Transaction Test
Finished Transaction Test
Transaction Test Succeeded
Running Transaction
  Updating  : php-ldap                     ######################### [1/9]
  Updating  : php-mysql                    ######################### [2/9]
  Updating  : php-pear                     ######################### [3/9]
  Updating  : php                          ######################### [4/9]
  Installing: php-gd                                                 [5/9]warning: /etc/php.d/gd.ini created as /etc/php.d/gd.ini.rpmnew
  Installing: php-gd                       ######################### [5/9]
  Cleanup   : php-pear                     ######################### [6/9]
  Cleanup   : php-mysql                    ######################### [7/9]
  Cleanup   : php                          ######################### [8/9]
  Cleanup   : php-ldap                     ######################### [9/9]

Installed: php-gd.i386 0:4.3.9-3.22.9
Dependency Updated: php.i386 0:4.3.9-3.22.9 php-ldap.i386 0:4.3.9-3.22.9 php-mysql.i386 0:4.3.9-3.22.9 php-pear.i386 0:4.3.9-3.22.9
Complete!