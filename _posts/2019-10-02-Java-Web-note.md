---
layout:     post
title:      "Java Web"
subtitle:   ""
date:       2019-10-02
author:     "LiuBiyongge"
header-img: "img/in-post/Web.png"
tags:

  - Java Web
---
# Java Web

[TOC]

## HTLM

- 标签
  - 单标签
  - 双标签
  - 标签属性
  - 大小写不敏感

## JavaScript

- Java script运行在客户端

```html
<script type="text/javascript"> </script>
<script language = "javascript"> </script>
```

code.js

```javascript
window.alert("...")	
```

```javascript
<script src="code.js" type="text/javascript"> </script>
```

## JSP

- JSP运行服务器端

### JSP注释

- 发送给客户端的注释

```jsp
<!-- 注释内容 -->
```

- 程序员看的注释

```jsp
<%-- 注释内容 --%>
<%// 注释内容%>
<%/* 注释内容*/%>
```

### JSP表达式

定义JSP的一些输出

```jsp
<% =变量/返回值/表达式 %>		
```

### JSP程序段

<%Java代码%>

**注意：**不能再JSP程序段中定义函数。

### JSP声明

变量必须先声明后使用

```jsp
<%! 代码 %>全局变量声明,会被优先执行
```

### URL传值

```
request.getParameter("m")
```



### JSP指令

告诉JSP引擎对JSP页码如何编译

```jsp
<%@ 指令类别 属性1="属性值1" ... %>
```

- page

控制页码属性，导入包，设置错误页面

- include

插入外部文件

```jsp
<%@ include file="文件名" %>
```



- taglib

### JSP动作

使用XML语法格式来标记控制服务器的行为。

```
<jsp:动作名 属性1="属性值1" ... />
```

| 动作        | 解释 |
| ----------- | ---- |
| include     |      |
| forward     |      |
| useBean     |      |
| setProperty |      |
| getProperty |      |
| plugin      |      |

与前面include的区别为:

- 只会把文件的输出包括进来
- 自动检查被包含文件的变化

## 表单开发

### 定义表单

```html
<form action="page.jsp" method="post">
    请输入你的账号:<input name="account" type="text"><BR>
    请输入你的密码:<input name="password" type="password"><BR>
    <input type="submit" value="登录">
</form>		
```

### 获取单一数据

```
request.getParameter("名称")
```

### 同时获取多个数据

```
String[] = request.getParameterValues("名称")
```

### 隐藏表单中的数据

不会再网页中希纳是出来

```jsp
<input type="hidden" name="number" value="<%=number%>">
```

### JSP访问数据库

- java.sql.Connection
- java.sql.Statement
- java.sql.ResultSet

```java
import java.sql.Connecton;
import java.sql.DriverManager;
import java.sql.Statement;

Class.forName("com.mysql.cj.jdbc.Driver");
Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306?serverTimezone=UTC,"password");

Statement stat = conn.createStatement();
stat.executeQuery(SQL语句);
stat.executeUpdate(SQL语句);

stat.close();
conn.close();
```

```java
String sql = "insert into t_student(stuno, stuname, stusex) values(?,?,?)";
PreparedStatement ps = conn.prepareStatement(sql);
ps.setString(1, stuno);
ps.setString(2, stuname);
ps.setString(3, stusex);
ps.executeUpdate();
```

- 事务

### JSP内置对象

- out

| function            |                                                              |
| ------------------- | ------------------------------------------------------------ |
| close()             | 关闭输出流。                                                 |
| clearBuffer()       | The clearBuffer method of out object is used to clear the output buffer. This method does not write any contents to the client. |
| clear()             | As the name implies, the clear method of out object is used to clear the output buffer. This method does not write any contents to the client. An exception is thrown by this method if the buffer was flushed. |
| int getRemaining()  | 获取缓冲区剩余空间的大小                                     |
| flush()             | 输出缓冲区中的数据。                                         |
| int getBufferSize() | 获取缓冲区的大小。缓冲区的大小可用<%@ page buffer="size" %>设置。 |

