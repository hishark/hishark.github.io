---
title: Room Database Viewer
date: 2020-05-01 01:18:15
tags:
- Android
- Room
- Database
categories: 学习笔记
authors:
- hishark777
---
Android已经有很多基于SQLite的第三方ORM框架，比如GreenDao、LitePal、OrmLite等等，而Google又在2017年推出了亲儿子Room——在SQLite上提供了一个抽象层，以便在充分利用SQLite的强大功能的同时，能够流畅地访问数据库。于是Android本地数据的可选储存方案又多了一个。

纠结了三分钟之后还是选了Room来保存本地数据，那么随之而来有一个新的问题，如何方便的查看数据库里的数据？

查了一大堆之后选定了两个比较好用的工具——Stetho和Android Debug Database。
<!--more-->

## 1. Stetho

Github: https://github.com/facebook/stetho

Stetho是Facebook开发的工具，功能还是非常强大的，具体使用方法README里说得很清楚。

如果按照教程做完了还是没用，检查一下是否在Application里对Stetho进行了初始化。

## 2. Android Debug Database

Github: https://github.com/amitshekhariitbhu/Android-Debug-Database

如果按照教程做完了还是没用，打开终端输入`adb forward tcp:8080 tcp:8080`，再访问http://localhost:8080 就ok了。

## 3. 注意⚠️

不管是Stetho还是Android Debug Database，二者的共同点就是不能自定义Room Database的路径。由于我之前自定义了路径，导致使用这两个都没法取到数据库，坑了我好一会儿。

像下面这样就是只指定了数据库的名字，没有自定义路径，是可行的。

```java
String DB_NAME = "xxx-db";
Room.databaseBuilder(context, AppDatabase.class, DB_NAME)
                .fallbackToDestructiveMigration()
                .allowMainThreadQueries()  
                .build();  
```

像下面这样就是自定义了数据库的存储路径，最终导致取不到数据库的数据。

```java
String DB_NAME = "xxx-db";
String DB_PATH = String.format("%s/%s",Environment.getExternalStorageDirectory().getAbsolutePath(), DB_NAME);
Room.databaseBuilder(context, AppDatabase.class, DB_PATH)
                .fallbackToDestructiveMigration()
                .allowMainThreadQueries()
                .build();
```

## 4. 总结

虽然Stetho在Github的Star更多，但是我个人还是更喜欢ADD，毕竟界面好看就很吸引本颜狗了哈！还能直接修改、删除数据，Debug效率蹭蹭往上涨📈。

## 5. 参考

- https://stackoverflow.com/questions/44429372/view-contents-of-database-created-with-room-persistence-library
- https://developer.android.com/training/data-storage/room?hl=zh-cn