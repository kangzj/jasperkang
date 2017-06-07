---
title: '配置nginx支持php,jsp,asp,aspx…'
tags:
  - nginx
  - 反向代理
id: 697
categories:
  - Systems&amp;Servers
date: 2009-08-15 08:36:45
---

说到Nginx，大家应该比较熟悉了吧，虽然出现地比较晚，但是他优良的性能让很多系统工程师折服，并被大量的采用。网上有好多文章介绍如何如何让nginx支持jsp啊、asp啊等等。我想说这个讲法是不太对的，因为nginx本身只是个静态的server和反向代理的利器，并不支持动态页面，所谓的支持asp,jsp,php等等都只是用nginx来做反向代理而已。

<!--more-->

[让nginx通过fastcgi支持php](http://kangzj.net/nginx_php_fastcgi_ubuntu/)已经介绍过了，这里仅介绍让nginx反向代理tomcat等jsp容器来serve jsp页面的方法：

假设你已经配置了tomcat并跑在本机的8080端口，打开你的虚拟机配置文件，加下下列几行：
> location / {
> proxy_pass  http://127.0.0.1:8080;
> proxy_redirect off;
> proxy_set_header Host $host;
> proxy_set_header X-Real-IP $remote_addr;
> proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
> client_max_body_size 10m;
> client_body_buffer_size 128k;
> proxy_connect_timeout 30;
> proxy_send_timeout 30;
> proxy_read_timeout 30;
> proxy_buffer_size 4k;
> proxy_buffers 4 32k;
> proxy_busy_buffers_size 64k;
> proxy_temp_file_write_size 64k;       
> }
OK啦，jsp可以跑了！想径向代理IIS?apache?——尽管去做吧！

PS：现在官方已经推出Windows版本的Nginx，所以支持Asp或者.net就完全是水到渠成了，可以直接在一台机器上做了，不用完全依赖mono了。