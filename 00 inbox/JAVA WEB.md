
# 01MYSQL

## 001 DDL操作数据库
## 002 DDL操作表
## 003 DML操作表
## 004 DQL
## 005 约束
## 006 数据库设计
## 007事务

含义：包含了一组数据库操作命令
### 01 开启事务
start transaction;
begin;

### 02 提交事务
commit;

### 03 回滚事务
rollback;

### 04 事务四大特征
-- 1. 原子性（Atomicity)：事务是不可分割的最小操作单位，要么同时成功，要么同时失败；
-- 2. 一致性（Consistency）：事务完成时，必须使所有的数据都保持一致状态；
-- 3. 隔离性（lsolation）:多个事务之间，操作的可见性；
-- 4. 持久性（Durability）:事务一旦提交或回滚，它对数据库中的数据的改变就是永久的；

## 008 JDBC
[概念] : JDBC 就是使用Java语言操作关系型数据库的一套API；
[全称]：( Java DataBase Connectivity）Java 数据库连接
同一套Java代码，操作不同的关系型数据库；
JDBC是一套标准[接口]。

Demo
```java
public class JDBCDemo {  
    public static void main(String[] args) throws Exception {  
    
        //  1. 注册驱动  
        Class.forName("com.mysql.cj.jdbc.Driver");  
  
        //  2. 获取链接  
        String url = "jdbc:mysql://127.0.0.1:3306/dbtest1";  
        String username = "root";  
        String password = "123456";  
        Connection conn = DriverManager.getConnection(url, username, password);  
  
        //  3.定义sql  
        String sql = "update student set score = 99 where id = 1";  
  
        //  4.获取执行sql的对象 Statement        
        Statement stmt = conn.createStatement();  
  
        //  5.执行sql  
        int count = stmt.executeUpdate(sql);  
  
        //  6.处理结果  
        System.out.println(count);  
  
        //  7.释放资源  
        stmt.close();  
        conn.close();  
    }  
}
```


# 02 WEB

## 001 http

1. http-请求数据格式
	1. 请求数据分为3部分：
		* 请求行：请求数据的第一行。其中GET表示请求方式，/表示请求资源路径，HTTP/1.1表示协议版本
		* 请求头：第二行开始，格式为key：value形式。
		* 请求体：POST请求的最后一部分，存放请求参数
		* GET请求和POST请求区别：
			1. GET请求请求参数在请求行中，没有请求体。POST请求请求参数在请求体中
			2. GET请求请求参数大小有限制，POST没有
	1. 常见的HTTP请求头：
		* Host：表示请求的主机名
		* User-Agent: 浏览器版本，例如Chrome浏览器的标识类似Mozilla/5.0..Chrome/79，IE浏览器的标识类似Mozilla/5.0(Windows NT…)like Gecko;
		* Accept：表示浏览器能接收的资源类型，如text/星号，image/星号 或者 星号/星号 表示所有;
		* Accept-Language：表示浏览器偏好的语言，服务器可以据此返回不同语言的网页；
		* Accept-Encoding：表示浏览器可以支持的压缩类型，例如gzip，deflate等。

2. http-响应数据格式
	1. 响应数据分为3部分：
		1. 响应行：响应数据的第一行，其中HTTP/1.1表示协议版本，200表示响应 状态码，OK表示状态码描述
		2. 响应头：第二行开始，格式为key：value形式
		3. 响应体：最后一部分。存放响应数据
	2. 常见的HTTP 响应头:
		* ContentType：表示该响应内容的类型，例如text/html,image/jpeg;
		* Content-Length：表示该响应内容的长度（字节数）;
		* Content-Encoding：表示该响应压缩算法，例如gzip；
		* Cache-Control：指示客户端应如何缓存，例如max-age=300表示可以最多缓存300秒
	3. 状态码分类-说明
		1. 1xx：响应中----临时状态码，表示请求已经接受，告诉客户端应该继续请求或者如果它已经完成则忽略它
		2. 2xx：成功----表示请求已经被成功接收，处理已完成
		3. 3xx：重定向----重定向到其它地方：它让客户端再发起一个请求以完成整个处理。
		4. 4xx：客户端错误----处理发生错误，责任在客户端，如：客户端的请求一个不存在的资源，客户端未被授权，禁止访问等
		5. 5xx：服务器端错误----处理发生错误，责任在服务端，如：服务端抛出异常，路由出错，HTTP版本不支持等
		6. [状态码大全](https://cloud.tencent.com/developer/chapter/13553)

## 002 servlet

### 01 入门
1. 创建web项目，导入Servlet依赖坐标
	```html
		<dependency>
			<groupld>javax.servlet</groupld>
			<artifactld>javax.servlet-api</artifactld><version>3.1.0</version>
			<scope>provided</scope>
		</dependency>
	```

2. 创建：定义一个类，实现Servlet接口，并重写接口中所有方法，并在 service方法中输入一句话
	```java
		public class ServletDemo1 implements Servlet(
		public void service(){
			System.out.println("servlet hello world~");
		}
	```

3. 配置：在类上使用@WebServlet 注解，配置该Servlet的访问路径
	@WebServlet("/demo1")
	public class ServletDemo1 implements Servlet {

4. 访问：启动Tomcat，浏览器输入URL访问该Servlet
	hnttp://localhost:8080/web-demo/demo1

### 02 servlet 生命周期
* Servlet运行在Servlet容器(web服务器)中，其生命周期由容器来管理，分为4个阶段：
1. 加载和实例化：默认情况下，当servlet第一次被访问时，由容器创建Servlet对象
2. 初始化：在Servlet实例化之后，容器将调用Servlet的init(方法初始化这个对象，完成一些如加载配置文件、创建连接等初始化的工作。该方法只调用一次
3. 请求处理：每次请求Servlet时，Servlet容器都会调用Servlet的service(）方法对请求进行处理。
4. 服务终止：当需要释放内存或者容器关闭时，容器就会调用Servlet实例的destroy()方法完成资源的释放。在destroy()方法调用之后，容器会释放这个Servlet实例，该实例随后会被Java的垃圾收集器所回收
### 03 方法
1. getservletInfo
2. ServletConfig
### 04 urlpattern 配置

1. 精确匹配:
	配置路径：@webServlet("/user/select")
	访问路径：localhost:8080/web-demo/user/select
2. 目录匹配：
	配置路径：@WebServlet("/user/星号“)
	访问路径:
	* localhost8080/web-dem/user/aaa
	* localhost:8080/web-demo/user/bbb
3. 扩展名匹配:
	配置路径：@WebServlet("星号.do")
	访问路径:
	* localhost:8080/web-demc/aaa.do
	* localhost:8080/web-demo/bbb.do
4. 任意匹配.
	配置路径：
	* @webservlet("/")
	* @WebServlet("/星号")
	访问路径
	* localhost:8080/web-demo/hehe
	* localhost:8080/web-demo/other
### 05 request
#### 1 继承体系
1. servletrequest
2. httpservletrequest
3. servletfacade
#### 2 获取请求数据
1. 请求行：GET/request-demo/req1?username=zhangsan HTTP/1.1
	* String getMethodO：获取请求方式：GET	  ```
	* String getContextPathO：获取虚拟目录(项目访问路径)：/request-demo
	* StringBuffer getRequestURLO:获取URL(统一资源定位符)：http://localhost:8080/request-demo/req1
	* String getRequestURI()：获取URI(统一资源标识符)：/request-demo/req1
	* String getQueryString():获取请求参数（GET方式）：username=zhangsan&password=123
	```java
	String method = req.getMethod();  
	System.out.println(method);  
		  
	String ContextPath = req.getContextPath();  
	System.out.println(ContextPath);  
		  
	StringBuffer URL = req.getRequestURL();  
	System.out.println(URL.toString());  
		  
	String URI = req.getRequestURI();  
	System.out.println(URI);  
		  
	String QueryString = req.getQueryString();  
	System.out.println(QueryString);
	```
2. 请求头：User-Agent: Mozilla/5.0 Chrome/91.0.4472.106
	String getHeader(String name）：根据请求头名称，获取值
	```java
	String agent = req.getHeader("user-agent");  
	System.out.println(agent);
	```
3. 请求体：username=superbaby&password=123
	ServletinputStream getinputStream()：获取字节输入流
	BufferedReader getReader()：获取字符输入流
	```java
	BufferedReader br = req.getReader();  
	String line = br.readLine();  
	System.out.println(line);
	```
4. 
#### 3 通用方式获取请求参数
#### 4 请求转发

### 06 response


#### 2 重定向

