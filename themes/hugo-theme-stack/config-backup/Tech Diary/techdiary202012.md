---
title: "Tech Diary | 2020.12"
date: 2020-12-01T08:40:36+08:00
categories: 
- 技术日记
tags:
- TechDiary
draft: false
authors:
- hishark777
description: 最后一个月，支棱起来咯。
---

## 2020-12-30 Wed

### VS Code

[VS-Code-Extension-Doc-ZH](https://github.com/Liiked/VS-Code-Extension-Doc-ZH)

有一个想法，有空了试试看

### IconPark

字节跳动的开源图标库：[http://iconpark.bytedance.com/](http://iconpark.bytedance.com/)

### Hugo

换了个主题发现 html 代码无法渲染了 查了一下配置里加点东西就成了

[Hugo博客中.md文件中嵌入的html代码无法被渲染](https://d.cosx.org/d/421422-hugomdhtml)

hugo 真的比 hexo 好用好多

最喜欢的是 url

实在是受不了 hexo 那个日期拼接的 url 了- -

## 2020-12-29 Tue

### chrome extension

又发现一个好用的插件：[SourceGraph](https://chrome.google.com/webstore/detail/sourcegraph/dgjhfomjieaadpoljlnidmbgkdffpack/related)

比之前找到的那个好用诶

## 2020-12-24 Thu

🎄

### HUAWEI安装app

烦死了老跳出来那个应用安装确认

[如何彻底关闭“外部来源应用检查”，真的很烦](https://club.huawei.com/thread-15131985-1-1.html)

- 安全设置里搞一下
- 开发人员选项里搞一下

成了

## 2020-12-23 Wed

### AS打开崩溃问题

最近每次打开 AS 都会卡死在 [Tip of the day] 那个界面上，而且是全屏卡住OTZ

查到这个终于解决了：[A1ndroid Studio suddenly crashes at startup](https://stackoverflow.com/questions/44239791/android-studio-suddenly-crashes-at-startup)

stackoverflow永远滴神！

### 杂

遇到问题千万不要一个人死磕 谨记

问题抛出去之后往往比你一个人钻牛角尖解决起来快得多🆙

## 2020-12-22 Tue

### DICOM生成问题

> 要相信 Bug总是会一个一个一个的解决的

Bug终于解开了呜呜呜感谢呵呵！呵总永远滴神！

- SAXReader解析xml必须在xml路径前面加上 `file://` 不然解析不到，但是图片路径直接 `/xx/xx` 是ok的

- 以及 `Didn't find class "java.nio.file.Paths" on path:` 是版本问题导致，这个minSdkversion必须要26，然而手上的华为只有24- - 

### okhttp cookie

[Add cookie to client request OkHttp](https://stackoverflow.com/questions/35743291/add-cookie-to-client-request-okhttp)

之前都自定义cookiejar

这次发现个方便的轮子：[PersistentCookieJar](https://github.com/franmontiel/PersistentCookieJar)

用法非常简单，保证 cookieJar 是同一个就可以啦

## 2020-12-21 Mon

### Split

https://www.runoob.com/java/java-string-split.html

记得加转义符啊啊啊啊

### Jar包

[Android Studio导入和删除jar包](https://blog.csdn.net/renwudao24/article/details/69071410)

## 2020-12-19

### AS

[INSTALL_PARSE_FAILED_NO_CERTIFICATES](https://blog.csdn.net/yanghrwork/article/details/103983275)

### Office

[Office 为何不设计 tab 标签？ - 尼欧的回答 - 知乎](https://www.zhihu.com/question/21905040/answer/751983175) 

- 用word就在疑惑为什么不跟WPS设计一个tab，找到了office tab这个完美插件后又发现只支持windows，是我mac不配555
- 看了知乎这个回答之后，妙啊原来藏起来啦。

### 输入法

还是换成了落格

按shift之后光标右下方显示【En】和【中】真是太舒服了

默认的样式也和自带输入法一模一样 太完美噜

用一段时间如果很喜欢的话我就去买个完全版～

[mac 删除自带 ABC 输入法的方法](https://www.jianshu.com/p/0ba1292441b9)

## 2020-12-18

### 自定义view

[HenCoder Android 开发进阶：自定义 View 1-5 绘制顺序](https://hencoder.com/ui-1-5/)

[Android自定义View：MeasureSpec的真正意义与View大小控制](https://segmentfault.com/a/1190000007948959)

### XML

读写以及移动存储位置

[DOM4J解析XML](https://www.freesion.com/article/495782425/)

[Dom4j解析和生成XML文档](https://www.cnblogs.com/yucongblog/p/6588798.html)

[android用流把项目里的xml文件复制到sdcard的方法（含乱码问题）](https://blog.csdn.net/lucherr/article/details/7520122)

[Android复制asset目录的文件到SD卡下](https://blog.csdn.net/u013693649/article/details/61623697)

- dom4j改完之后要写回文件的呀。

## 2020-12-16 Wed

### Dom4j

[Dom4j增加，修改，删除XML文件](https://www.jianshu.com/p/b617266bc2df)

[Android 资源(Resources)访问](https://www.runoob.com/android/android-resources.html)

xml/可以通过调用Resources.getXML()来在运行时读取任意的XML文件。可以在这里保存运行时使用的各种配置文件

[How to edit XML in Android and save?](https://stackoverflow.com/questions/7162285/how-to-edit-xml-in-android-and-save)

- 我悟了，找到盲点了，明天再来改！

### Room

Error：`java.lang.IllegalStateException: attempt to re-open an already-closed object:`

[Room attempt to re-open an already closed database](https://stackoverflow.com/questions/45376492/room-attempt-to-re-open-an-already-closed-database)

- 还有个办法删了db就好

[Room数据库的版本升级姿势](https://www.jianshu.com/p/fae0245cf384)

[Room踩坑：理解Room的正确升库](https://juejin.cn/post/6844903889611800584)

### Json

[浅谈x-www-form-urlencoded与json的区别](https://blog.csdn.net/qq_23049221/article/details/108621301)

## 2020-12-15 Tue

### DICOM协议基本内容

[医疗业务学习笔记--DICOM协议的基础内容](https://zhuanlan.zhihu.com/p/74966427)

[DICOM LIBRARY - TAGS](https://www.dicomlibrary.com/dicom/dicom-tags/)

### AS Error

Error Log

```
java.lang.UnsatisfiedLinkError: Unable to load library 'CoreFoundation':
dlopen(libCoreFoundation.dylib, 9): image not found
dlopen(libCoreFoundation.dylib, 9): image not found
Native library (darwin/libCoreFoundation.dylib) not found in resource path (/Applications/Android Studio 2.app/Contents/lib/bootstrap.jar:/Applications/Android Studio 2.app/Contents/lib/extensions.jar:/Applications/Android Studio 2.app/Contents/lib/util.jar:/Applications/Android Studio 2.app/Contents/lib/jdom.jar:/Applications/Android Studio 2.app/Contents/lib/log4j.jar:/Applications/Android Studio 2.app/Contents/lib/trove4j.jar:/Applications/Android Studio 2.app/Contents/lib/jna.jar:/Applications/Android Studio 2.app/Contents/jre/jdk/Contents/Home/lib/tools.jar)
```

好像是因为更新完系统导致的

### Sublime

[Sublime打开报错：Error trying to parse file](https://blog.csdn.net/mayfla/article/details/79157463)

- `Preferences -> Browse Packages` 点开删除 `User` 文件夹就好啦。

### 杂

事情扎堆的感觉让人崩溃

## 2020-12-08 Tue

### RecyclerView

[RecyclerView 实现item点击水波纹动画](https://blog.csdn.net/android_zhengyongbo/article/details/70171631)

- 加个水波纹
- 法一比较快

[添加下拉刷新](https://www.jianshu.com/p/3bf125b4917d)

### ARTS

学到个好登西：https://juejin.cn/post/6902996077549617160

另外突然发现掘金真的是个很不错的社区

忙完这个月的事开始 ARTS 打卡！

能坚持下来的话真的超好哈哈哈哈哈

### Typora

一直觉得 typora 的宽度太窄了很浪费空间

反正是自己看东西也无所谓什么留白美观

查了一下改主题源代码就可以扩宽编辑器的长度

https://blog.csdn.net/wsq119/article/details/104611585

### Activity通信方式

https://www.jianshu.com/p/c833eb46bc73

https://www.jianshu.com/p/12438e23c6b8

https://www.jianshu.com/p/75eccd29c229

## 2020-12-04 Fri

### @string

对文本内容不要硬编码

[Android Developer - 字符串资源](https://developer.android.com/guide/topics/resources/string-resource?hl=zh-cn)

[你真的会用Android中Strings资源吗](https://cloud.tencent.com/developer/article/1035180)

- Android为了帮助开发者把应用更方便发布给全球不同语言的人们使用，建议开发者在进行开发时不要把UI呈现相关的文本内容硬编码，而是把内容写入到strings.xml中，这样做更加灵活，也更方便翻译成不同其他语言。

### Java

[Java注释会被执行吗](https://mp.weixin.qq.com/s/st3LORDRXMwADsCWdBH1KQ)

- 这个真的有点意思

### RecyclerView

[添加分割线](https://blog.csdn.net/Lindroid20/article/details/76407954)

[添加点击事件](https://www.jianshu.com/p/971396467a62)

- 诶居然没有直接提供 `ListView` 那样的 `setOnItemClickListener()` ？觉得很神奇于是去查了一下，还是有道理的：https://stackoverflow.com/questions/24885223/why-doesnt-recyclerview-have-onitemclicklistener，RecyclerView 的使用要比 ListView 使用要灵活得多。之前用 ListView 的时候如果 item 里面的布局复杂的话确实是比较难搞。
- 注意是在item的布局文件里设置点击事件，不是给recyclerview设置哦。

### WifiManager

[wifiManager.getScanResult() returns null value](https://stackoverflow.com/questions/56379635/wifimanager-getscanresult-returns-null-value)

- 有毒，我怎么就是拿不到这个列表呢- -

[WLAN 扫描功能概览](https://developer.android.com/guide/topics/connectivity/wifi-scan#java)

气死我了气死我了整了一下午都找不出任何bug，然后最后找到的解决方法就是打开位置信息OTZ：https://clz.me/ionic-android-wifimanager-getscanresults/

官方文档里也没说Android7.0要打开位置信息啊5555就说了8.0以上要加位置权限嘛555气死我了 

### 连接指定wifi

[Android自定义连接指定WiFi&热点开关](https://blog.csdn.net/weixin_43835637/article/details/91350820)

## 2020-12-02 Wed

### Android Code Search

Android 代码搜索 ([cs.android.com](https://cs.android.com/?hl=zh-cn)) 是一款可帮助开发者查看实际使用的 Android 源代码的工具。

利用代码搜索，您可以点击源代码的一部分到另一部分，从而更轻松地在所有 AOSP 中浏览交叉引用。这有助于您在 Android 的开源分支之间切换。只有主分支在 Java 和 CPP 中有交叉引用信息，而 Go 则没有。

### AOSP

https://source.android.google.cn/

### RecyclerView

[使用 RecyclerView 创建列表](https://developer.android.com/guide/topics/ui/layout/recyclerview?hl=zh-cn)

- 看啥博客都不如直接看官网文档靠谱哈

《第一行代码》里有的东西必不找其他的看，郭霖写东西确实有一手。

## 2020-12-01 Tue

### Jenkins

[Jenkins](https://juejin.cn/post/6844903879725809678)是一款开源的CI工具，利用Jenkins可以通过规范化的操作流程避免一些低级错误，将开发人员从简单、繁琐的工作中释放出来。关于Jenkins的配置教程网上也是有很多，[Jenkins 持续集成使用教程](https://juejin.im/post/6844903592608923655)就比较详细。

### Android - Surface

[**Surface、SurfaceView、SurfaceHolder 及 SurfaceHolder.Callback 之间的关系**](https://blog.csdn.net/u013898698/article/details/79397437)

- 这一篇文章把 Surface 相关讲的非常清楚了

### Blog

Listify 作者的博客：[MikeTech](https://miketech.it/)

### Xcode Error

[“Xcode quit unexpectedly while using the libswiftCore.dylib plug-in”](https://stackoverflow.com/questions/33303015/xcode-quit-unexpectedly-while-using-the-libswiftcore-dylib-plug-in)

- 然鹅我找不到 Developer?

### IntentFilter

[Intent 与 IntentFilter 详解](https://blog.csdn.net/weixin_33947521/article/details/91442998)

### receiver

[android:报Activity has leaked IntentReceiver或者receiver is not registered错误](https://blog.csdn.net/weiren1101/article/details/51752498)