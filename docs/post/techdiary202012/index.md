
最后一个月

支棱起来咯

<!--more-->

## 2020-12-08 Tue

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

气死我了气死我了整了一下午都找不出任何bug，然后最后找到的解决方法就是打开位置信息OTZ：https://clz.me/ionic-android-wifimanager-getscanresults/****

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