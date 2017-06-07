---
title: 在GAE上用二级域名托管Feed
tags:
  - '302'
  - feed
  - feedburner
  - FeedSky
  - gae
  - google
  - google app engine
  - google apps
  - python
  - redirect
id: 1159
categories:
  - Web-Development
date: 2009-10-17 03:30:13
---

前面介绍过怎样不被Feed托管商绑死，[在Feedburner和FeedSky之间来回换而不损失订户的方法](http://kangzj.net/move-from-feedsky-to-feedburner/)。由于Feedburner不支持二级域名绑定，我用一个虚拟机来给feed域名做302重定向到托管在Feedburner的地址，但是这个主机在国外，教育网上不方便。于是想把feed子域名停放在GAE上，再做302重定向。

上传程序和绑定域名的方法不赘述，参考下面三篇文章即可：

> 大蜘蛛：[Google App Engine (GAE)注册与部署](http://www.allengao.com/blog/register-gae-google-app-engine-apply.html)
> 
> 徐明：[Google App Engine 入门:上传应用程序](http://xuming.net/2008/05/google-app-engine-toturial-9.html)
> 
> 无名氏：[Google企业应用套件最新最全申请攻略](http://outwindowsxp.blog.sohu.com/90535925.html)

**需要注意的是**，申请Google Apps的时候直接绑定你的根域即可，不要绑定二级域名，因为现在Google Apps已经不支持绑定裸域了，即使本来就是二级域名。举例：绑定kangzj.net，而不要绑定feed.kangzj.net 。

[打包下载](http://kangzj.net/wp-content/uploads/rars/200910/redirecting.zip)

下面附上代码：
<!--more-->
<pre lang="python">
import cgi
import wsgiref.handlers

from google.appengine.ext import webapp

class MainPage(webapp.RequestHandler):
  def get(self):
    self.redirect('http://feeds.feedburner.com/kangzjnet')

application = webapp.WSGIApplication([
  ('/', MainPage),
], debug=False)

def main():
  wsgiref.handlers.CGIHandler().run(application)

if __name__ == '__main__':
  main()

</pre>