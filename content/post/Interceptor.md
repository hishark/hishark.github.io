---
title: Interceptor
date: 2018-03-14 09:00:54
tags:
- Struts
categories: 
- 学习笔记
thumbnail:
---
#### 拦截器流程概览
<!--more-->

##### 定义一个自定义拦截器MyInterceptor实现Interceptor接口

```java
/*
 * 拦截器需要定义 
 * 默认的那些拦截器都定义在struts-default.xml中 
 * 自定义拦截器要去struts.xml中定义
 */
public class MyInterceptor implements Interceptor {

	@Override
	public void destroy() {
		// TODO Auto-generated method stub

	}

	@Override
	public void init() {
		// TODO Auto-generated method stub

	}

	@Override
	public String intercept(ActionInvocation action) throws Exception {
		// TODO Auto-generated method stub
		String str = "";

		// 执行action之前
		System.out.println("before action...");

		/*
		 * 进入action 唤醒action
		 * 此时系统流程进入action
		 * action中execute方法返回的字符串赋给这里的str
		 */
		str = action.invoke();

		// 执行action之后
		System.out.println("after action...");

		// str返回到struts.xml中根据action的result进行匹配
		return str;
	}

}
```

##### 在struts.xml中定义拦截器

```xml
<!-- 定义自定义的拦截器 -->
<interceptors>
	<interceptor name="MyInterceptor" class="interceptor.MyInterceptor"/>
</interceptors>
```

##### 创建一个action来进行拦截器测试

```java
import com.opensymphony.xwork2.ActionSupport;

public class InterceptorTestAction extends ActionSupport {
	@Override
	public String execute() throws Exception {
		// TODO Auto-generated method stub
		String str = "succ";
		System.out.println("in action...");
		return str;
	}
}
```

##### 在struts.xml中定义action

```xml
<action name="InterceptorTest" class="jxnu.edu.cn.x3321.action.InterceptorTestAction">
	<!-- 在想要插入拦截器的action中加上下一句 -->
	<interceptor-ref name="MyInterceptor" />
	<!-- 还要指定系统必需的拦截器栈 -->
	<interceptor-ref name="defaultStack" />
	<result name="succ">/login/login.jsp</result>
	<result name="fail">/login/error.jsp</result>
</action>
```

##### 调用InterceptorTestAction

<center>![](https://ws1.sinaimg.cn/large/0068SXX6gy1fpc2uyze19j304n01oq2p.jpg)</center>
<br>
#### 拦截器简单应用

>实际上应该在User表里定义一个Role字段来判断用户的角色，这里为了应用演示就简化为直接通过用户名来判断用户角色。

##### 先在LoginAction中定义一个session来存储登录的用户名

```java
Map<String,Object> session = ActionContext.getContext().getSession();
session.put("role", user.getUserName());
```

##### 创建一个自定义的权限判断拦截器

```java
public class InterceptorPower implements Interceptor {

	@Override
	public void destroy() {
		// TODO Auto-generated method stub

	}

	@Override
	public void init() {
		// TODO Auto-generated method stub

	}

	// 分调用之前、调用action、调用之后
	// 组件化 即插即用 可扩展性可维护性很强
	@Override
	public String intercept(ActionInvocation arg0) throws Exception {
		// TODO Auto-generated method stub
		String str = "";// 接受从action传来的字符串
		String role = "";// 角色
		
		// 从session中取得角色
		role = (String) ServletActionContext.getRequest().getSession().getAttribute("role");

		//判断是否是合法用户
		if (role != null && !role.equals("")) {
			//这里假设小添添是管理员哈哈哈哈哈哈
			if(role.equals("zzm")) {
				//唤醒action
				str = arg0.invoke();
			}else {
				System.out.println("你不是管理员别瞎按！");
				//记得在struts.xml中配置powerfail的result
				str = "powerfail";
			}
		}else {
			System.out.println("请登录！");
			//记得在struts.xml中配置loginfail的result
			str = "loginfail";
		}

		return str;
	}

}
```

##### 在struts.xml中配置拦截器

```xml
<action name="book_*" class="jxnu.edu.cn.x3321.action.BookManagementAction" method="{1}">
	<!-- 添加图书时需要进行用户权限判断 所以加上一个拦截器 -->
	<interceptor-ref name="InterceptorPower" />
	<!-- 系统缺省的拦截器栈别忘了加 -->
	<interceptor-ref name="defaultStack" />

	<result name="AddBookSucc" type="redirect">/curd/BookAdd.jsp</result>
	<result name="AddBookFail">/curd/error.jsp</result>

	<!-- 这里记得配置 -->
	<result name="loginfail">/login/login.jsp</result>
	<result name="powerfail">/login/login.jsp</result>
</action>
```
