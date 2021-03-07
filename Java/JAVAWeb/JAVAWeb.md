# JAVAWeb

#### Tomcat访问

双击bin目录下的startup.bat运行该文件

本地IP：222.24.28.235

http：//222.24.28.235：8080（Tomcat默认端口号）

------

**Request_请求转发**

步骤：

​		1.通过request对象获取请求转发器对象：RequestDispatcher  getRequestDispatcher（String  path）

​		2.通过RequestDispatcher对象来进行转发：forward（ServletRequest  request， ServletResponse  response）

#### **特点：（面试题）**

​		**1.浏览器地址栏路径不发生变化**

​		**2.只能转发当前服务器内部资源中**

​		**3.转发是一次请求**

------

#### **面试题：**

**重定向（redirect）的特点：**

​			**1.地址栏发生变化**

​			**2.重定向可以访问其他站点（服务器）的资源**

​			**3.重定向是两次请求。不能使用request对象来共享数据**

**转发（forward）的特点：**

​			**1.转发地址栏路径不变**

​			**2.转发只能访问当前服务器下的资源**

​			**3.转发是一次请求，可以使用request对象来共享数据**

------

服务器输出字符数据到浏览器

步骤：

​		1.获取字符输出流

​		2.输出数据

注意：

​	**乱码问题：**

​				1.PrintWriter pw = response.getWriter();获取的流的默认编码是ISO-885-1

​				2.设置该流的默认编码

​				3.告诉浏览器响应体使用的编码

**最简单的方式：response.setContentType("text/heml;charset-utf-8");**

