# Servlet生命周期

Servlet运行在Servlet容器中，其生命周期由容器来管理。Servlet的生命周期由`javax.servlet.Servlet`接口中的`init()`、`service()`和`destroy()`方法来表示。

## Servlet的生命周期包括以下4个阶段

（1）	加载与实例化

（2）	初始化

（3）	请求处理

（4）	服务终止

## Web服务器与客户端交互时Servlet的工作过程

（1）	客户端对Web服务器发出请求

（2）	Web服务器接收到请求后将其发送给Servlet

（3）	Servlet容器为此产生一个实例对象并调用ServletAPI中相应的方法来对客户端HTTP请求进行处理，然后将处理的响应结果返回给Web服务器

（4）	Web服务器将Servlet实例对象中收到的响应结果发送回客户端

## 参考
[1] (java基础面试题（Servlet生命周期）)(https://www.cnblogs.com/lgk8023/p/6427977.html)
