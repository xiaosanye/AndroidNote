RESTful 的核心是 `everything is a “resource”`，所有的HTTP action，都应该是在相应resource上作增删改查操作，而API 就是对资源的管理操作，而这个具体操作是由 HTTP action 指定的。

目前比较成熟的一套网络应用程序的API设计理论。


### HTTP协议语义使用方法

在一个RESTful系统里，客户端向服务端发起索取资源的操作只能通过HTTP协议语义来进行交互。最常用的HTTP协议语义有以下5个：

GET : 从服务器取出资源（一项或多项）

POST：在服务器新建一个资源

PUT：在服务器更新资源（客户端提供完整资源数据）

DELETE：从服务器删除资源

HEAD : 从服务器获取报头信息（不是资源）


### WEB服务接收与返回的互联网资源类型

客户端与服务端进行交互响应时，需要规定双方能够接受何种类型的媒体表现形式，最常见的以application开头的媒体格式类型有：

application/json： JSON数据格式

application/xhtml+xml：XHTML格式

application/xml： XML数据格式

application/atom+xml：Atom XML聚合格式



### API设计原则
#### 1、URL
URL中应尽量使用名词，尽量避免使用动词；
应该尽量将API部署在专用域名之下；
https://api.example.com
如果确定 API 很简单，不会有进一步扩展，可以考虑放在主域名下；
https://example.org/api/
应该将API 的版本号放入URL，或者将版本号放在HTTP头信息中；
https://api.example.com/v1/

#### 2、路径
路径又称"终点"（endpoint），表示API的具体网址。
在RESTful架构中，每个网址代表一种资源，所以网址中不能有动词，只能有名词，而且所用的名词往往与数据库的表格名对应。一般来说，数据库中的表都是同种记录的”集合"（collection），所以API中的名词也应该使用复数。






























#
