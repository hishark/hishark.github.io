---
title: Struts-CURD
date: 2018-03-09 15:33:53
tags: 
- Struts
categories: 
- 学习笔记
thumbnail:
---
CURD教你做人
<!--more-->

#### CURD之R--查询

1. 创建一个Javabean--Book。
2. 创建一个接口Bookservice，在接口中定义一个得到所有图书的抽象方法。
3. 业务逻辑层M：创建一个实现接口的类。BookServiceImp，在该类中实现上面定义的抽象方法，得到所有图书。 
4. 控制层C：创建一个Action-BookManagementAction，拦截器会自动通过get、set方法取得、设置数据。定义一个方法，jsp调用时就将数据显示到jsp。 
5. 记得在struts.xml中配置action。（name,method）
6. 在jsp中设置一个按钮，点击即可查询出所有图书并显示出来。

#### CURD之U--增

1. 在接口中定义一个添加图书的抽象方法
2. 在BookServiceImp类中实现上面定义的抽象方法，实现添加一本图书。
3. 在Action中定义一个方法，在其中调用BookServiceImp中的添加图书方法即可。
4. 在struts.xml中配置action。(配置name,method)
5. 在BookAdd.jsp表单的action属性中填入AddBook。

#### CURD之U--删除

##### 删除一本图书

1. 在接口中定义一个删除图书的抽象方法。
2. 在BookServiceImp类中实现上面定义的抽象方法，实现删除一本图书。
3. 在BookManagementAction中定义一个方法，在其中调用BookServiceImp中的删除图书方法即可。还要定义一个变量bookId用于存储待删除图书的Id。
4. 在struts.xml中配置action。（需求是删除后立马显示当前图书列表所以记得将result的type设置为chain）
5. `<a href='<s:url action="bookDelete"><s:param name="bookId" value="bookId"/></s:url>'>Delete</a>`以获取想要删除的图书的bookId，则点击Delete链接时调用action——bookDelete。

##### 删除多本图书

1. 在BookManagementAction中定义一个方法，在其中循环调用BookServiceImp中的删除图书方法即可。还要定义一个数组bookIds[]用于存储待删除图书的Id。
2. 在struts.xml中配置action。（需求是删除后立马显示当前图书列表所以记得将result的type设置为chain）
3. 选中一个checkbox就获得一个bookId。↓
```jsp
<!-- 用户选中的bookId全部放入bookIds -->
<td><input type="checkbox" name="bookIds" value='<s:property value="bookId"/>'></td>
<td><s:property value="isbn" /></td>
<td><s:property value="title" /></td>
<td><s:property value="price" /></td>
```
4. 修改提交表单时调用action——bookDeletes。`<s:form theme="simple" action="bookDeletes">`

#### CURD之U--修改

1. 修改需要两个action——bookLoad和bookUpdate。
2. 点击Edit时调用bookLoad获取选中图书的信息并显示出来。别忘了这句`<a href='<s:url action="bookLoad"><s:param name="bookId" value="bookId"/></s:url>'>Edit</a>`，不然获取不到选中的bookId。
3. 修改完成后，提交表单时再调用bookUpdate更新图书信息。

---
*<font color='#FF8C00'>ResultSet</font>*
数据库结果集的数据表，通常通过执行查询数据库的语句生成。
*<font color='#FF8C00'>href写绝对路径</font>*
`<a href='/15Struts2-09-curd/curd/BookList.jsp'>return</a>`
*<font color='#FF8C00'>数据setget</font>*
拦截器在action中拦截数据
*<font color='#FF8C00'>href嵌套s:url</font>*
`<a href='<s:url action="bookList"></s:url>'>返回</a>`
*<font color='#FF8C00'>hidden隐藏</font>*
`<s:hidden name="book.bookId"></s:hidden>`