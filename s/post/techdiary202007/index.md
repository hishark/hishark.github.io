明年暑假在校招

今年暑假在撒欢
<!--more-->

<!-- 
# 日记打卡
|  一  |  二  |  三  |  四  |  五  |  六  |  日  |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: |
|      |      |  [1](#2020-07-01)   |  [2](#2020-07-02)   |  3   |  [4](#2020-07-04)  |  5   |
|  [6](#2020-07-06)   |  [7](#2020-07-07)   |  8   |  9   |  10  |  11  |  [12](#2020-07-12)  |
|  13  |  [14](#2020-07-14)  |  15  |  [16](#2020-07-16)  |  [17](#2020-07-17)  |  [18](#2020-07-18)  |  19  |
|  20  |  [21](#2020-07-21)  |  [22](#2020-07-22)  |  [23](#2020-07-23)  |  24  |  25  |  26  |
|  [27](#2020-07-27)  |  [28](#2020-07-28)  |  [29](#2020-07-29)  |  [30](#2020-07-30)  |  31  |      |      | -->

## 2020-07-30
### Error
木村先生那边的新代码
运行报错记录一下

```
ERROR: Unable to find method 'org.gradle.api.tasks.compile.CompileOptions.setBootClasspath(Ljava/lang/String;)V'.
Possible causes for this unexpected error include:
Gradle's dependency cache may be corrupt (this sometimes occurs after a network connection timeout.)
Re-download dependencies and sync project (requires network)

The state of a Gradle build process (daemon) may be corrupt. Stopping all Gradle daemons may solve this problem.
Stop Gradle build processes (requires restart)

Your project may be using a third-party plugin which is not compatible with the other plugins in the project or the version of Gradle requested by the project.

In the case of corrupt Gradle processes, you can also try closing the IDE and then killing all Java processes.
```
- https://www.jianshu.com/p/f109bcaeff78 版本改一下就ok了

```
ERROR: The SourceSet 'instrumentTest' is not recognized by the Android Gradle Plugin. Perhaps you misspelled something?
```
- https://stackoverflow.com/questions/49511200/the-sourceset-instrumenttest-is-not-recognized-by-the-android-gradle-plugin 已废弃，替换即可

```
* What went wrong:
Execution failed for task ':processDebugResources'.
> A failure occurred while executing com.android.build.gradle.internal.tasks.Workers$ActionFacade
   > Android resource linking failed
     /Users/a777/Documents/work/blood-version/prj/AndroidManifest.xml:21:5-94:19: AAPT: error: attribute android:extractNativeLibs not found.
```
- 改改编译版本号突然ok了

## 2020-07-29

### NetworkCallback
[ConnectivityManager.NetworkCallback](https://developer.android.com/reference/android/net/ConnectivityManager.NetworkCallback)
>For callbacks registered with ConnectivityManager.registerNetworkCallback(NetworkRequest, PendingIntent), multiple networks may be available at the same time, and onAvailable will be called for each of these as they appear.
For callbacks registered with ConnectivityManager.requestNetwork(NetworkRequest, PendingIntent) and ConnectivityManager.registerDefaultNetworkCallback(ConnectivityManager.NetworkCallback), this means the network passed as an argument is the new best network for this request and is now tracked by this callback ; this callback will no longer receive method calls about other networks that may have been passed to this method previously. The previously-best network may have disconnected, or it may still be around and the newly-best network may simply be better.

[Android即时网络监听(二)-ConnectivityManager.NetworkCallback](https://www.jianshu.com/p/66afbd05c9b9)

### ROI
[数字图像处理--图像ROI](https://blog.csdn.net/baidu_38172402/article/details/89017041)

### 杂
...我以后一定乖乖看英文文档
看得烦人也要看
谷歌百度了大半天一个问题
看一下官方文档一下就解决了啊啊啊啊

## 2020-07-28
### 血流成像
[基于多普勒和散斑跟踪的超声矢量血流成像方法比较](http://aammt.tmmu.edu.cn/Upload/rhtml/201605014.htm)

## 2020-07-27
### 回调
[说说安卓回调——CallBack](https://www.jianshu.com/p/c92525606e70)

### 杂
🍅todo真好用
下半年坚持用下去吧~
另外发现每次做之前觉得如狼似虎的问题
最后解决了又会觉得：啊 还好
所以以后别怕啦！

## 2020-07-23
### Toast
不要随便用Toast弹Log测试
一次性的还好
放到回调里头不停的弹出来会影响整个界面的速度啦！

### Network
```
    /**
     * Binds the current process to {@code network}.  All Sockets created in the future
     * (and not explicitly bound via a bound SocketFactory from
     * {@link Network#getSocketFactory() Network.getSocketFactory()}) will be bound to
     * {@code network}.  All host name resolutions will be limited to {@code network} as well.
     * Note that if {@code network} ever disconnects, all Sockets created in this way will cease to
     * work and all host name resolutions will fail.  This is by design so an application doesn't
     * accidentally use Sockets it thinks are still bound to a particular {@link Network}.
     * To clear binding pass {@code null} for {@code network}.  Using individually bound
     * Sockets created by Network.getSocketFactory().createSocket() and
     * performing network-specific host name resolutions via
     * {@link Network#getAllByName Network.getAllByName} is preferred to calling
     * {@code bindProcessToNetwork}.
     *
     * @param network The {@link Network} to bind the current process to, or {@code null} to clear
     *                the current binding.
     * @return {@code true} on success, {@code false} if the {@link Network} is no longer valid.
     */
    public boolean bindProcessToNetwork(Network network) {
        // Forcing callers to call thru non-static function ensures ConnectivityManager
        // instantiated.
        return setProcessDefaultNetwork(network);
    }
```
看源码这玩意绑定指定网络之后是只会影响到之后的网络请求
所以才会：wifi连接好仪器之后，再用4g发出视频会议也没有影响仪器的连接？
好的

## 2020-07-22
### Network Wifi+4G
前几天搜的一大堆一直忘记整理，今天收拾一下。
感觉wifi连接上仪器上之后，想要全局网络请求都绑定为4G好像不可行啊。。群里有个老哥说这个好像跟ROM有关的，API层没办法。那我能不能试试每次需要发起网络请求的时候改为4G又不切断与仪器的wifi连接？但是这里又涉及到了远程会诊持续性的问题。。这样请求的话能够满足长时间的网络请求吗OTZ 难搞 我试试吧- -

[手机连接 WiFi 后通过 4g 上网？-V2EX](https://www.v2ex.com/t/356583)

[Android和IOS实现Wifi及4G双通道](https://www.codeleading.com/article/4648668408/)☆

[在wifi开启时,强制通过手机网络发送请求](https://blog.csdn.net/hlq19901005/article/details/61914603)☆

[Android多网络环境（wifi,mobile）下强制在某个网络(mobile)访问服务端以及适配](https://blog.csdn.net/u010019468/article/details/72886859)☆
> ↑这人笑死我了哈哈哈哈哈 “可能会觉得哪会有这样的蛋疼需求，认为只要能访问就行了，还要特地移动网络，那我只能讲你们的业务发展中没有这样的需求。”
> 害！可不就是么=^=

[知乎上相关问题的第一个回答](https://www.zhihu.com/question/40910036)

之后可能要用 马一下
[Android Network ——判断网络状态](http://www.androidchina.net/2471.html)

[ANDROID判断网络是否可用_手机网络状态类型判断](http://dditblog.com/itshare_477.html)

### Android屏幕适配
[Android屏幕适配很麻烦吗？不！太简单了。。。](https://www.jianshu.com/p/4254ea9d1b27)

[一种极低成本的Android屏幕适配方式](https://mp.weixin.qq.com/s/d9QCoBP6kV9VSWvVldVVwA)

[屏幕兼容性概览 - Android Developer](https://developer.android.com/guide/practices/screens_support.html)

### Kotlin & Android
[Learn Android and Kotlin with no programming experience](https://android-developers.googleblog.com/2020/07/learn-android-and-kotlin-with-no-experience.html)

[Android Basics in Kotlin](https://developer.android.com/courses/android-basics-kotlin/course) #TODO

### 计算机网络
跑完步回家拉伸的时候为了凑学习时长
边拉伸边找了个计算机网络的视频听听
还挺有意思哈 看评论好像还有韩立刚老师的视频不错
之后听听

### 杂
加了一个番茄todo里每日必须学习6h的自习室
进去约束一下自己吧
毕竟最近一天完完整整连续3h的专注时间都不知道有没有OTZ


## 2020-07-21
### 杂
时常觉得Leetcode的URL有点过于冗长，比如今天这个题的题解：
https://leetcode-cn.com/problems/unique-binary-search-trees-ii/solution/bu-tong-de-er-cha-sou-suo-shu-ii-by-leetcode-solut/
敢不敢再长一点！
然后今天终于把之前Goodnotes上的笔记

## 2020-07-18
### Android Broadcast
[Google官方文档-广播概览](https://developer.android.com/guide/components/broadcasts?hl=zh-cn)

### Wifi
[Wi-Fi](https://zh.wikipedia.org/wiki/Wi-Fi)

[WPS](https://baike.baidu.com/item/WPS/4810478)

[WPS在AndroidP（即9.0）中已弃用](https://source.android.com/devices/tech/connect/wifi-easy-connect)

>link: https://gadgets.ndtv.com/mobiles/news/google-wi-fi-protected-setup-wps-android-p-1880957
Google is reportedly ending support for Wi-Fi Protected Setup (WPS) in Android P. WPS is essentially a protocol that enables a client Wi-Fi device to connect to a router using a PIN or a push-button. It was devised to be used as a secure and faster way to connect a router to wireless devices. However, in recent few years, loopholes have been discovered. Thus, it was found that it made users susceptible to hacking especially those on personal Wi-Fi. According to the latest reports, this method will not be available for Android P users are all.
### Wifi+4G双通道 
Wifi连接超声仪器 使用4G远程会诊 
难搞哦这个需求- -

[手机连接行车记录仪WiFi后无法上网1](https://club.huawei.com/thread-17008229-2-1.html)

[手机连接行车记录仪WiFi后无法上网2](https://club.huawei.com/thread-17008229-1-1.html)

[wifi开启时,强制通过手机网络发送请求](https://blog.csdn.net/hlq19901005/article/details/61914603)

### Network
[ConnectivityManager.requestNetwork in Android 6.0](https://stackoverflow.com/questions/32185628/connectivitymanager-requestnetwork-in-android-6-0)
- 还好看到了这个，把华为那个测试机升级到Android7.0就解决了



### 杂
everyday查漏补缺

## 2020-07-17
### Github Arctic Code Vault
[GitHub 启动代码永久保存计划，为人类文明留“火种”？](https://blog.csdn.net/wypblog/article/details/103105350)
>GitHub Arctic Code Vault 是一个数据存储库，存储在北极世界档案馆（AWA）中，这是一个长期的档案设施，位于北极山永久冻土层深250米。该档案馆位于斯瓦尔巴群岛的一个退役煤矿中，比北极圈更靠近北极。
GitHub 将在 2020 年 2 月 2 日捕获每个活动公共存储库的快照，并将这些数据保存在 Arctic Code Vault 中。此外还包括由星号、依赖项和咨询小组确定的大量休眠存储库。快照将由每个存储库的默认分支的 HEAD 减去任何大于 100KB 的二进制文件组成，每个存储库将打包为一个 TAR 文件。

我靠这太酷了 我的代码被存到北极啦！！

### Valine自定义表情
[Valine添加自定义表情](https://www.fezhu.top/2020/05/01/Valinebiaoqing/)

## 2020-07-16
### Hexo延迟问题
[Hexo发布新文章，github更新了，但是页面就是不显示新文章](https://segmentfault.com/q/1010000012969562)

我哭了 以后deploy了之后博客不更新就别管了
hexo clean之后还是没用就！别！管！
会自己好的！
反复generate又deploy就是浪费时间啦！！
顺便可以[在这里](https://github.com/hishark/hishark.github.io/deployments/activity_log?environment=github-pages)看到有没有成功deploy！

### Valine邮件提醒
[官方教程](https://github.com/zhaojun1998/Valine-Admin/blob/master/README.md)已经没有维护啦

leancloud后台已经更新了

下面这个最新的教程ok👇
[Valine添加自定义邮件提醒](https://www.fezhu.top/2020/05/15/Valineyoujian/)

### Github Page
直接用[page](https://zhuanlan.zhihu.com/p/35668237)好方便哈哈哈

另外github page的标题原来默认是仓库名

可以通过修改`_config.yml`来修改 [🔗](https://stackoverflow.com/questions/42100627/why-does-my-repository-name-appear-as-the-title-in-my-github-pages-site)
eg:
```
title: 777
```
### GoDaddy
绝了，狗爹官网死活没办法改动域名服务器
然后跑到它的小程序里秒改哈哈哈哈哈哈开心
于是兜兜转转又用回了hishark777.com
网上冲浪还是用网名8！
xiaoqizhang.com用github小号整了个Github Pages做中转站啦~

## 2020-07-14
### chrom切换tab

[Google Chrome浏览器如何快速切换标签页](https://jingyan.baidu.com/article/c146541340c9d70bfdfc4c5c.html)

### Artstation

太好看了这些画！！

[Sylvain Sarrailh Portfolio](https://tohad.artstation.com/)

### 思源宋体

[Google Fonts 已支持思源宋体！](https://io-oi.me/tech/noto-serif-sc-added-on-google-fonts/)

## 2020-07-12
### SurfaceView

[Android中的SurfaceView详解](https://www.jianshu.com/p/b037249e6d31)

[Android进阶5：SurfaceView实现原理分析](https://juejin.im/post/5da721a6518825200b2d547e#heading-8)

实现拖动的surfaceview

用scrollview可以最简单的实现

[surfaceview如何实现可以滚动的画板-CSDN论坛](https://bbs.csdn.net/topics/391071463?page=1)

[ScrollView的子View高度match_parent无效 解决_yanzi1225627的专栏-CSDN博客_android nestedscrollview 里面 子控件 layout_height=mat](https://blog.csdn.net/yanzi1225627/article/details/52163460)

[设置ScrollView 里面的布局高度为match_parent不起作用_toast_tips的博客-CSDN博客_android scrollview布局设置match_parent不起作用](https://blog.csdn.net/toast_tips/article/details/55253239?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.nonecase)

还有更复杂的解决方法 之后研究一下 TODO

[Android SurfaceView scrolling](https://stackoverflow.com/questions/1096618/android-surfaceview-scrolling)

[How can I make a SurfaceView larger than the screen?](https://stackoverflow.com/questions/6050923/how-can-i-make-a-surfaceview-larger-than-the-screen)

### 动态更改SV的大小

[Android设置SurfaceView任意大小和任意位置_MyArrow的专栏-CSDN博客_surfaceview 设置大小](https://blog.csdn.net/MyArrow/article/details/41083735)

[被SurfaceView搞死了的搞后感 - 拉风的道长_Android之路 - OSCHINA](https://my.oschina.net/lifj/blog/749350)

[改变SurfaceView的大小|RelativeLayout|LayoutParams_stefzeus的专栏-CSDN博客_surfaceview layoutparams](https://blog.csdn.net/stefzeus/article/details/6817424)

成了

注意此处的单位是px

如果需要使用dp为单位，需要进行转换：

[android中dp与px（像素）之间的转换_seevc的专栏-CSDN博客_android 像素和dp之间的换算](https://blog.csdn.net/seevc/article/details/43053707?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.nonecase)

### AS Log

[https://jingyan.baidu.com/article/5d6edee2d35ec199eadeecd2.html](https://jingyan.baidu.com/article/5d6edee2d35ec199eadeecd2.html)

## **2020-07-07**
### Module

[](https://developer.android.com/studio/projects/add-app-module?hl=zh-cn)

[Application Fundamentals | Android Developers](https://developer.android.com/guide/components/fundamentals.html)

### okhttp

[OkHttp3的基本用法](https://www.jianshu.com/p/1873287eed87)

### okhttp上传多个文件

有个坑，我上传9个文件（包括图片和视频）的时候，addFormDataPart的第一个参数如果都设置成file"就只能成功上传一个，我改成不一样的参数就成功上传了9个。看了几个博客都是一样的参数我还以为无所谓！！

[https://www.jianshu.com/p/20a7fab00c6d](https://www.jianshu.com/p/20a7fab00c6d)

[okhttp上传多个文件_libin657913204的博客-CSDN博客_okhttp 上传多文件](https://blog.csdn.net/libin657913204/article/details/104546972)

[Okhttp中的 MultipartBody.addFormDataPart() 参数解释_Hu_wenpeng的博客-CSDN博客_okhttp addformdatapart](https://blog.csdn.net/Hu_wenpeng/article/details/105492603?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase)

### okhttp连接超时

除了设置时间这些操作，第一个应该确保自己的网是好的（。。。

[连接服务器接口时java.net.SocketTimeoutException: timeout_流萤梦的博客-CSDN博客_java.net.sockettimeoutexception](https://blog.csdn.net/weixin_38629529/article/details/89788963)

connectTimeout writeTimeout readTimeout都设置一下

### okhttp打印完整的网络请求信息

[Android中使用logger打印完整的okhttp网络请求和响应的所有相关信息（请求行、请求头、请求体、响应行、响应行、响应头、响应体）_yonbor605的博客-CSDN博客_android okhttp 打印header](https://blog.csdn.net/yonbor605/article/details/82253985)

### MIME

[MIME 参考手册](https://www.w3school.com.cn/media/media_mimeref.asp)

### 遍历文件

[Android 遍历文件夹中所有文件](https://www.jianshu.com/p/22b56318bd56)

[45.安心技术梳理 - Okhttp3，java.net.SocketTimeoutException: timeout](https://blog.csdn.net/majunzhu/article/details/103388964)

[okhttp3之java.net.SocketTimeoutException: timeout 异常处理_Vincent2014Linux-CSDN博客_java.net.sockettimeoutexception: timeout](https://blog.csdn.net/Vincent2014Linux/article/details/98881462)

### 合并APP

[Android--合并两个APP的具体做法（掌握）_超宇的博客-CSDN博客_两个app整合到一起](https://blog.csdn.net/chaoyu168/article/details/70228045)

[将多个APP合并到一个APP](https://www.jianshu.com/p/c36760341e0d)

[android-studio-Android 多个Module能够共用一份资源分拣吗--CSDN问答频道](https://ask.csdn.net/questions/643032)

[project和module的关系？](https://www.jianshu.com/p/9f1fba2f8ad1)

[Android Studio 使用他人的项目－导入他的 Module](http://www.itpow.com/c/2017/03/6856.asp)

[https://developer.android.com/studio/projects/add-app-module?hl=zh-cn](https://developer.android.com/studio/projects/add-app-module?hl=zh-cn)

[Android：将project当成module导入项目中_XIADANXIN的博客-CSDN博客_将一个project转成module](https://blog.csdn.net/XIADANXIN/article/details/80051738?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase)

[Android Studio 将一个android项目当做另外一个android项目的library_薛瑄的博客-CSDN博客_怎么把一个安卓项目移植到另一个安卓项目](https://blog.csdn.net/xx326664162/article/details/48175069)

[https://blog.csdn.net/qq_28193019/article/details/103608977](https://blog.csdn.net/qq_28193019/article/details/103608977)

[https://blog.csdn.net/colinandroid/article/details/72781498](https://blog.csdn.net/colinandroid/article/details/72781498)

## **2020-07-06**
### kotlin

二维数组初始化Array(3){IntArray(3)}

[Kotlin数组](https://www.jianshu.com/p/e75795be48c8)

### android

[How to embed a mobile application in other application?](https://stackoverflow.com/questions/19209856/how-to-embed-a-mobile-application-in-other-application)

[Application Fundamentals | Android Developers](https://developer.android.com/guide/components/fundamentals.html)

[使用 RecyclerView 创建列表 | Android 开发者 | Android Developers](https://developer.android.com/guide/topics/ui/layout/recyclerview?hl=zh-cn)

↓这个up讲得好
[https://www.bilibili.com/video/BV1F4411Y7it](https://www.bilibili.com/video/BV1F4411Y7it)

## **2020-07-04**
### hexo

我又换主题了 太快乐了

这个也太好看 了 点 吧！

[hexo博客主题「paper」的设计与开发](https://randomyang.top/2019/12/01/hexo%E5%8D%9A%E5%AE%A2%E4%B8%BB%E9%A2%98%E3%80%8Cpaper%E3%80%8D%E7%9A%84%E8%AE%BE%E8%AE%A1%E4%B8%8E%E5%BC%80%E5%8F%91/)

[Hexo主题开发经验杂谈 | MARKSZのBlog](https://molunerfinn.com/make-a-hexo-theme/)

[Hexo启动页面显示extends includes/layout.pug block content include includes/recent-posts.pug include](https://blog.csdn.net/weixin_44318830/article/details/104884936)

[Regex101](https://regex101.com/)

[css 中要用到了 google 的思源字体，加载不动怎么办？ - V2EX](https://www.v2ex.com/t/400856)

[在web页面中使用Google思源宋体，思源黑体](https://cloud.tencent.com/developer/news/402607)

[Chrome 中文设置字体无效 始终为宋体 的坑之一 html lang_pzx521521的博客-CSDN博客_chrome字体不会变](https://blog.csdn.net/pzx521521/article/details/80267972?utm_source=blogxgwz6)

### 短路

差点忘了这个，做题目碰到了

[JAVA &&（短路与），&，|，||（短路或）_StruggleOldBoy的博客-CSDN博客_短路与短路或](https://blog.csdn.net/StruggleOldBoy/article/details/51967120)

### 正则

[https://blog.csdn.net/pzx521521/article/details/80267972?utm_source=blogxgwz6](https://blog.csdn.net/pzx521521/article/details/80267972?utm_source=blogxgwz6)

## **2020-07-02**
### latex

把latex配一下

这个成了✅

中文也没问题哈哈哈哈

[MacOS10.15.3+MacTex (TexLive2019)+VS Code的LaTex教程](https://zhuanlan.zhihu.com/p/107393437)

### mkdocs
[Material for MkDocs - Getting started](https://squidfunk.github.io/mkdocs-material/getting-started/)



## **2020-07-01**
### hexo+aliyun

啥时候有空了再来转一下

（八成因为嫌麻烦懒得搞

[从零搭建Hexo博客并部署阿里云服务器（奶妈级教学）_Object的博客-CSDN博客_hexo部署到阿里云](https://blog.csdn.net/NoCortY/article/details/99631249)

[基于阿里云搭建自己的的Hexo博客-云栖社区-阿里云](https://yq.aliyun.com/articles/749372)
