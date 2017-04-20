# request
## post/get接收请求
```
<%
request.setCharacterEncoding("UTF-8");//无法解决get传递中文乱码问题
%>
<% 
out.print("用户名:"+request.getParameter("name")+"<br/>");
out.print("密码:"+request.getParameter("password"+"<br/>"));
out.print("爱好有:");
String habit[]=request.getParameterValues("habit");
if(habit!=null){
	for(String string:habit){
		out.print(string);
		if(string.equals(habit[habit.length-1]))out.print("。");
		else out.print("、");
	}
}
%>
```
其中以解决post传递中文乱码问题，而get传递中文乱码需要修改tomcat配置中的server.xml里和修改端口同一个地方,只需添加  **URIEncoding="utf-8"**
```
<Connector connectionTimeout="20000" port="8080" protocol="HTTP/1.1" redirectPort="8443" URIEncoding="utf-8"/>
```
## 重定向与转发
重定向
```
request.getRequestDispatcher("/index.jsp").forward(request, response);
```
```
resp.sendRedirect(req.getContextPath()+"/index.jsp");
```
转hua
```
response.sendRedirect(request.getContextPath()+"/request"+"/redirect.jsp");
```
# session
## session设置登录超时时间
### web.xml设置
```
<session-config>
		<session-timeout>1</session-timeout>
	</session-config>
```
Tomcat提供的web.xml里已有session-config,可修改
### jsp中设置	
```
session.setMaxInactiveInterval(10);//设置session过期时间为10秒，过期后session存储信息丢失
```
## 利用session传递不同页面信息
存储键值
```
SimpleDateFormat simpleDateFormat=new SimpleDateFormat("YY年MM月dd日 HH:mm:ss");
	Date date=new Date(session.getCreationTime());
	String time=simpleDateFormat.format(date);
	session.setAttribute("time","time");
```
提取键值或键值名集合
```
session.getAttribute("time");
//键值名集合
String[] attributes=session.getValueNames();
for(String string:attributes){
	out.print(string+":"+session.getAttribute(string)+"<br/>");
}
```
# pageContext
## pageContext转HUA和包含
pageContext主要作用应该是包含include
```
<%
	//pageContext.forward("../index.jsp");//页面跳转
	//pageContext.include("../index.jsp");//页面包含
%>
```
## pageContext获取不同页面session数据
好像没什么卵用，可以直接session.getAttribute("username");
```
pageContext能获取整个session周期 存储的属性<br/>
pageContext包含的session用户名为<%=pageContext.getSession().getAttribute("username")%>
```


# Application
application开始于服务器启动，结束于服务器关闭，类似java中的静态变量
可用于不同session的数据传递
## 利用Application传递数据
application存储键值
```
application.setAttribute("counter",0);
```
获取存储键值整型并转为整型
```
int number=Integer.parseInt(application.getAttribute("counter").toString());
```
枚举服务器所有属性
```
Enumeration attributes=application.getAttributeNames();
while(attributes.hasMoreElements()){
	out.print(attributes.nextElement()+"&nbsp;");
	out.print("<br/>");
}
```
## Application存储的服务器信息
```
out.print("JSP(SERVLET)引擎名及版本号:"+application.getServerInfo()+"<br/>");
```
# exception
设置错误页面:errorPage="exception.jsp"
```
<%@ page errorPage="exception.jsp"%>
<%
	out.print(1/0);
%>
```

设置接收错误页面
```
<%@ page isErrorPage="true"%>
错误信息为:
<%=exception.getMessage() %><br/>
错误信息tosting为:
<%=exception.toString() %><br/>
```
# javabean(java的属性种子)
## javabean初始化
减少代码冗余
一个学生属性种子
```
public class Student{
	private String name;
	private int age;
	public void setName(String name){
		this.name=name;
	}
	public String getName(){
		return name;
	}
	public void setAge(int age){
		this.age=age;
	}
	public int getAge(){
		return age;
	}
}
```
## javabean普通使用
```
<%
Student student=new Student(); 
student.setName("小明");
%>
学生姓名:<%=student.getName()%>
```
## useBean动作使用
都需要先定义一个对象student_useBean
```
<jsp:useBean id="student_useBean" class="bean.Student" scope="page" />
```
### useBean两种普通赋值/getProperty
```
<%
student_useBean.setName("小光");
%>
useBean学生姓名:<%=student_useBean.getName()%><br/>
<jsp:setProperty name="student_useBean" property="name" value="小光"/>
getProperty获取学生姓名：<jsp:getProperty name="student_useBean" property="name"/><br>
```
### useBean根据表单赋值
```
<jsp:setProperty name="student_useBean" property="*"/> 
```
表单:
```
<form name="loginForm" action="javaBean.jsp" method="post">
    <table>
      <tr>
        <td>name：</td>
        <td><input type="text" name="name" value=""/></td>
      </tr>
      <tr>
        <td>age：</td>
        <td><input type="text" name="age" value=""/></td>
      </tr>
      <tr>
        <td colspan="2" align="center"><input type="submit" value="登录"/></td>
        
      </tr>
    </table>
</form>
```
### useBean通过URL传参赋值
```
<jsp:setProperty name="student_useBean" property="name"/>//获取键值名为name的键值
<jsp:setProperty name="student_useBean" property="age" param="myAge" />//获取键值名为myAge的键值
url传参:<br/>
name:<%=student_useBean.getName()%><br/>
age:<%=student_useBean.getAge()%><br/>
```
表单:
```
<form name="loginForm" action="javaBean.jsp?name=小张&myAge=12" method="post">
<input type="submit" value="登录"/>
</form>
```
### 总结
总结以上
**get表单是将form中的参数转为url传参
post表单是将form中的参数转为body中的键值对**
所以
setProperty原理都是获取数据包为:
**HEADERS:Content-Type为空(默认application/x-www-form-urlencoded)
url参数或BODY中的键值名name和myAge的键值(如果重复优先url参数)**
无论post or get

即数据包形势为
发送包
```
POST /Practice/javaben/javaBean.jsp?myAge=12 HTTP/1.1
Host: localhost:8080
Content-Type: application/x-www-form-urlencoded
Content-Length: 12

name=1&age=1
```

返回包:
```
HTTP/1.1 200 OK
Server: Apache-Coyote/1.1
Content-Type: text/html;charset=UTF-8
Content-Length: 397
Date: Sat, 11 Mar 2017 03:09:00 GMT



<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
JAVA普通形式<br/>

学生姓名:小明<br/>


useBean学生姓名:小光<br/>



url传参:<br/>
name:1<br/>
age:12<br/>
</body>
</html>
```
### useBean四种作用范围
#### aplication:
```
<jsp:useBean id="student_useBean" class="bean.Student" scope="application" />
```
```
用户名：<%=((Student)application.getAttribute("student_useBean")).getName()%><br>
       密码：<%=((Student)application.getAttribute("student_useBean")).getName() %><br>
```
#### session
```
<jsp:useBean id="student_useBean" class="bean.Student" scope="session" />
```
```
用户名：<%=((Student)session.getAttribute("student_useBean")).getName()%><br>
       密码：<%=((Student)session.getAttribute("student_useBean")).getName() %><br>
```
#### request
```
<jsp:useBean id="student_useBean" class="bean.Student" scope="request" />
```
```
用户名：<%=((Student)request.getAttribute("student_useBean")).getName()%><br>
       密码：<%=((Student)request.getAttribute("student_useBean")).getName() %><br>
```
#### page
```
<jsp:useBean id="student_useBean" class="bean.Student" scope="page" />
```
```
用户名：<%=((Student)pageContext.getAttribute("student_useBean")).getName()%><br>
       密码：<%=((Student)pageContext.getAttribute("student_useBean")).getName() %><br>
```
# Cookie
## Cookie存储
以下代码用Cookie保存用户名密码，或取消Cookie保存
```
//首先判断用户是否选择了记住登录状态
       String[] isUseCookies = request.getParameterValues("isUseCookie");
       if(isUseCookies!=null&&isUseCookies.length>0)
       {
          //把用户名和密码保存在Cookie对象里面
          String username = URLEncoder.encode(request.getParameter("username"),"utf-8");
          //使用URLEncoder解决无法在Cookie当中保存中文字符串问题
          String password = URLEncoder.encode(request.getParameter("password"),"utf-8");
          
          Cookie usernameCookie = new Cookie("username",username);
          Cookie passwordCookie = new Cookie("password",password);
          usernameCookie.setMaxAge(864000);
          passwordCookie.setMaxAge(864000);//设置最大生存期限为10天
          response.addCookie(usernameCookie);
          response.addCookie(passwordCookie);
       }
       else
       {
          Cookie[] cookies = request.getCookies();
          if(cookies!=null&&cookies.length>0)
          {
             for(Cookie c:cookies)
             {
                if(c.getName().equals("username")||c.getName().equals("password"))
                {
                    c.setMaxAge(0); //设置Cookie失效
                    response.addCookie(c); //重新保存。
                }
             }
          }
       }
```
## Cookie提取
```
request.setCharacterEncoding("utf-8");
      String username="";
      String password = "";
      Cookie[] cookies = request.getCookies();
      if(cookies!=null&&cookies.length>0)
      {
           for(Cookie c:cookies)
           {
              if(c.getName().equals("username"))
              {
                   username =  URLDecoder.decode(c.getValue(),"utf-8");
              }
              if(c.getName().equals("password"))
              {
                   password =  URLDecoder.decode(c.getValue(),"utf-8");
              }
           }
```
# jsp动作
## include
### include指令
```
<%@include file="../index.jsp" %>
```
### include动作
```
<jsp:include page="date.jsp" flush="false"/> <!--flush="false"不从缓冲区读取  -->
```
### 区别
![enter description here][1]
include指令在生成的servlet(也就是java类)中重复被包含java类的内容代码，且只有一个

include动作生成先生成被包含文件的servlet，然后在再生成自身servlet，在自身java类中使用
```
org.apache.jasper.runtime.JspRuntimeLibrary.include(request, response, "date.jsp", out, false);
```
包含内容的结果

## forward
forward转发:
**可以在url中带参数**
```
	<jsp:forward page="user.jsp?username=123"/>
    <!-- <%  request.getRequestDispatcher("user.jsp").forward(request, response);
    %> --><!-- 等价于此代码-->
```

forward携带参数转发:也可以修改参数
**url带参数,url优先**
```
<jsp:forward page="user.jsp?username=123&password=123">
      <jsp:param value="admin@123.net" name="email"/>
      <jsp:param value="888888" name="password"/>
    </jsp:forward>
```
# servlet
web.xml:
```
	<servlet>
		<servlet-name>myServlet</servlet-name>
		<servlet-class>servlet.MyServlet</servlet-class>
	</servlet>
	<servlet-mapping>
	  <servlet-name>myServlet</servlet-name>
	  <url-pattern>/servlet/MyServlet</url-pattern>
	  <load-on-startup>1</load-on-startup><!--服务器启动时直接构造servlet,,且执行init方法数字越小越优先构造-->
	</servlet-mapping>
```
MyServlet.java:
```
package servlet;
import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
public class MyServlet extends HttpServlet{
	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		//super.doGet(req, resp);//需要注释掉
	}
	@Override
	protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
		//super.doPost(req, resp);
	}
}

```
jsp:
```
	<a href="servlet/MyServlet">Get方式请求HelloServlet</a><br>
    <form action="servlet/MyServlet" method="post">
      <input type="submit" value="Post方式请求HelloServlet"/> 
    </form>
```



  [1]: ./images/1489279696654.jpg "1489279696654"