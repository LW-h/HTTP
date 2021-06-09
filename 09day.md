## 基于HTTP的功能追加协议

> 在建立HTTP标准规范时，制定者主要想把HTTP当作传输HTML文档协议。但随着时代的发展，Web的用途更具多样性，例如：在线购物网站、SNS(Social Networking Service,社交网络服务)、企业或组织内部的各种管理工具。这些虽然已经实现，但性能上未必最优，这是因为HTTP协议上的限制以及自身性的限制

#### 消除HTTP瓶颈的SPDY

> Google在2010年发布了SPDY(取自SPeeDY,发音同speedy),开发目的在于解决HTTP的性能瓶颈，缩短Web页面的加载时间(50%)[SPDY-The Chromium Projects](http://www.chromium.org/spdy/).HTTP瓶颈如下：

+ 一条连接上只可发送一个请求
+ 请求只能从客户端开始，客户端不可以接收除响应以外的指令
+ 请求/响应首部未经压缩就发送，首部信息越多延迟越大
+ 发送冗长的首部，每次互相发送相同的首部造成的浪费较多
+ 可任意选择数据压缩格式，非强制压缩发送

> Ajax(Asynchronous JavaScript and XML,异步JavaScript与XML技术)是一种有效利用JavaScript和DOM(Document Object Msodel,文档对象模型)的操作。一达到局部Web页面替换加载的异步通信手段。由于只更新一部分，响应中传输的数据量会因此减少。Ajax的核心技术是名为XMLHttpRequest的API。通过JavaScript脚本的调用和服务器进行通信。**利用Ajax实时地从服务器获取内容，有可能导致大量请求产生，另外，Ajax没有解决HTTP协议本身存在地问题**

Comet：

> 一旦服务器有内容更新，Comet不会让请求等待，会直接发送给客户端。是一种通过模拟延迟回答，实现向客户端推送(Server Push)的功能。但为了实现推送功能，Comet会先将响应置于挂起状态，当服务器端有内容更新时，再返回响应。缺点：**虽然可以做到内容实时更新，但为了保留响应，连接的持续时间会变成。为了持续连接会消耗更多的资源。仍未解决HTTP协议本身存在的问题**

#### SPDY

SPDY目标：在协议级别上消除HTTP所遭遇的瓶颈

SPDY没有完全改写HTTP协议，而是在TCP/IP的应用层与传输层之间通过新加会话层。同时，考虑到安全性问题，SPDY规定在通信中使用SSL。SPDY以会话层的形式加入，控制对数据的流动，但还是采用HTTP建立通信连接。使用SPDY后，HTTP协议额外获得一些功能：

+ 多路复用流，通过单一的TCP连接，可以无限制处理多个HTTP请求。所有请求的处理都在一条TCP连接上完成，因此TCP的处理效率得到提高
+ 赋予请求优先级：SPDY不仅可以无限制地并发处理请求，还可以给请求逐个分配优先级。主要是为了在发送多个请求时，解决因带宽低而导致响应变慢地问题
+ 压缩HTTP首部：压缩HTTP请求和响应的首部，通信产生的数据包数量和发送的字节数就会更少
+ 推送功能：支持服务器主动向客户端推送数据，而不必等待客户端的请求
+ 服务器提示功能：服务器可以主动提示客户端所需的资源。由于在客户端发现资源之前就可以获知资源的存在，因此在资源已缓存等情况下，可以避免发送不必要的请求

> SPDY确实可以消除HTTP瓶颈问题，但很多Web网站存在的问题并非仅仅是由HTTP瓶颈所导致。对Web本身的 速度提升，还应该从其它细致钻研的地方入手，比如改善Web内容的编写方式...

#### 使用浏览器进行全双工通信的WebSocket

> 利用Ajax和Comet技术进行通信可以提升Web的浏览速度。但问题在于使用HTTP协议，就无法彻底解决瓶颈问题。WebSocket网络技术正是解决这些问题而实现的一套新协议及API。WebSocket通信协议在2011年12月11日，被RFC6455-The WebSocket Protocol定位标准

> WebSocket的设计与功能。即Web浏览器与Web服务器之间全双工通信标准。WebSocket协议标准由IETF定为标准，WebSocket API由W3C定为标准。主要就是为了解决Ajax和Comet里XMLHttpRequest附带的缺陷所引起的问题

WebSocket协议

> 一旦客户端与服务器之间建立起WebSocket协议的通信连接，之后所有的通信都依靠这个专用协议进行。通信双方可以发送任意格式的数据。由于是建立在HTTP基础上的协议，因此发起方仍是客户端，而一旦建立WebSocket通信连接，不论是哪一方，都可以直接向对方发送报文。WebSocket协议的主要特点如下：

+ 推送功能：服务器可以直接发送数据，而不必要等待客户端的请求
+ 减少通信量：只要建立起WebSockket连接，就希望一直保持连接状态。和HTTP相比，不但每次连接时的总开销减少，而且由于WebSocket的首部信息很小，通信量也相应减少
+ 为了实现WebSocket通信，在HTTP建立连接之后。需要完成一次握手(Handshaking)：**请求：【为了实现WebSocket通信，需要用到HTTP的Upgrade首部字段，告知服务器通信协议发生了改变，以达到握手的目的。Sec-WebSocket-Key字段记录着握手过程中必不可少的键值，Sec-WebSocket-Protocol记录使用的子协议。子协议按协议标准在连接分开使用时，定义那些连接的名称】。响应：【对于之前的请求，返回状态码101 Switching Protocols的响应。Sec-WebSocket-Aaccept字段值由握手请求中的Sec-WebSocket-Key的字段值生成的】**，成功建立WebSocket链接之后，通信不再使用HTTP数据帧，而采用WebSocket独立的数据帧。**HTTP阶段(客户端【Upgrade:websocket】-->服务端响应【101 Switching Protocols】)--WebSocket阶段【该协议支持全双工通信，不必等请求可以直接发送数据】>**

WebSocket API

> JavaScript可调用‘The WebSocket API’(http://www.w3.org/TR/websockets/,由W3C定制)提供的WebSocket程序接口，以实现WebSocket协议下全双工通信


#### HPPT/2.0

> 目的是改善用户在使用Web时的速度体验，基本上会通过HTTP/1.1与TCP链接。实现方法如下：

+ SPDY
+ HTTP Speed + Mobility【是由微软起草，用于改善移动端的通信速度与性能，建立在谷歌公司提出的WebSocket基础之上】
+ Network-Friendly HTTP Upgrade【在移动端通信时改善HTTP性能的标准】 

HTTP/2.0围绕7项技术，如下：

+ 压缩【SPDY、Friendly】
+ 多路复用【SPDY】
+ TLS【Speed+Mobility】
+ 协商【Speed+Mobility,Friendly】
+ client拉拽server推送【client pull,server push】【speed+mobility】
+ 流量控制【SPDY】
+ WebSocket【Speed+mobility】

> WebDAV是基于万维网的分布式创作和版本控制，可以对Web服务器上的内容直接进行文件复制、编辑等操作的分布式文件系统。WebDAV扩展的概念如下：

+ 集合(Collection):是一种统一管理多个资源的概念。
+ 资源(Redource):把文件或集合称为资源
+ 属性(Property):定义资源的属性，定义以‘名称=值’的格式执行
+ 锁(Lock):把文件设置成无法编辑状态，多人同时编辑时，可防止同一时间进行内容写入

WebDAV内新增的方法及状态码：

+ PROPFIND:获取属性
+ PROPPATCH:修改属性
+ MKCOL:创建集合
+ COPY：复制资源及属性
+ MOVE：移动资源
+ LOCK：资源加锁
+ UNLOCK：资源解锁

为配合扩展方法，状态码也随之增加：

+ 102 Processing:可正常处理请求，但目前是处理状态
+ 207 Multi-Status:存在多种状态
+ 422 Unprocessible Enity:格式正确，内容错误
+ 423 Locked:资源已被加锁
+ 424 Failed Dependency:处理与某请求关联的请求失败，因此不再维持依赖关系
+ 507 Insuffcient Storage:保存空间不足

HTTP协议广泛原因

+ 编写接入互联网的软件，还需要编写实现与必要功能对应的协议。使用HTTP可以减少开发时间
+ 防火墙的基本功能就是禁止指定的协议和端口号的数据包通过，使用新协议或端口则必须修改防火墙设置
+ 互联网上，使用最高的当属Web
+ 许多公司或组织已设定权限将HTTP作为通信环境
+ 客户单浏览器已相当普遍，HTTP服务器数量已具有规模化...

