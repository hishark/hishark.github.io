乱七八糟的笔记
<!--more-->

#### 分页

没啥难点
注意几个变量就好

```jsp
<a href='<s:url action="page"><s:param name="pageNow" value="1"/></s:url>'>首页</a> 
<a href='<s:url action="page"><s:param name="pageNow" value="pageNow-1"/></s:url>'>上页</a>
<a href='<s:url action="page"><s:param name="pageNow" value="pageNow+1"/></s:url>'>下页</a>
<a href='<s:url action="page"><s:param name="pageNow" value="pageCount"/></s:url>'>末页</a> 
```
SQL语句注意一哈
```java
@Override
public List<Book> getBookListByPage(int pageNow, int pageSize) {
	// TODO Auto-generated method stub
	List<Book> books = new ArrayList();
	String strSql = "select top "+pageSize+" * from book_table where bookId not in"+ "(select top "+(pageNow-1)*pageSize+" bookId from book_table)";
		
	rs = db.executeQuery(strSql);
	try {
		while(rs.next()) {
			Book book = new Book();
			book.setBookId(rs.getInt("bookId"));
			book.setIsbn(rs.getString("isbn"));
			book.setTitle(rs.getString("title"));
			book.setPrice(rs.getString("price"));
			books.add(book);
		}
	} catch (SQLException e) {
		e.printStackTrace();
	}
	return books;
}
```

#### 通配符

用通配符来代替你的操作名称从而简化struts.xml文档中的配置
```xml
<action name="book_*" class="jxnu.edu.cn.x3321.BookManegementAction" method="{1}">
```
1. 优点：简化
2. 缺点：可读性降低

我还是喜欢分开写啊

>举个栗子🌰

*<font color='#FF8C00'>BoodAdd.jsp</font>*
```jsp
<s:form action="book_add" method="post" >
     <s:textfield name="book.isbn"  label="isbn"></s:textfield>
     <s:textfield name="book.title" label="title"></s:textfield>
     <s:textfield name="book.price" label="price"></s:textfield>
     <s:submit value="增加"></s:submit>
</s:form>
```
*<font color='#FF8C00'>BookManagementAction.java</font>*
```java
public String add() {
	String str = "AddBookFail";
	if (bs.AddBook(book) != 0) {
		str = "AddBookSucc";
	}
	return str;
}
```

#### ORDER BY

之前在jsp页面上添加数据时总是莫名其妙插到表的中间
没有插到最后一行
就很奇怪啊
查来查去查到这位老哥
<center>![](https://ws1.sinaimg.cn/large/0068SXX6gy1fpb5c1hs59j30k005vaab.jpg)</center>
很有道理了> < 
select的时候order一下就很美了
数据库里插到哪里随便了哈哈哈哈哈