The only difference between the clear method of out object and clearBuffer method is
clear method throws an exception when the buffer is flushed.
clearBuffer method does not throw an exception when the buffer is flushed.
General syntax of clearBuffer method of out object is as follows:
out.clearBuffer();

- request

| Method                                   | Description                                                  |
| :--------------------------------------- | :----------------------------------------------------------- |
| Cookie[] getCookies()                    | Returns an array containing all of the Cookie objects the client sent. |
| Enumeration getAttributeNames()          | Returns an Enumeration containing the names of the attributes for this request. |
| Enumeration getHeaderNames()             | Returns an enumeration of all the header names.              |
| Enumeration getParameterNames()          | Returns an Enumeration of String objects containing the names of the parameters |
| HttpSession getSession()                 | Returns the current session. If the request does not have a session, creates a new one and return. |
| HttpSession getSession(boolean create)   | Returns the current HttpSession or, if there is no current session and create is true, returns a new session. |
| Locale getLocale()                       | Returns the preferred Locale for the client, based on the Accept-Language header |
| Object getAttribute(String name)         | Returns the value of the named attribute, or null if no attribute for the given name. |
| ServletInputStream getInputStream()      | Retrieves the body of the request as binary data using a ServletInputStream. |
| String getAuthType()                     | Returns the name of the authentication scheme used to protect the servlet, for example, "BASIC" or "SSL," or null. |
| String getCharacterEncoding()            | Returns the name of the character encoding.                  |
| String getContentType()                  | Returns the MIME type, or null if the type is not known.     |
| String getContextPath()                  | Returns the portion of the request URI that indicates the context of the request. |
| String getHeader(String name)            | Returns the value of the specified request header as a String. |
| String getMethod()                       | Returns the name of the HTTP method, for example, GET, POST, or PUT. |
| String getParameter(String name)         | Returns the value of a request parameter as a String, or null if the parameter does not exist. |
| String getPathInfo()                     | Returns path information associated with the URL the client sent. |
| String getProtocol()                     | Returns the name and version of the protocol for the request. |
| String getQueryString()                  | Returns the query string contained in the request URL after the path. |
| String getRemoteAddr()                   | Returns IP address of the client.                            |
| String getRemoteHost()                   | Returns the fully qualified name of the client.              |
| String getRemoteUser()                   | Returns the login of the user, or null if the user has not been authenticated. |
| String getRequestURI()                   | Returns request's URL from the protocol name up to the query string. |
| String getRequestedSessionId()           | Returns the session ID                                       |
| String getServletPath()                  | Returns request's URL that calls the JSP.                    |
| String[] getParameterValues(String name) | Returns String arrays containing all of the values the given request parameter has |
| boolean isSecure()                       | Returns a boolean indicating if the request is from a secure channel, such as HTTPS. |
| int getContentLength()                   | Returns the length, in bytes, of the request, or -1 if the length is not known. |
| int getIntHeader(String name)            | Returns the value of the specified request header as an int. |
| int getServerPort()                      | Returns the port number on which this request was received.  |

- response

`response.sendRedirect(目标页码地址)`告诉客户端去请求哪一个地址，相当于客户端重新请求一遍。地址显示框会变。不能跨页面共享数据,可以跨站点请求页码

`<jsp:forward>·服务器直接直接访问目标地址发送给客户端，客户端地址显示框不变。可以跨页面共享数据，不能跨站点请求数据

- session

跨页面保持，对于同一个网站，不管在哪个页面，session都相同。

```java
session.SetAttribute(String name, Object obj);		
session.getAttribute(String name);
session.removeAttribue(String name);
String session.getId();
```



- application

所有用户共同使用一个application对象。

```
application.setAttribute(String name, Object obj);
application.getAttribute(String name);
application.removeAttribue(String name);
```



- exception
- page
- pageContext
- config

### Cookie

由服务器发给客户端的小文本数据，保存在客户端的某个目录下。

```java
Cookie cookie = new Cookie(属性, 内容);
cookie.setMaxAge(600);
response.addCookie(cookie)

