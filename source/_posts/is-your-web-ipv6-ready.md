---
title: 你的网站“IPv6 Ready”了吗？
tags:
  - he
  - Hurricane Electronics
  - ipv6
  - IPv6 Ready
  - IPv6 Tunnel Broker
  - nginx
id: 1631
categories:
  - Systems&amp;Servers
date: 2010-01-22 16:58:23
---

本文写给在用VPS的同学，即使你的VPS提供商并不支持IPv6，你可以将你网站做成IPv6 Ready！如果你的读者中的不少在教育网，做下这个就十分值得了，因为教育网没有国际连线，但是有免费的IPv6。如果你的VPS服务商支持IPv6那你可以直接从第5步看起，如果不支持，那就请从头看起。**<span style="color: #0000ff;">目前只在Diahosting的VPS上实验成功（独立服务器当然也没有问题，至于个人电脑，必须有公网IP地址的才行；因为需要内核支持IPv6和tun/tap，所以可能部分Xen、OpenVZ的不支持）</span>**。准备好了吗，Let’s begin!

### 1\. 基本原理

虽然你的VPS不支持IPv6，但是我们可以通过IPv6 Tunnel来解决，也就是平时说的IPv6 Over IPv4，可以理解成在IPv4上建立的IPv6的小管道。我们使用的是HE（Hurricane Electronics）提供的免费的IPv6 Tunnel Broker，HE拥有世界是最大的IPv6骨干网，在世界各地都有提供IPv6 Tunnel Broker的服务。

### 2\. 注册免费的HE IPv6 Tunnel Broker

注册地址：[http://tunnelbroker.net/](http://tunnelbroker.net/ "http://tunnelbroker.net/")，点击“Register”即可注册，注册流程很简单，就不多讲了。<!--more-->

### 3\. 添加Tunnel

点击左侧“Create Regular Tunnel”：

[![image](http://blog.kangzj.net/wp-content/uploads/2010/01/image_thumb.png "image")](http://blog.kangzj.net/wp-content/uploads/2010/01/image.png)

在“IPv4 endpoint”填入你VPS的IP地址，HE会根据你的浏览器的IP地址帮你选择服务器，但并不一定是最好的，你要根据你的**VPS的地理位置**，选择服务器的地址，我的是美国西部的VPS，于是我选择了Fremont, CA, US的服务器，点击“Override”可选择服务器。

[![image](http://blog.kangzj.net/wp-content/uploads/2010/01/image_thumb1.png "image")](http://blog.kangzj.net/wp-content/uploads/2010/01/image1.png)

再点击“Submit”，即可建立Tunnel成功。

### 4\. VPS上的设置

回到HE IPv6 Tunnel Broker的首页，点击刚刚建立的Tunnel，会有这个Tunnel的详细信息：

[![image](http://blog.kangzj.net/wp-content/uploads/2010/01/image_thumb2.png "image")](http://blog.kangzj.net/wp-content/uploads/2010/01/image2.png)

可以看到，HE给你分配了/64的IPv6地址，也就是你有2的64次方个地址，这辈子都用不完，哈哈。在详细信息的下面，有一个设置你VPS的方法，点击“Show Config”就会出来设置方法：

[![image](http://blog.kangzj.net/wp-content/uploads/2010/01/image_thumb3.png "image")](http://blog.kangzj.net/wp-content/uploads/2010/01/image3.png)

把这些命令在你的VPS上执行下。测试下看设置成功没，ping6 he.net，如果跟下图差不多，就说明配置成功：

[![image](http://blog.kangzj.net/wp-content/uploads/2010/01/image_thumb4.png "image")](http://blog.kangzj.net/wp-content/uploads/2010/01/image4.png)

行啦，你的VPS也支持IPv6啦！

### 5\. 让的网站IPv6 Ready

做完这些还不行，还得让你的HTTP服务器支持IPv6。Apache 2.0版本开始支持IPv6，Nginx从0.7.36之后开始支持IPv6。我们只讲Nginx的配置方法，其他可以自己摸索。

我的VPS上装的是lnmp一键安装包：[http://lnmp.org/](http://lnmp.org/ "http://lnmp.org/") ，下面讲解中安装路径就以lnmp中安装路径为准。

重新编译Nginx使之支持IPv6。不详细说了，晒下命令，最关键的一句是“--with-ipv6”：
<pre lang="bash">wget http://nginx.org/download/nginx-0.8.32.tar.gz
tar –xvzf nginx-0.8.32.tar.gz
cd nginx-0.8.32
./configure --user=www --group=www --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module --with-ipv6
make && make install
</pre>
在终端执行ifconfig，可以看到你的IPv6地址：

[![](http://blog.kangzj.net/wp-content/uploads/2010/01/ipv6-addr-300x83.jpg "ipv6-addr")](http://blog.kangzj.net/wp-content/uploads/2010/01/ipv6-addr.jpg)

把你虚拟机配置文件中_listen 80;_全部替换为_listen ip:80;_的形式，否则启动不了。再在你想支持IPv6的虚拟机里加一句_listen [ipv6]:80_，配置好之后，大体如下图所示：
<pre lang="bash">server {
listen       216.45.55.20:80;
listen       [2001:470:1f04:873::2]:80;
server_name kangzj.net;

………………
}
</pre>
安装配置完毕。停掉旧nginx，启动新编译的nginx：
<pre lang="bash">killall nginx
/usr/local/nginx/sbin/nginx
</pre>

### 6\. 增加IPv6地址的DNS AAAA记录

这个需要你的DNS支持AAAA记录，也就是IPv6记录。现在基本所有的域名注册商的DNS都支持了，如果不支持，你可以使用dnspod的服务，是免费的，而且支持AAAA记录。

我的是Name.com的域名，本身就支持，就不麻烦了。加好之后，域名会有两条记录，一条A的，一条AAAA的：

[![image](http://blog.kangzj.net/wp-content/uploads/2010/01/image_thumb5.png "image")](http://blog.kangzj.net/wp-content/uploads/2010/01/image5.png)

搞掂，等生效吧。生效之后，如果用户网络支持IPv6的话，就会访问IPv6地址。如果只有IPv4网络就会访问IPv4的地址啦！

### 7\. 后记

原来以为只有Native的IPv6才能提供网络服务，我错了，走Tunnel的也可以。这下子VPS商支不支持IPv6无所谓了，我们可以自己解决，DIY万岁！