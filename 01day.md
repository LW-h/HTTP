## 了解Web

> 本章将概述Web是建立在何种技术之上，以及HTTP是如何诞生并发展的。

> Web使用HTTP【HyperText Transfer Protocol】,超文本传输协议，可以说Web是建立在HTTP上通信的.HTTP通常被译为超文本传输协议，但严谨的翻译应该是超文本转移协议

#### HTTP诞生

###### 为知识共享诞生

> 1989年3月HTTP诞生了。WWW这一名词，是Web浏览器当年用来浏览超文本的客户端应用程序时的名称。现在则表示一系列集合，也可简称Web。开始是由CERN【欧洲核子研究组织】的蒂姆.伯纳斯-李博士提出的一种让远隔两地的研究者们共享知识的想法。现在已经提出3项WWWW构架技术：

+ HTML：超文本标记语言
+ HTTP：文档传递协议
+ URL：【Uniform Resource Locator】指定文档所在地址

###### Web成长时代

> 1990年11月，CERN成功研发了世界第一台Web服务器和Web浏览器.1993年1月，现代浏览器的之父NCSA【National Center for Supercomputer Application,美国国家超级计算机应用中心】研发了Mosaic,它以in-line内联等形式显示HTML图像.1994年12月，王景通信公司发布了Netscape Navigator1.0。1995年微软公司发布了Internet Explorer1.0和2.0。紧随其后的就是以成为Web服务器标准之一的Apache0.2,HTML也发布了2.0，那一年，Web技术突飞猛进

> 1995年左右，微软与网景公司爆发了浏览器大战，2000以后随着网景公司衰落而告一段落。但在2004年，Mozilla基金会发布了Firefox浏览器，第二次大战开始

> 现今IE浏览器基本上已经淘汰，微软代替的产品为Edge浏览器，另外Chrome、Opera、Safari等浏览器也在占领市场

###### HTTP

+ HTTP/0.9：HTTP于1990年问世，那时的HTTP并没有作为正式的标准被建立
+ HTTP/1.0:HTTP正式作为标准被公布是在1996年5月，版本被命令为HTTP/1.0，记载于[RFC1945](http://www.ietf.org/rfc/rfc1945.txt)
+ HTTP/1.1:1997年1月公布的HTTP/1.1是目前主流的HTTP协议版本。[RFC2616](http:www.ietf.org/rfc/rfc2616.txt)

> 作为Web文档传输协议，HTTP版本几乎没有更新。新一代的HTTP2.0正在制度中。现在HTTP协议已经超出了Web这个框架的局限，被运用到了各种场景里

###### TCP/IP

> 详细关于TCP/IP讲解，请观我的另外一个仓库Wireshark。利用TCP/IP协议族进行网络通信时，会通过分层顺序与对方进行通信。发送端从应用层往下走，接收端则往应用层往上走。整个过程以HTTP为例子：**客户端在应用层(HTTP协议)发出一个想看某个Web页面的HTTP请求-->在传输层把从应用层接收到的数据进行分割，并在各个报文上打上标记序号及端口号转发给网络层-->在IP网络层，增加了通信目的地下一跳的MAC地址，转发给链路层下一跳通信端-->接收端在链路层接收到数据，按序往上层发送，一直到应用层接收到。发送端在层与层之间传输数据时，每经过一层时必须会被打上一个属于该层的头部信息，反之，接收端每经过一层时会把对应的首部去掉**。这种把数据包封装起来的做法叫做封装【encapsulate】

#### 与HTTP关系密切的协议：IP、TCP、DNS

+ 负责传输路径的IP协议
+ 确保可靠性的TCP协议
+ 负责域名解析的DNS服务

#### URI和URL

> URI:统一资源标识符。URL【Uniform Resource Locator】:统一资源定位符.URL正是使用Web浏览器等访问Web页面需要输入的网页地址

URI【Uniform Resource Identifier】

+ Uniform:规定统一的格式可方便处理多种不同类型的资源，而不用根据上下文环境来识别资源指定的访问方式
+ Resourece:资源定义‘可标识的任何东西’，除了文档文件、图像或服务等能够区别于其他类型的。全部可以作为资源。另外，资源不仅可以是单一的，还可以是多数的集合体
+ Identifier:表示可表示的对象，也称标识符
> URI就是由某个协议方案表示的资源的定位标识符。协议方案是指访问资源所使用的协议类型名称。标准的URI协议方案有30种左右，由隶属于国际互联网资源管理的非营利社团ICANN(Internet Corporation for Assigned Names and Numbers,互联网名称与数字地址分配机构)的LANA(Internet Assigned Numbers Authority,互联网号码分配据)管理分配。**URI用字符串标识某一互联网资源，而URL表示资源的地点(互联网上所处的位置)，URL是URI的子集**

###### URI格式

> 表示指定的URI，要使用涵盖全部必要信息的绝对URI、绝对URL以及相对URL。相对URL，是指从浏览器中基本URI处指定的URL，例如：/images/xx.gif.绝对URI例如：**http://user:pass@www.example.org:80/dir/index.html?uid=1#ch1**,具体参数讲解如下：

+ 使用http或https等协议方案访问资源时要指定协议类型。不区分大小写，最后附带一个冒号【：】
+ 登录信息【认证】：指定用户名和密码作为服务器端获取资源时必要的登录信息，此选项可选
+ 服务器地址：使用绝对URI必须指定待访问的服务器地址。地址可以是类似域名、IPV4、IPV6
+ 服务器端口号：指定服务器连接的端口号。此项也是可选，省略则为默认端口号
+ 带层次的路径：指定服务器上的文件路径来定位特指的资源，与UNIX系统文件目录结构相似
+ 查询字符串：针对已指定的文件路径内的资源，可以使用查询字符串传入任意参数，可选
+ 片段标识符：使用片段标识符可以标记出以获取资源中的子资源，可选

> 有些用来制定HTTP协议技术标准的文档，它们被称为RFC【Request for Comments】,征求修正意见书