Cookie[] cookies = request.getcookies();
cookies[i].getName();
cookies[i].getValue();
```

## Servlet

web.xml

```
    <!-- 设置全局参数 -->
    <context-param>
    	<param-name>encoding</param-name>
    	<param-value>gb2312</param-value>
    </context-param>
    <servlet>
        <servlet-name>WelcomeServlet</servlet-name>
        <servlet-class>servlets.WelcomeServlet</servlet-class>
        <~-- 设置局部参数 -->
        <init-param>
            <param-name>driverClassName</param-name>
            <param-value>abcd</param-value>
        </init-param>
    </servlet>
    <servlet-mapping>
        <servlet-name>WelcomeServlet</servlet-name>
        <url-pattern>/servlets/WelcomeServlet</url-pattern>
    </servlet-mapping>
        <welcome-file-list>
        <welcome-file>welcome.jsp</welcome-file>
    </welcome-file-list>
    
```

- init()
- doGet()
- doPost()
- service()
- destroy()

```java
PrintWriter out = response.getWriter();//获得out对象
//request response
HttpSession session = request.getSession();//获得session对象
ServletContext application = this.getServletContext();//获得application对象
response.sendRedirect("URL地址");//重定向
RequestDispatcher rd = application.getRequestDispatcher("URL地址");//服务器内跳转
rd.forward(request, response);
application.getInitParameter("参数名称");//获取全局参数
this.getInitParameter("参数名称");//获取局部参数
```

### 过滤器

一种只需要在web.xml文件中配置就能对JSP、HTML和Servlet文件进行过滤。

```
javax.servlet.Filter;
public void init(FilterConfig config);
public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain);
```

```
public class EncodingFilter implements Filter{
	public void init(FilterConfig config) throws ServletException{}
	public void destroy(){}
	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain){
		request.setCharacterEncoding("gb2312");
		chain.doFilter(request, response);
	}
}
```

```
<filter>
	<filter-name>EncodingFilter</filter-name>
	<filter-class>filter.EncodingFilter</filter-class>
</filter>
<filter-mapping>
	<filter-name>EncodingFilter</filter-name>
	<url-pattern>/*</url-pattern>
</filter-mapping>
```

### 异常处理

```
<%@ page language="java" pageEncoding="gb2312" isErrorPage="true"%>
<html>
<body>
对不起，你操作错误
</body>
</html>
```

```
<error-page>
	<exception-java> java.lang.Exception</exception-java>
	<location>/error.jsp</location>
</error-page>
```

## JSP和JavaBean

JavaBean可以控制逻辑、值、数据库访问和其它对象进行封装。

(1) 通过getter和setter方法来读/写变量的值，对应变量首字母必须大写.

(2)属性名称由getter和setter方法决定

```
public class Student {
    private String stuno;
    private String stuname;

    public String getStuno() {
        return stuno;
    }

    public void setStuno(String stuno) {
        this.stuno = stuno;
    }

    public String getStuname() {
        return stuname;
    }
    public void setStuname(String stuname){
        this.stuname = stuname;
    }
}
```

(3) 给bool类型设置属性，getter改为is方法



- 定义

```
<%
	Student student = new Student();
%>
```

```
<jsp::useBean id="idName" class="package.class" scope="page|session|...">
//page 实例化的页面
//request forward跳转页面
//session 用户所有访问页面
//application 所有用户
```

- 设置属性

```
<%
	student.setStuname("张华")
%>
```

```
<jsp::setProperty property="stuname" name="student" value="张华">
```

- 获得属性

```
<%
	student.getStuname("张华")
%>
```



```
<jsp::getProperty property="stuname" name="student">
```

### DAO(Data Access Object) and VO(Value Object)

