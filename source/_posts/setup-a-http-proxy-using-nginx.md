---
title: nginx架设http代理
tags:
  - hosts
  - linux
  - nginx
  - 代理
  - 反向代理
  - 正向代理
  - 透明代理
id: 968
categories:
  - Systems&amp;Servers
date: 2009-09-17 00:17:56
---

![](http://nginx.net/nginx.gif)

[squid透明代理](http://kangzj.net/squid-tranparent/)已经向大家介绍过了，前两天在[Libing](http://www.libing.name/)大哥的博客逛的时候发现原来也可以用[nginx来作透明代理](http://www.libing.name/2009/09/10/nginx-transparent-forward-proxy.html)（个人觉得叫正向代理更合理些），学习了下，又丰富了下，给大家分享一下。
> server {
> 
> listen 81;
> 
> location / {
> 
> proxy_pass http://$http_host$request_uri;
> 
> }
> 
> }
<!--more-->

步骤非常简单，只要新建一个主机，随便监听一个端口就可以，但是不能加主机名，因为我们是正向http代理，如果加了主机名，那岂不是就只能访问那几个网站了吗，呵呵。
> <span style="background-color: #ffffff;">$http_host - 主机名，即是访问该服务器的域名</span>
> 
> <span style="background-color: #ffffff;">$request_uri - 主机名后面跟的所有的东西</span>
> 
> <span style="background-color: #ffffff;"> </span>
> 
> <span style="background-color: #ffffff;">例如：[http://<span style="color: #0000ff;">www.kangzj.net</span><span style="color: #ff0000;">/preminder/</span>](http://www.kangzj.net/preminder/)</span><span style="color: #ff0000;"> </span><span style="color: #400000;">蓝色部分就是$http_host 红色部分就是$request_uri</span>
<span style="background-color: #ffffff;"> </span>

<span style="background-color: #ffffff;">然后怎样，不用我教了吧，打开IE选项设置代理即可利用代理上网啦！</span>

当然，如果你想**限制用户只能上某几个网站**，那么就加上：
> server_name www.163.com g.cn;
等等就可以啦，是不是很方便呢。

如果把代理端口设置成80就可以作为透明代理来使用了（严格来说并不是透明代理，反而更像反向代理）：

<span style="background-color: #ffffff;">但是需要我们修改无敌的hosts文件了，为什么？——因为我们要访问的网站的域名并不是指向我们的nginx服务器啊~OK改好，这样子，所有的网站就好像工作在那台nginx服务器似的，可以上啦！</span>

说到这里同学们可能会有点乱了，正向代理、反向代理、透明代理……最后再跟大家明确下：

1.  这三种方式的代理本质是相同的：都是代理服务器代理客户端到相应的互联网服务器取东西（浏览、下载等）。
2.  代理使用的方式是不同的：正向代理是在IE或者其它浏览器设置代理选项，浏览器向代理服务器请求所有网页，由代理服务器代理取回网页；透明代理跟正向代理原理一样，只不过主机将代理服务器当做网关使用，并不需要设置代理选项；而反向代理是为一个（或几个）网站架设的代理，网站好像就在代理服务器端似的，多用来给网站加速用（跟我上面讲的所谓透明代理是一个意思）。
不会越说越乱吧，呵呵，其实不用在定义上这么纠缠，在有用的时候想到有方法可以实现就可以了。

Nginx真的很好用、很强大，你不妨试一下:-)