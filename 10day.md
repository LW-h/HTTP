## 构建Web内容的技术

> 刚开始，只能浏览简单的页面，如今，可以访问丰富多彩的资源

#### HTML

> Web页面几乎全由HTML构成，HTML是为了发送Web上的超文本而开发的标记语言。HTML文档内的特殊字符串叫做HTML标签(Tag)。由HTML构成的文档经浏览器解析、渲染后，呈现出来的就是Web页面

HTML版本

> Tim Berners-Lee提出HTTP概念的同时，还提出了HTML原型。1993年在伊利诺伊大学读的NCSA(The National Center for Supercomputing Application,国家超级计算机应用中心)发布了Mosaic浏览器(世界首个图形浏览器)，能够被Mosaic解析的HTML，统一标准后作为HTML1.0发布。现今HTML5标准不仅解决了浏览器之间的兼容问题，并且可把文本作为数据对待，更容易复用，动画等效果也变得更生动

#### 设计应用CSS

> CSS可以指定如何展现HTML内容的元素，属于样式标准之一。CSS理念就是让文档的结构和设计分离，达到解耦的目的。可通过指定HTML元素或特定的class、ID等作为选择器来限定样式的应用范围

#### 动态HTML

> 所谓动态HTML(Dynamic HTML),是指使用客户端脚本语言将静态的HTML内容变成动态的技术的总称。动态HTML技术是通过调用客户端脚本语言JavaScript，实现对HTML的Web页面的动态改造。利用DOM(Document Object Model,文档对象模型)可指定欲发生动态变化的HTML元素

更易控制HTML的DOM

> DOM是用以操作HTML文档和XML文档的API(Application Programming Interface,应用编程接口)。使用DOM可将HTML元素当做对象操作。DOM内存在各种函数，可以查阅HTML中的各个元素

#### Web应用

> Web应用是指通过Web功能提供的应用程序。例如：网站、网银...由程序创建的内容称为动态内容，而事先准备好的内容称为静态内容。Web应用则作用在动态内容上。

与Web服务器及程序协作的CGI

> CGI(common Gateway Interface,通用网管接口)是指Web服务器在接收到客户端过来的请求时转发给程序的一组机制。在CGI的作用下，程序会对请求做出相应的动作。使用CGI接口的程序叫做CGI程序。

因Java而普及的Servlet

> CGI由于每次接到请求，程序都要跟着启动一次。因此一旦访问量过大，Web服务器要承担相当大的负载。而Servlet运行在与Web服务器相同的进程中，因此受到的负载较小。Servlet的运行环境叫做Web容器或Servlet容器

#### 数据发布的格式及语言

> XML(eXtensible Markup Language,可扩展标记语言)是一种可按应用目标进行扩展的通用标记语言。旨在通过使用XML，使互联网数据共享变得更容易。XML和HTML都是从标准通用标记语言SGML(Standard Generalized Markup Language)简化而成。为了保持数据的正确读取，HTML不适合用来记录数据结构

> XML和HTML一样，使用标签构成树形结构，并且可自定义扩展标签。从XML文档中读取数据比起HTML更为简单。由于XML的结构基本上都是用标签分割而成的树形结构，因此通过语法分析器(Parser)的解析功能解析XML结构并取出数据元素。更容易地复用使得XML在互联网被广泛接受。例如：可在不同的应用之间的交换数据格式化

发布更新信息的RSS/Atom

> RSS(简易信息聚合，也叫聚合内容)和Atom都是发布新闻或博客日志等更新信息文档的格式的总称。两者都用到了XML

JavaScript衍生的轻量级JSON

> JSON(javaScript Object Notation)是一种以JavaScript(ECMAScript)的对象表示法为基础的轻量级数据标记语言。能够处理的数据类型有false/null/true/对象/数组/数字/字符串.7类。当初配合XML使用的Ajax技术也让JSON的应用变得更广泛。其它各种编程语言也提供了丰富的库类，已达到更轻便操作JSON