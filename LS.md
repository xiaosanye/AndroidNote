Java Web 技术 :
基础:jsp+servlet+JDBC:
jsp [本质是Servlet]: 用于 显示界面  ,通俗说就是HTML代码里可以写Java代码的一种文件,比如login.jsp 就是 展示login界面的文件[相当于静态网站的Login.html文件]

Servlet:就是控制逻辑代码的文件,控制调用哪一个业务逻辑层的代码

JDBC技术:就是Java访问数据库的一种技术,针对每种数据库,比如MySQL数据库和SQLServer数据库,都有与之对于的驱动[就是.jar包,封装好的Java代码],这里我们用的MySQL,所有需要MySQL的驱动包[mysql-connector-java-版本号.jar].让项目引用他就OK了.

其实用以上三种技术就可以做Java Web网站,但是为了代码的结构简单,可重用强
我使用了Struts2框架.Struts2 框架是一种MVC[Model -- view -- Control]框架


Python 爬虫 技术:
什么是爬虫?爬虫的原理是什么?
首先爬虫就是模拟浏览器,发送Http请求,就是访问网站,获取网站返回的HTML代码,如果用浏览器访问网站,获取HTML代码后会进行解析,渲染展示出界面
而爬虫就是在获取网站返回的HTML代码之后,通过字符串匹配获取我们想要的信息,我们想要什么?这里我们想要的是图片的网址,.比如,之后再通过图片的网址,找到下载到我们的本地电脑中;

代码解析:
