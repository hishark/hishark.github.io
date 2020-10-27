---
title: 在 Struts 中应用 Ajax 技术
date: 2018-03-19 14:28:25
tags: 
- Struts
- Ajax
categories: 学习笔记
thumbnail:
---
Ajax在浏览器与Web服务器之间使用了异步数据传输，从而减少了网页向服务器请求的信息量，使得每次请求并不需要返回整个页面。
<!--more-->

#### 一个简单的应用

注册时输入用户名，要检测该用户名是否已被注册。

##### 在\WebContent\WEB-INF\lib中添加jar包
<center>![](https://ws1.sinaimg.cn/large/0068SXX6gy1fpi4a7fbkzj305m00nwe9.jpg)</center>

##### 在jsp中配置库

```jsp
<%@ taglib uri="/struts-tags" prefix="s"%>
<%@ taglib uri="/struts-dojo-tags" prefix="sx" %>
```

##### 添加头部

```jsp
<head>
<meta http-equiv="Content-Type" content="text/html; charset=GB18030">
<title>用户注册</title>
<sx:head/>
</head>
```

##### 添加一个链接
```jsp
<!-- 添加一个链接检查用户是否存在 -->
<s:url id="check" value="checkUser.action"></s:url>

<s:form id="regForm" action="regAction" method="post">
<s:textfield label="用户名" name="user.userName" title="请输入用户名！"/>

<!-- 
	参数含义：
	1.href：提交给哪个action处理，这里即提交给name为checkUser的action处理。
	2.formId：提交的是哪个表单，这里提交id为regForm的表单。
	3.targets：结果返回到哪里，这里就是返回到下面id为receiveResult的盒子里。
-->
<sx:a href="%{check}" formId="regForm" targets="receiveResult">check</sx:a>

<sx:div id="receiveResult" theme="simple"></sx:div>
</s:form>
```

##### UserService接口以及接口的实现

```java
public interface UserService {
	boolean checkUser(User user);
}

public class UserServiceImp implements UserService {
	//从数据库里取数据要用db里的一个查询方法！
	DbConnection db = new DbConnection();
	//取数据先要放到这个里头 利用db查询得到的是一个resultset结果集
	ResultSet rs = null;
	
	@Override
	public boolean checkUser(User user) {
		// TODO Auto-generated method stub
		boolean bl = false;
		String strSql = "select * from user_table where userName=N'"+user.getUserName()+"'";
		rs = db.executeQuery(strSql);
		try {
			while(rs.next()) {
				bl=true;
				break;
			}
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		return bl;
	}

}
```

##### 在RegAction中添加checkUser方法

```java
User user;
String checkUserResult = "";
UserService us = new UserServiceImp();

public String checkUser() {
	String str = "checkDone";
	if(us.checkUser(user)) {
		checkUserResult = "用户名已存在！换一个啦！";
	}else {
		checkUserResult = "用户名不存在！可以使用！";
	}	
	return str;
}
```

##### 在struts.xml中配置checkUser.action

```xml
<action name="checkUser" class="jxnu.edu.cn.x3321.action.RegAction" method="checkUser">
<result name="checkDone">/reg/ajaxResult.jsp</result>
</action>
```

##### ajaxResult.jsp中即可获得checkUserResult的值

```jsp
<s:property value="checkUserResult"/>
```

##### 整个jsp页面将返回到reg.jsp中id为receiveResult的盒子里

<center>![](https://ws1.sinaimg.cn/large/0068SXX6gy1fpi5an2gvoj308a01i3yb.jpg)</center>
<hr>
#### 踩了一些坑

1. struts.xml改动了就要重启服务器。
2. 前面的工程中有写过一个注册校验的功能，检测用户名是否存在时会提交整个表单所以无法通过校验，会报错。
3. 表单提交中文没有正确获得中文，而是获得`&#21834;&#21834;&#21834;`编码，把struts中这一句的gbk换成utf-8即可。
<center>
<div>
~~`<constant name="struts.i18n.encoding" value="gbk"></constant>`~~
`<constant name="struts.i18n.encoding" value="utf-8"></constant>`
</div></center>

