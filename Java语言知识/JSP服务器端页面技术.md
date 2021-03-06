# JSP服务器端页面技术

## 目录

## 1.Servlet和CGI的对比

* 调用一个CGI程序的时候，服务端就要新启用一个进程，服务完成后就销毁，效率比较低。而Servlet充分发挥了服务器端的资源并高效地利用，每次调用Servlet时并不是新启用一个进程，而是通过多线程方式运行其service方法，一个实例可以服务于多个请求，并且其实例一般不会销毁。

* 传统的CGI不具备平台无关特性，系统环境发生变化，CGI程序就要瘫痪。而Servlet具备Java的平台无关性，在系统开发过程中保持了系统的可扩展性、高效性。

* 传统的二层系统架构，即Web服务器+数据库服务器，在网站访问量大时，无法克服CGI程序与数据库建立连接时速度慢的瓶颈，从而死机、数据库死锁现象频繁发生。而Servlet有连接池的概念，它可以利用多线程的优点，在系统缓存中事先建立好若干与数据库的连接，在想与数据库打交道时再随时跟系统索取一个连接即可，反应速度可想而知。

## 2.Servlet的生命周期5个阶段：加载、创建、初始化、处理客户请求、卸载

（1）加载：容奇通过类加载器使用servlet类对应的文件加载servlet

（2）创建：通过调用servlet构造函数创建一个servlet对象

（3）初始化：调用init方法初始化

（4）处理客户请求：每当有一个客户请求，容器会创建一个线程来处理客户请求

（5）卸载：调用destroy方法让Servlet自己释放其占用的资源
