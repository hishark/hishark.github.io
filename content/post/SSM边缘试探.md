---
title: SSM 边缘试探
date: 2018-04-03 20:38:10
tags:
- SSM
categories: 学习笔记
---
SSM真的很好用啊鼓掌！👏

<!--more-->

#### 安装Mysql数据库

MySQL-Front贼好用b（￣▽￣）d　

![](https://ws1.sinaimg.cn/large/0068SXX6gy1fq0wqi52jij30m70fjab6.jpg)

#### 创建动态Web工程

创建一个Dynamic Web Project。

![](https://ws1.sinaimg.cn/large/0068SXX6gy1fq0wt4rtgcj30i10hit9r.jpg)

#### 把jar包导入WEB-INF/lib

![](https://ws1.sinaimg.cn/large/0068SXX6gy1fq0gm9e2vyj30p805xmxn.jpg)

#### 创建bean

该bean和数据库中的表产生映射。

```java
package pojo;

public class Book {
	// 变量名和MySQL数据库中表的字段需一致
	private int BookId;
	private String Isbn;
	private String Title;
	private String Price;

	public int getBookId() {
		return BookId;
	}

	public void setBookId(int bookId) {
		BookId = bookId;
	}

	public String getIsbn() {
		return Isbn;
	}

	public void setIsbn(String isbn) {
		Isbn = isbn;
	}

	public String getTitle() {
		return Title;
	}

	public void setTitle(String title) {
		Title = title;
	}

	public String getPrice() {
		return Price;
	}

	public void setPrice(String price) {
		Price = price;
	}
}
```

#### 创建BookMapper

说明对数据库中表的相关操作

```java
package mapper;

import java.util.List;
import pojo.*;

//可以提供给用户的服务
public interface BookMapper {
	// 得到所有图书
	public List<Book> list();

	// 添加图书
	public void add(Book book);

	// 删除图书
	public void delete(int bookId);

	// 得到一本书
	public Book get(int bookId);

	// 更新图书
	public void update(Book book);
}
```

#### 创建Book.xml

Book.xml将bean与数据库中的表建立关联并实现对数据库的相关操作。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- 需要这个xml来发生映射 -->
<!-- book.xml建立关联并且执行相关操作 -->
<!-- 这个相当于之前用到的DbConnection -->
<!DOCTYPE mapper
         PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
         "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!-- 目录一定要指定 -->
<mapper namespace="mapper.BookMapper">
	<!-- 这里就是所有的映射 1.book和表发生关联 2.book相关操作的sql语句全部在这 -->
	<!-- id和BookMapper里的函数名一致 -->
	<!-- resulttype为数据的返回类型 -->
    <!-- parameterType为输入参数的类型 -->
	<select id="list" resultType="Book">
		select * from book_table
	</select>
    <!-- 取值用#{} -->
	<insert id="add" parameterType="Book">
		insert into book_table(Title,Isbn,Price) values(#{Title},#{Isbn},#{Price})
	</insert>
	<delete id="delete" parameterType="Book">
		delete from book_table where BookId = #{BookId}
	</delete>
	<!-- int前面要加下划线 -->
	<select id="get" parameterType="_int" resultType="Book">
		select * from book_table where BookId = #{BookId}
	</select>
	<update id="update" parameterType="Book">
		update book_table set Isbn = #{Isbn},Title = #{Title},Price = #{Price} where BookId = #{BookId}
	</update>
</mapper>
```

#### 创建BookService接口

业务逻辑层，对外提供的功能。

```java
package service;

import java.util.List;
import pojo.Book;

public interface BookService {
	public List<Book> list();

	// 添加图书
	public void add(Book book);

	// 删除图书
	public void delete(int bookId);

	// 得到一本书
	public Book get(int bookId);

	// 更新图书
	public void update(Book book);
}
```

#### 实现BookService接口

控制器类Controller首先调用这里面的方法，然后这里面的方法又调用BookMapper的方法，最后BookMapper调用Book.xml执行相关SQL操作。

要加上各种注解——Service、Autowired。

注解的好处：比如`@Autowired`主要声明一个引用变量，不需要实例化，spring框架会帮我们实例化，简化了操作。

```java
package serviceImp;

import java.util.List;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import mapper.BookMapper;
import pojo.Book;
import service.BookService;
/* Service注解
 * 告诉spring这是一个实现类（是BookService的实现类）
 * 所以不需要自己实例化啦
 */
@Service
public class BookServiceImp implements BookService {
  
	/* 只需要定义接口的引用变量
	 * spring利用注解进行注入
	 * spring框架可实现自动实例化
	 */
	@Autowired
	BookMapper bookMapper;
	
	@Override
	public List<Book> list() {
		// TODO Auto-generated method stub
		return bookMapper.list();
	}

	@Override
	public void add(Book book) {
		// TODO Auto-generated method stub
		bookMapper.add(book);
	}

	@Override
	public void delete(int bookId) {
		// TODO Auto-generated method stub
		bookMapper.delete(bookId);
	}

	@Override
	public Book get(int bookId) {
		// TODO Auto-generated method stub
		return bookMapper.get(bookId);
	}

	@Override
	public void update(Book book) {
		// TODO Auto-generated method stub
		bookMapper.update(book);
	}
}
```

#### 创建控制器类

Controller通过`@RequestMapping("")`内的操作名接收用户请求。

JSP页面通过操作名调用相关操作，Controller首先调用BookService里的方法，然后BookService里的方法又调用BookMapper的方法，最后BookMapper调用Book.xml执行相关SQL操作。

```java
package controller;

import java.util.List;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.servlet.ModelAndView;
import pojo.*;
import service.BookService;

@Controller//告诉spring mvc这是一个控制器类
@RequestMapping("")//接收用户的请求
public class BookController {
	//不需要new！spring自动实例化。记得加上注解
	@Autowired
	BookService bookService;

	//JSP页面就是通过listBook进行相应的方法调用，这个就相当于structx.xml的action的名字，是一个对外的操作名。
	@RequestMapping("listBook")
	public ModelAndView listBook(){
		ModelAndView mv = new ModelAndView();
		List<Book> cs = bookService.list();
		//把cs带到页面上去
		//mv存放转发的参数（要转发到JSP的数据）
		mv.addObject("cs",cs);
		//放入将要跳转到的JSP文件名，不需要后缀名，配置文件中再进行配置
		mv.setViewName("BookList");
        //return给springMVC框架 然后就会自动匹配跳转页面
		return mv;
	}
  
	@RequestMapping("addBook")
	public ModelAndView addBook(Book book) {
		ModelAndView mv = new ModelAndView();
		bookService.add(book);
		List<Book> cs = bookService.list();
		mv.addObject("cs",cs);
		mv.setViewName("BookList");
	    return mv;
	}
	
	@RequestMapping("deleteBook") 
	public ModelAndView deleteBook(int bookId) {
		ModelAndView mv = new ModelAndView();
		bookService.delete(bookId);
		List<Book> cs = bookService.list();
		mv.addObject("cs",cs);
		mv.setViewName("BookList");
		return mv;
	}
	
  	//编辑图书前要先加载图书信息
	@RequestMapping("loadBook") 
	public ModelAndView loadBook(int bookId) {
		ModelAndView mv = new ModelAndView();
		Book book = bookService.get(bookId);
		mv.addObject("book",book);
		mv.setViewName("BookEdit");
		return mv;
	}
	
	@RequestMapping("editBook") 
	public ModelAndView editBook(Book book) {
		ModelAndView mv = new ModelAndView();
		bookService.update(book);
		List<Book> cs = bookService.list();
		mv.addObject("cs",cs);
		mv.setViewName("BookList");
		return mv;
	}
}
```

#### 编写配置文件

##### applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
	xmlns:aop="http://www.springframework.org/schema/aop"
	xmlns:tx="http://www.springframework.org/schema/tx" 
	xmlns:jdbc="http://www.springframework.org/schema/jdbc"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:mvc="http://www.springframework.org/schema/mvc"
	xsi:schemaLocation="http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context-3.0.xsd 
    http://www.springframework.org/schema/beans 
    http://www.springframework.org/schema/beans/spring-beans-3.0.xsd 
    http://www.springframework.org/schema/jdbc 
    http://www.springframework.org/schema/jdbc/spring-jdbc-3.0.xsd 
    http://www.springframework.org/schema/tx 
    http://www.springframework.org/schema/tx/spring-tx-3.0.xsd 
    http://www.springframework.org/schema/aop 
    http://www.springframework.org/schema/aop/spring-aop-3.0.xsd 
    http://www.springframework.org/schema/mvc 
    http://www.springframework.org/schema/mvc/spring-mvc.xsd ">
	<!-- 1.通过注解，将service的生命周期纳入spring框架进行管理 -->
	<context:annotation-config />
	<context:component-scan base-package="service" />
	<context:component-scan base-package="serviceImp" />
	<!-- 2.配置数据源 -->
	<bean id="dataSource"
		class="org.springframework.jdbc.datasource.DriverManagerDataSource">
		<property name="driverClassName">
			<value>com.mysql.jdbc.Driver</value>
		</property>
		<property name="url">
			<value>jdbc:mysql://localhost:3306/777-ssm?characterEncoding=UTF-8
			</value>
		</property>
		<property name="username">
			<value>root</value>
		</property>
		<property name="password">
			<value>123456</value>
		</property>
	</bean>
	<!-- 3.扫描存放sql语句的Book.xml -->
	<bean id="sqlSession" class="org.mybatis.spring.SqlSessionFactoryBean">
		<property name="typeAliasesPackage" value="pojo" />
		<property name="dataSource" ref="dataSource" />
		<property name="mapperLocations" value="classpath:mapper/*.xml" />
	</bean>
	<!-- 4.扫描Mapper,并将其生命周期纳入spring管理 -->
	<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
		<property name="basePackage" value="mapper" />
	</bean>
</beans>
```

##### springMVC.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:aop="http://www.springframework.org/schema/aop"
	xmlns:tx="http://www.springframework.org/schema/tx" xmlns:jdbc="http://www.springframework.org/schema/jdbc"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:mvc="http://www.springframework.org/schema/mvc"
	xsi:schemaLocation="http://www.springframework.org/schema/jdbc
	 http://www.springframework.org/schema/jdbc/spring-jdbc-3.0.xsd 
	        http://www.springframework.org/schema/aop 
	 http://www.springframework.org/schema/aop/spring-aop-3.0.xsd 
	        http://www.springframework.org/schema/beans 
	 http://www.springframework.org/schema/beans/spring-beans-3.0.xsd 
	        http://www.springframework.org/schema/context 
	 http://www.springframework.org/schema/context/spring-context-3.0.xsd 
	        http://www.springframework.org/schema/tx 
	 http://www.springframework.org/schema/tx/spring-tx-3.0.xsd
	        http://www.springframework.org/schema/mvc 
	 http://www.springframework.org/schema/mvc/spring-mvc-3.2.xsd ">
	<!-- 1.扫描Controller,并将其生命周期纳入spring管理 -->
	<context:annotation-config />
	<context:component-scan base-package="controller">
		<context:include-filter type="annotation"
			expression="org.springframework.stereotype.Controller" />
	</context:component-scan>
	<!-- 2.注解驱动，使得访问路径和方法的匹配可以通过注解进行配置 -->
	<mvc:annotation-driven />
	<!-- 3.静态页面跳转 -->
	<mvc:default-servlet-handler />
	<!-- 视图定位/webContent/curd -->
	<bean
		class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<property name="viewClass"
			value="org.springframework.web.servlet.view.JstlView" />
		<property name="prefix" value="/curd/" />
		<property name="suffix" value=".jsp" />
	</bean>
</beans>
```

##### web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		 xmlns="http://java.sun.com/xml/ns/javaee"
		 xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
		 version="3.0">
	<!-- spring的配置文件 -->
	<context-param><!--全局范围内环境参数初始化 -->
		<param-name>contextConfigLocation</param-name><!--参数名称 -->
		<param-value>classpath:applicationContext.xml</param-value><!--参数取值 -->
	</context-param>
	<listener>
		<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
	</listener>
	<!-- spring mvc核心：分发servlet -->
	<servlet>
		<servlet-name>mvc-dispatcher</servlet-name>
		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
		<!-- spring mvc的配置文件 -->
		<init-param>
			<param-name>contextConfigLocation</param-name>
			<param-value>classpath:springMVC.xml</param-value>
		</init-param>
		<load-on-startup>1</load-on-startup>
	</servlet>
	<servlet-mapping>
		<servlet-name>mvc-dispatcher</servlet-name>
		<url-pattern>/</url-pattern>
	</servlet-mapping>
	<!-- 配置过滤器解决中文乱码问题 -->
	<filter>
		<filter-name>CharacterEncoding</filter-name>
		<filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
		<init-param>
			<param-name>encoding</param-name>
			<param-value>UTF-8</param-value>
		</init-param>
	</filter>
	<filter-mapping>
		<filter-name>CharacterEncoding</filter-name>
		<url-pattern>/*</url-pattern>
	</filter-mapping>
</web-app>
```

#### View层

##### BookList.jsp

```jsp
<%@ page language="java" pageEncoding="utf-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
<head>
<title>图书列表</title>
<style type="text/css">
table {
	border: 1px solid black;
	border-collapse: collapse;
}
table thead tr th {
	border: 1px solid black;
	padding: 3px;
	background-color: #cccccc;
}
table tbody tr td {
	border: 1px solid black;
	padding: 3px;
}
</style>
</head>
<body>
	<div align="center">
		<h4>图书列表</h4>
		<table cellspacing="0">
			<thead>
				<tr>
					<th>Select</th>
					<th>ISBN</th>
					<th>Title</th>
					<th>Price</th>
					<th>Operation</th>
				</tr>
			</thead>
			<tbody>
				<!-- items从Controller的mv传出的cs取值  起个别名为c-->
				<c:forEach items="${cs}" var="c" varStatus="st">
					<tr>
						<td></td>
						<!-- 取值用${} -->
						<td>${c.isbn}</td>
						<td>${c.title}</td>
						<td>${c.price}</td>
						<td>
						<!-- loadBook和deleteBook都是Controller里设置的请求名 ?带参数 -->
						<a href='loadBook?bookId=${c.bookId}'>Edit</a> 
						<a href='deleteBook?bookId=${c.bookId}'>Delete</a>
						</td>
					</tr>
				</c:forEach>
			</tbody>
		</table>
		<a href="/777-SSMBook/curd/BookAdd.jsp">addBook</a>
	</div>
</body>
</html>
```

##### BookAdd.jsp

```jsp
<%@ page language="java" import="java.util.*" pageEncoding="utf-8"%>
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
<head>
<title>增加图书</title>
</head>
<body onload="">
	<div align="center">
		<!-- 指定提交表单时调用addBook执行添加操作 -->
		<form action="/777-SSMBook/addBook" method="post">
			<!-- name这里首字母大小写都可以欸 迷 -->
			Isbn:<input type="text" name="isbn">
			Title:<input type="text" name="title">
			Price:<input type="text" name="price">
			<input type="submit" value="提交">
		</form>
		<!-- 返回就调用listBook显示所有图书啦 -->
		<a href='/777-SSMBook/listBook'>返回 </a>
	</div>
</body>
</html>
```

##### BookEdit.jsp

```jsp
<%@ page language="java" import="java.util.*" pageEncoding="utf-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
<head>
<title>编辑图书</title>
</head>
<body>
	<div align="center">
		<form action="/777-SSMBook/editBook" method="post">
			<!-- value里的book是控制器里的ModelAndView的key值！！——mv.addObject("book",book); -->
			<input type="hidden" name="bookId" value="${book.bookId}">
			Isbn:<input type="text" name="isbn" value="${book.isbn}">
			Title:<input type="text" name="title" value="${book.title}">
			<!-- value取值用book.price和 <c:catch>${book.price}</c:catch>都可以-->
			Price:<input type="text" name="price" value='<c:catch>${book.price}</c:catch>'>
			<input type="submit" value="提交">
		</form>
		<a href='/777-SSMBook/listBook'>返回 </a>
	</div>
</body>
</html>
```

----

#### 杂

##### 踩坑记录

1. bean里面的字段，如果首字母是大写，在JSP中引用的时候首字母一定要改成小写，不然gg。如果字段为BookId，引用的时候一定要写bookId，写bookid也会报错啦，只有首字母需要小写。
2. 表单提交中文乱码[解决方案](https://blog.csdn.net/u013009808/article/details/48325243)，然后再在JSP加上`<%@ page language="java" pageEncoding="utf-8"%>`即可。
3. `Dynamic web module version 3.0` 版本需要匹配，[版本修改方法](https://www.cnblogs.com/2016-10-07/p/7297826.html) 。
4. 找了好久的bug，包名`service.Imp`被我写成了`serviceImp`。写成后者其实也没猫饼，但是没有在`applicationContext.xml`里面把`serviceImp`包纳入spring框架进行管理所以出错啦。如果只注解`service`包的话包名一定要有层级关系啦，如果两个包都注解了就无所谓了OTZ。
5. xml取值用#{}，jsp取值用${}。

##### Unsolved

1. 由于在控制器类里的添加图书操作中设置了将要跳转的JSP页面`mav.setViewName("BookList")`,所以在添加图书后自动跳转到BookList.jsp页面，但是问题出现了，此时浏览器的地址还处在addBook状态，所以如果刷新浏览器就会重复添加图书。
2. 编辑图书出现的问题同上。
3. form表单的name属性添添说是一定要和bean里的变量名统一，但是我bean里是Isbn，name用isbn也没问题啦。反正以后都小写就好了OTZ