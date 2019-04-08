# JSP九大内置对象极其作用

![JSP九大内置对象](https://github.com/JasonCeng/NoteBook-Java/blob/master/Java%E8%AF%AD%E8%A8%80%E7%9F%A5%E8%AF%86/img/JSP%E4%B9%9D%E5%A4%A7%E5%86%85%E7%BD%AE%E5%AF%B9%E8%B1%A1.png)

## JSP九大内置对象
（1）	request对象 `javax.servlet.http.HttpServletRequest`

该对象代表了客户端的请求信息，主要用于接受通过HTTP协议传送到服务器的数据。（包括头信息、系统信息、请求方式以及请求参数）request对象的作用域为一次请求。

当Request对象获取客户端提交的汉字字符时，会出现乱码问题，必须进行特殊处理。

**方法一：**

首先，将获取的字符串用ISO-8859-1进行编码，并将编码存放到一个字节数组中，然后再将数组转换为字符串对象。如下：
```java
String name = new String(request.getParameter(“name”).getBytes(“ISO-8859-1”));
```

**方法二：**

使用request.setCharacterEncoding(“Encoding”)方法，如下：

```java
request.setCharacterEncoding(“gb2312”);
String name = new String(request.getParameter(“name”);
```

**例子：**

inputName.jsp

```JSP
<%@ page language="java" contentType="text/html; charset=gbk"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<meta http-equiv="Content-Type" content="text/html; charset=gbk">
<head>

<title>数据录入</title>
</head>

<body>
<form action="show.jsp" method="get">
用户名：<input type="text" name="user"></input>
密码：<input type="password" name="pwd"></input>
<br>
<input type="submit" value="登录"></input>
<input type="reset" value="重置"></input>
</form>
</body>
</html>
```

show.jsp
```JSP
<%@ page language="java" contentType="text/html; charset=gbk"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>

<title>传递过来的数据显示</title>
</head>
<body>
<%
			String name = request.getParameter(“name”);
			Byte b[] = name.getBytes(“ISO-8859-1”);
			name = new String(b);

				String pwd = request.getParameter(“pwd”);
				Byte b1[] = pwd.getBytes(“ISO-8859-1”);
				pwd = new String(b1);

				out.println(“姓名是：”+name+”<br>”);
				out.println(“密码是：”+pwd+”<br>”);
		%>
	</body>
</html>
```
**request常用的方法：**

* getParameter（String strTextName）获取表单提交的信息 `request.getParameter()`

* getProtocal() 获取客户使用的协议`String strProtocal = request.getProtocal();`

* getServletPath() 获取客户提交信息的页面 `String strServlet = request.getServletPath();`

* getMethod() 获取客户提交信息的方式 `String strMethod = request.getMethod();`

* getHeader() 获取HTTP头文件中的accept，accept-encoding和Host的值，`String strHeader = request.getHeader();`

*	getRemoteAddr() 获取客户的IP地址。`String strIP = request.getRemoteAddr();`

*	getRemoteHost() 获取客户机的名称。`String clientName = request.getRemoteHost();`

*	getServerName() 获取服务器名称。`String serverName = request.getServerName();`

*	getServerPort() 获取服务器的端口号。`int serverPort = request.getServerPort();`

*	getParameterNames() 获取客户端提交的所有参数的名字。

```Java
Enumeration enum = request.getParameterNames();
while(enum.hasMoreElements()) {
		String s = (String)enum.nextElement();
		out.println(s);
}
```

（2）	response对象 `javax.servlet.http.HttpServletResponse`

response代表的是客户端的响应，主要是将JSP客户端处理过的对象传回客户端。response对象也有作用域，它只在JSP页面内有效。

具有动态响应contentType属性，当一个用户访问一个JSP页面时，如果该页面用page指令设置页面的contentType的属性是text/html，那么JSP引擎将按照这个属性值作出反应。

如果要动态改变这个属性值来响应客户，就需要使用Response的`setContentType(String s)`方法来改变contentType的属性值。

`response.setContentType(String s);`参数s可取`text/hmtl`，`application/x-msexcel`，`application/msword`等。

在某些情况下，当响应客户时，需要将客户重新引导到另一个页面，而言使用`response的sendRedirect(URL)`方法实现客户端的重定向。

```Java
response.sendRedirect(index.jsp);
```

（3）	session对象 `javax.servlet.http.HttpSession`

session对象是一个JSP内置对象，它在第一个JSP页面被转载时自动创建，完成会话期管理。从一个客户打开浏览器并连接到服务器开始，到客户关闭浏览器离开这个服务器结束，被称为一个会话。当一个客户访问服务器时，可能会在这个服务器的几个页面之间来回切换，服务器应当通过某种办法知道这是一个客户，就需要session对象。

当一个客户首次访问服务器上的一个jsp页面时，JSP引擎产生一个session对象，同时分配一个String类型的ID号，JSP引擎同时将这个ID号发送到客户端，存放在cookie中，这样session对象，知道客户关闭浏览器后，服务器端该客户的session对象才消失，并且和客户的会话对应关系消失。当客户重新打开浏览器再连接到该服务器时，服务器为该客户重新创建一个新的session对象。

session对象是由服务器自动创建的与用户请求相关的对象。服务器为每个用户都生成一个session对象，用于保存该用户的信息，跟踪用户的操作状态。

session对象内部使用Map类来保存对象数据，因此保存数据的格式为“key/value”。session对象的value类型可以为复杂的对象类型，而不仅仅为局限于字符串类型。

**session常用的方法：**

* public String getId() 获取session对象的编号

* public void setAttribute(String key, Object obj) 将参数Object指定的对象obj添加到Session对象中，并未添加的对象指定一个索引关键字。

* public Object getAttribute(String key) 获取session中含有关键字的对象。

* public Boolean isNew() 判断是否是一个新用户

（4）	application对象 `javax.servlet.ServletContext`
application对象可将信息可将信息保存在服务器中，直到服务器关闭，否则application对象保存的信息会在整个应用中都有效。与session对象相比，application对象的生命周期更长，类似于系统的“全局变量”，而session类型与系统的“局部变量”，只不过这里是以时间维度去类比定义。

服务器启动后就产生了application对象，当客户在访问的网站的各个页面之间浏览时，这个application对象都是同一个，直到服务器关闭。但是与session对象不同，所有客户的application对象都是同一个，即所有客户共享这个内置的application对象。

`setAttribute(String key,Object obj) `将参数Object指定的对象obj添加到Application对象中，并未添加的对象指定一个索引关键字。

`getAttribute(String key)` 获取application对象中含有关键字的对象。

（5）	out对象 `javax.servlet.jsp.jspWriter`

out对象用于在Web浏览器内输出信息，并且管理应用服务器上的输出缓冲区。在使用out对象输出数据时，可以对数据缓冲区进行操作，及时清除缓冲区中的残余数据，为其他的输出让出缓冲空间。待数据输出完毕后，要及时关闭输出流。

out对象是一个输出流，用来向客户端输出数据。out对象用于各种数据的输出。

**out常用的方法：**

* out.print() 输出各种类型的数据

* out.newLine()  输出一个换行符

* out.close() 关闭流

（6）	pageContext对象 `javax.servlet.jsp.PageContext`

pageContext对象的作用是取得任何范围的参数，通过它可以获取JSP页面的request、response、session、application、out等对象。pageContext对象相当于页面中所有功能的集大成者。

pageContext对象的创建和初始化都是由容器来完成的，在JSP页面中可以直接使用pageContext对象。

**pageContext常用的方法：**

* `jspWriter getOut()` 返回当前客户端响应被使用的jspWriter流（out）

* `HttpSession getSession() `返回当前页的HttpSession对象（Session）

* `Object getPage() `返回当前页的Object对象（page）

* `ServletRequest getRequest() `返回当前页的Request对象（Request）

* `ServtResponse etResponse()` 返回当前页的Response对象（Response）

* `void setAttribute(String name, Object Attribute) `设置属性及属性值

* `Object getAttribute(String name)` 返回某属性的作用范围

* `int getAttribute(String name) `返回某属性的作用范围

* `void forward(String relativeURLPath) `使当前页重定向到另一个页面

* `void include(String relativeURLPath)` 在当前位置包含另一个文件


（7）	config对象 `javax.servlet.ServletConfig`

config对象的主要作用是取得服务器的配置信息。通过pageContext对象的getServletConfig()方法可以获取一个config对象。当一个Servlet初始化时，容器把某些信息通过config对象传递给这个Servlet。开发者可以在web.xml文件中为应用环境中的Servlet程序和JSP页面提供初始化参数。

**config常用的方法：**

* `ServletContext getServletContext() `返回包含服务器相关信息的ServletContext对象

* `String getInitParameter(String name)` 返回初始化参数的值

* `Enumeration getParameterNames()` 返回Servlet初始化所需所有参数的枚举

（8）	page对象 `java.long.Object`

page对象代表JSP本身，只有在JSP页面内才是合法的。page隐藏对象本质上包含Servlet接口引用的变量，类似于Java编程中的this指针。

**page常用方法：**

主要是Object中声明的方法：

* class getClass() 返回此Object的类

* int hashCode() 返回此Object的hash码

* boolean equals(Object obj) 判断Object是否与指导的Object对象相等

* void copy(Object obj)把此Object拷贝到指定的Object对象中

* Object clone() 克隆此Object对象

* String toString()把此Object对象转换为String对象

* void notify() 唤醒一个等待的线程

* void wait(int timeout) 使一个线程处于等待直到timeout结束或唤醒

* void wait() 使一个线程处于等待直到被唤醒

（9）	exception对象 `java.lang.Throwable`

exception对象的作用是显示异常信息，只有在包含isErrorPage=”true”的页面中才可以被使用，在一般的JSP页面中使用该对象将无法编译JSP文件。exception对象和所有Java对象一样，都具有系统提供的继承结构。

exception对象几乎定义了所有异常情况。在Java程序中，可以使用try/catch关键字来处理异常；如果在JSP页面中出现没有捕获的异常，就会生成exception对象，并把exception对象传送到在page指令中设定的错误页面中，然后再错误页面中处理相应的exception对象。

**Exception常用方法：**

* String getMessage() 获取产生异常的信息

* String toString() 获取描述异常的信息

* void printStackTrace() 获取异常及其栈轨迹

* Throwable FillStackTrace() 重写异常的执行栈轨迹


## 其他：JSP的Cookie（客户端，不是内置对象）

当客户第一次访问服务器的时候，服务器会在用户的硬盘上创建一个小文本，用来记录客户的跟踪信息，例如访问站点的次数等。它的内容由web服务器决定，可以随时读取，但是只能被web站点的页面读取。Cookies文件存放在Windows的Cooikes文件夹下。

Cookie不是内置对象，所以需要new。Cookie是由服务器产生，然后发送到客户端保存。（本地缓存）

类：`javax.servlet.http.Cookie`

构造器：`public Cookie(String name,String value)`

服务端发送到客户端：`response.addCookie(Cookie cookie)`

页面跳转：`response.sendRedirect();`

客户端获取Cookie：`request.getCookies();`

```Java
Cookie[] cookies = request.getCookies();
for(Cookie cookie : cookies)｛
	out.print(cookie	.getName() + “---”cookie.getValue());
｝
```

设置cookie过期时间：`setMaxAge()`

不过虽然设置了cookie过期时间，但是如果从request那边是查看不见的，因为cookie默认只把name和value传到服务器。

如果客户禁用了cookie，那么按照默认方式session将失效，但是我们可以将sessionId通过URL的方式携带到后台服务器。

## 参考

[1] (jsp 九大内置对象和其作用详解)(https://www.cnblogs.com/leirenyuan/p/6016063.html)

[2] (JSP九大内置对象的作用和用法总结？)(https://blog.csdn.net/sona_shi555/article/details/7797068)

[3] (jsp中request处理汉字信息)(https://blog.csdn.net/homedjy/article/details/8468046)

[4] (JSP中page和pageContext的区别)(https://blog.csdn.net/baidu_20876831/article/details/78952409)

[5] (JSP page对象)(https://blog.csdn.net/sinat_32873711/article/details/53144446)

[6] (JSP pageContext对象和config对象)(https://blog.csdn.net/mikou168/article/details/80887037)

[7] (JSP内置对象之exception对象)(https://blog.csdn.net/wildbeast_/article/details/79073575)

[8] (JSP内置对象——exception对象)(https://www.jellythink.com/archives/204)

[9] (JSP内置对象之Exception对象)(https://blog.csdn.net/yhy_it/article/details/80612541)

[10] (jsp中的cookie(客户端,不是内置对象))( https://blog.csdn.net/weixin_42979840/article/details/82825580)

[11] (JSP九大内置对象+其他对象Cookie)(https://blog.csdn.net/m0_37834471/article/details/80946161)

[12] (JSP —— 内置对象 Cookie 与 Session)(https://blog.csdn.net/qq_19865749/article/details/69976936)

[13] (Servlet--浅析会话管理之Cookie、URL重写、HttpSession原理)(https://blog.csdn.net/championhengyi/article/details/72855552)

[14] (URL重写实现session跟踪)(https://blog.csdn.net/aircraftxjd/article/details/42060503)

[15] (使用url重写实现Session跟踪)(https://blog.csdn.net/mmllkkjj/article/details/6132139)
