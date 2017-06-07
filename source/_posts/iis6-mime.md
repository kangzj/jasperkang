---
title: MIME与IIS 6
tags:
  - iis6
  - mime
id: 22
categories:
  - Systems&amp;Servers
date: 2008-02-21 00:50:30
---

来源：未知

一、什么是MIME？
二、什么是MIME类型
三、解决win2003服务器不能下载iso exe rmvb等文件的问题
四、微软的帮助文档：[http://www.microsoft.com/china/TechNet/iis/mimeiis.asp](http://www.microsoft.com/china/TechNet/iis/mimeiis.asp)

<!--more-->

一、什么是MIME？
用户可以通过使用MIME以设置服务器传送多媒体如声音和动画信息，这一切可能通过CGI脚本来进行。在下面的文章中，你可以了解到一此关于MIME和关于在网络上使用MIME的知识。
MIME是一种技术规范，它原来是用于电子邮件的，现在也可以用于浏览器上，传送可以供浏览器识别的信息，关于MIME的知识并是十分难懂的，有一些基本的计算机概念就可以理解了，但如果要进一步使用，就必须注意内容。实际上，我们在上网的时候就已经接触到了MIME，只是浏览器和服务器在底层实现了。
MIME有时候被错误地理解为多媒体Internet邮件扩展（Multimedia Internet Mail Extensions），这是一个错误，但是MIME在网上经常用于多媒体应用程序，所以人们以为这是它是多媒体邮件扩展，而实际上它应该被称为多用途Internet邮件扩展（Multipurpose Internet Mail Extensions），这一点一定要注意，因为有时候内容里根本没有非文本成份。
MIME对于邮件系统的扩展是巨大的，因为在MIME出现以前，信件内容如果要包括声音和动画，就必须把它变为ASCII码或把二进制的信息变成可以传送的编码标准，而接收方必须经过解码才可以获得声音和图画信息。MIME提供了一种可以在邮件中附加多种不同编码文件的方法。这与原来的邮件是大大不同的。而现在MIME已经成为了HTTP协议标准的一个部分。
MIME是服务器通知客户机传送文件是什么类型的主要方法，客户机浏览器也通过MIME告诉服务器它的参数。在网上，如果接收到的文件没有MIME头，就默认它为HTML格式。但这样也不好，因为当MIME的包头是text/plain时，浏览器将直接显示而不关心它的什么字体，颜色之类的参数，这样显示出来的内容可不是很好看呀。
MIME头是什么样子要看它是用在电子邮件中还是用在浏览器上，两者内容可能有所不同。对于邮件头来说，版本号，内容类型声明，编码方式，内容描述是必不可少的。这是用于邮件头中的格式，在下面，我们将重点说到在HTTP中传送MIME头，这时MIME头要简单一些。
下例是一个邮件的标准MIME头：

Mime-Version: 1.0 //版本号：1.0
Content-Type: multipart/mixed; boundary="IMA.Boundary.750407228" //内容类型是多种的
--IMA.Boundary.750407228
Content-Type: text/plain; charset=US-ASCII //内容类型：文本，字符是ASCII的
Content-Transfer-Encoding: 7bit //编码方式：7位
Content-Description: cc:Mail note part

在用于浏览器时，用户不需要知道那么多的信息，所以MIME头就比较简单了。在访问一个网页时，浏览器和服务器之间产生一个会话，作为请求内容的一部分，浏览器发送它能够理解的MIME类型的描述，这就告诉服务器，浏览器除了网页外还可以支持什么，服务器对这个信息一般不作为什么修改。
服务器通过发向客户机的MIME头通知客户浏览器内容是什么，我们看看下面这个头：

Content-type: text/html

在实现的时候，一定要注意MIME头后要跟一个空行，不然这个头会被浏览器忽略，这个头会被当作文本显示出来。当服务器传送GIF图象时，头会如下：

Content-type: image/gif
Content-transfer-encoding: BINARY

通常的MIME内容类型并不起什么作用，浏览器可以自己识别内容的类型，但是如果您使用一些另外的类型，这个问题可就大了，如果你使用了text/postscript，那浏览器会显示下载窗口，或就把这个东西显示出来，那可就不好办了。下面我们介绍一下标准MIME类型。

Text. 文本，它用于描述不同类型的文本，包括通常的文本，PostScript和HTML，虽然HTML不是一个可能的子类型。

Multipart. 多类型，指出此信息包括多种信息，不止一种类型。

Message. 用于标记不同类型的消息。

Application. 应用类型。

Image. 图象，用于标明图形文件。

Audio. 声音，用于标明声音文件。

Video. 影象，用于标明动画文件。

每个MIME类型有不同的子类型，实际上，您不可能单独使用类型而不使用子类型，只有一个例外，这就是"telnet"类型。IANA提供45种类型/子类型对支持。当然，标准是开放的，允许用户自定义自己的类型，用户自定义类型要以“X-”开始以示区别。在添加新的类型时，一定要注意，尽量使用已有的类型达到自己的目的。如果非要添加新的类型，一定要保证服务器一方支持这种类型，也要保证客户端也能够通过一些应用程序（如插件）来识别新类型。如果您的网站的访问者很广，不要轻易使用新类型，要么使用已有的类型，或者向IANA提出注册请求。

二、什么是MIME类型
在把输出结果传送到浏览器上的时候，浏览器必须启动是党的应用程序来处理这个输出文档。这可以通过多种类型MIME（多功能网际邮件扩充协议）来完成。在HTTP中，MIME类型被定义在Content-Type header中。

例如，架设你要传送一个Microsoft Excel文件到客户端。那么这时的MIME类型就是“application/vnd.ms-excel”。在大多数实际情况中，这个文件然后将传送给Execl来处理（假设我们设定Execl为处理特殊MIME类型的应用程序）。在ASP中，设定MIME类型的方法是通过Response对象的ContentType属性。

多媒体文件格式MIME

最早的HTTP协议中，并没有附加的数据类型信息，所有传送的数据都被客户程序解释为超文本标记语言HTML 文档，而为了支持多媒体数据类型，HTTP协议中就使用了附加在文档之前的MIME数据类型信息来标识数据类型。

MIME意为多目Internet邮件扩展，它设计的最初目的是为了在发送电子邮件时附加多媒体数据，让邮件客户程序能根据其类型进行处理。然而当它被HTTP协议支持之后，它的意义就更为显著了。它使得HTTP传输的不仅是普通的文本，而变得丰富多彩。

每个MIME类型由两部分组成，前面是数据的大类别，例如声音audio、图象image等，后面定义具体的种类。

常见的MIME类型

超文本标记语言文本 .html,.html text/html
普通文本 .txt text/plain
RTF文本 .rtf application/rtf
GIF图形 .gif image/gif
JPEG图形 .ipeg,.jpg image/jpeg
au声音文件 .au audio/basic
MIDI音乐文件 mid,.midi audio/midi,audio/x-midi
RealAudio音乐文件 .ra, .ram audio/x-pn-realaudio
MPEG文件 .mpg,.mpeg video/mpeg
AVI文件 .avi video/x-msvideo
GZIP文件 .gz application/x-gzip
TAR文件 .tar application/x-tar

Internet中有一个专门组织IANA来确认标准的MIME类型，但Internet发展的太快，很多应用程序等不及IANA来确认他们使用的MIME类型为标准类型。因此他们使用在类别中以x-开头的方法标识这个类别还没有成为标准，例如：x-gzip，x-tar等。事实上这些类型运用的很广泛，已经成为了事实标准。只要客户机和服务器共同承认这个MIME类型，即使它是不标准的类型也没有关系，客户程序就能根据MIME类型，采用具体的处理手段来处理数据。而Web服务器和浏览器（包括操作系统）中，缺省都设置了标准的和常见的MIME类型，只有对于不常见的 MIME类型，才需要同时设置服务器和客户浏览器，以进行识别。

由于MIME类型与文档的后缀相关，因此服务器使用文档的后缀来区分不同文件的MIME类型，服务器中必须定义文档后缀和MIME类型之间的对应关系。而客户程序从服务器上接收数据的时候，它只是从服务器接受数据流，并不了解文档的名字，因此服务器必须使用附加信息来告诉客户程序数据的MIME类型。服务器在发送真正的数据之前，就要先发送标志数据的MIME类型的信息，这个信息使用Content-type关键字进行定义，例如对于HTML文档，服务器将首先发送以下两行MIME标识信息,这个标识并不是真正的数据文件的一部分。

Content-type: text/html

注意，第二行为一个空行，这是必须的，使用这个空行的目的是将MIME信息与真正的数据内容分隔开。

三、解决win2003服务器不能下载iso/exe/rmvb等文件的问题
--------------------------------------------------------------------------------
今天有朋友帮忙维护flydown，告诉我说上传的金山词霸无法下载，看了一下，原来是.ISO文件。原来在win2000服务器没有这个问题，可以用http模式下载 zip rar iso 等文件
现在改成win2003，下载zip rar等正常，也没有注意iso，现在发现iso文件无法下载，下载路径肯定正确，应该是IIS处于安全考虑没有注册ISO吧。

解决办法：打开IIS，选中服务器，点右键，属性里有MIME类型，

添加扩展名：.iso

类型：application

ok!

另外也可以单独对网站进行设置：网站－&gt;属性－&gt;HTTP头－－MIME类型

添加扩展名：.iso

类型：application