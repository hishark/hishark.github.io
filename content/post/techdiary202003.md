---
title: 三月の技术日记
date: 2020-03-01 22:41:57
tags:
- TechDiary
categories: 技术日记
authors: 
- hishark777
---
有在好好做算法题
<!--more-->

<!-- # 日记打卡
|  一  |  二  |  三  |  四  |  五  |  六  |  日  |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: |
|      |      |      |      |      |      |  1   |
|  <font color="#B22222">**2**   |  <font color="#B22222">**3**   |  4   |  5   |  6   |  7   |  8   |
|  <font color="#B22222">**9**   |  10  |  11  |  <font color="#B22222">**12**  |  <font color="#B22222">**13**  |  <font color="#B22222">**14**  |  <font color="#B22222">**15**  |
|  <font color="#B22222">**16**  |  <font color="#B22222">**17**  |  <font color="#B22222">**18**  |  19  |  20  |  21  |  22  |
|  23  |  24  |  <font color="#B22222">**25**  |  <font color="#B22222">**26**  |  27  |  <font color="#B22222">**28**  |  <font color="#B22222">**29**  |
|  <font color="#B22222">**30**  |  <font color="#B22222">**31**  |      |      |      |      |      | -->


# 2020-03-31
## **Algorithm - sort**

面试的时候考排序直接用Arrays.sort()可能会挨打。

1. [http://panthema.net/2013/sound-of-sorting/](http://panthema.net/2013/sound-of-sorting/)这个好好玩哈哈哈
2. [https://leetcode-cn.com/problems/sort-an-array/solution/fu-xi-ji-chu-pai-xu-suan-fa-java-by-liweiwei1419/](https://leetcode-cn.com/problems/sort-an-array/solution/fu-xi-ji-chu-pai-xu-suan-fa-java-by-liweiwei1419/)wei哥总结的不错
3. [https://www.cs.usfca.edu/~galles/visualization/Algorithms.html](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html)题解里看到的学习算法的可视化网站

## **Android**

> Build anything on Android

喜欢android开发者官网的这个slogan

# 2020-03-30
## **Android**

检测常用手势

[https://developer.android.com/training/gestures/detector?hl=zh-cn](https://developer.android.com/training/gestures/detector?hl=zh-cn)

# 2020-03-29
## **Android Studio**

AS更新到3.6.1了，这个logo颜色。。好刺眼啊，还是之前的版本更好看（可能会真香

[https://developer.android.com/studio/releases](https://developer.android.com/studio/releases)

中文页面还没更新，粗略看了一下新特性感觉更新蛮大啊，另外感觉可以学学kotlin了。

- Design Tools
- 妈呀代码区和预览区终于可以一起看了我哭 好方便
- Color Picker Resource Tab
- Resource Manager
- Updates to the Android Gradle plugin
- findViewById被替换了
- Apply Changes
- Refactor menu option to enable Instant Apps support
- Deobfuscate class and method bytecode in APK Analyzer
- Native tooling
- Attach Kotlin-only APK sources
- Leak detection in Memory Profiler
- Emulators
- Resumable SDK downloads
- Win32 deprecated
- New option for optimizing Gradle sync time

## **Algorithm**

1. [LeetCode1162](https://leetcode-cn.com/problems/as-far-from-land-as-possible/)
- [java queue](https://blog.csdn.net/u012050154/article/details/60572567)
- 使用常量增量数组进行坐标的平移 again
- 宽度/广度优先搜索BFS
1. 稳定的排序算法
- 基数排序
- 冒泡排序
- 直接插入排序
- 二分插入排序
- 归并排序
1. 不稳定的排序算法
- 堆排序
- 快速排序
- 希尔排序
- 直接选择排序

## **App**

Android端发现一个好用的时间追踪app——Boosted

巨好用喔完全切合我的需求👍（话说买了pixel2xl之后，感觉原生安卓现在真滴好好用啊，以后的备用机估计会一直买pixel了哈哈哈哈）

开发者把用到的库放出来了我记一下以后瞅瞅

- [Android Architecture Components](https://developer.android.com/topic/libraries/architecture)
- [Android Week View](https://jitpack.io/p/kmenager/android-week-view)
- [Butter Knife](https://jakewharton.github.io/butterknife)
- [Dagger 2](https://github.com/google/dagger)
- [Gson](https://github.com/google/gson)
- [Joda Time](https://github.com/JodaOrg/joda-time)
- [Material DateTime Picker](https://github.com/wdullaer/MaterialDateTimePicker)
- [MPAndroidChart](https://github.com/PhilJay/MPAndroidChart)
- [OpenSans font](https://fonts.google.com/specimen/Open+Sans)
- [Third-party icons](https://www.flaticon.com/)

还有一个很喜欢的[habit tracker](https://github.com/iSoron/uhabits)突然发现源代码作者放在github上了

star一下⭐️

## **Android**

1. include标签的目的是解决对布局的重复定义，从而提高代码的复用性。
- include标签如果定义了id，若layout也定义了id，那么会被include的id所覆盖。
1. [支持不同的屏幕尺寸](https://developer.android.com/training/multiscreen/screensizes?hl=zh-cn)
- 有一说一我感觉官方文档真滴好全，i了。
1. [自适应界面的 Material 指南](https://material.io/guidelines/layout/responsive-ui.html)
- 马一下这个

# 2020-03-28
## **Algorithm**

字典树

[https://leetcode-cn.com/problems/short-encoding-of-words/solution/99-java-trie-tu-xie-gong-lue-bao-jiao-bao-hui-by-s/](https://leetcode-cn.com/problems/short-encoding-of-words/solution/99-java-trie-tu-xie-gong-lue-bao-jiao-bao-hui-by-s/)

`Arrays.sort()` [https://stackoverflow.com/questions/21970719/java-arrays-sort-with-lambda-expression](https://stackoverflow.com/questions/21970719/java-arrays-sort-with-lambda-expression)

`->` [https://www.runoob.com/java/java8-lambda-expressions.html](https://www.runoob.com/java/java8-lambda-expressions.html)

# 2020-03-26
## **Algorithm**

[借助数组对坐标进行平移！](https://leetcode-cn.com/problems/available-captures-for-rook/)

# 2020-03-25
## **Algorithm**

调整一点代码实现节省时间真的有爽到哈

## **杂**

最近玩动森玩到日夜颠倒

time to study!

# 2020-03-18
## **Algorithm**

正着想不明白就反着想嘛

莫死磕

## **Android phone-tablet适配方案**

# 2020-03-17
## **Algorithm**

我终于可以不看题解做出一点题目了

虽然是简单题

但是还是比以前好些了555

keep moving!

每日刷题能坚持到找到工作的那一天吗

试试吧试试吧

说不定成了呢哈哈哈哈

## **杂**

无语

中午吃完犯困钻到被窝里忘记定闹钟

然后睡了一下午

睡成一滩泥巴了

# 2020-03-16
## **环信视频会议集成**

集成完了

集成过程很舒服

文档详细真是使人愉悦

## **Android Error**

java.lang.RuntimeException: Failed to create EGL context: 0x3003

[https://stackoverflow.com/questions/45392309/failed-to-create-egl-context](https://stackoverflow.com/questions/45392309/failed-to-create-egl-context)

## **杂**

好的

我是猪

我在`resultCode != RESULT_OK`里写了大半天`resultCode == RESULT_OK`的逻辑

# 2020-03-15
## **环信视频会议**

注册的时候记得新建一个线程！

```java
//新建一个线程来进行网络请求注册
new Thread(new Runnable() {
  @Override
  public void run() {
    try {
      EMClient.getInstance().createAccount("robot003", "123456");//同步方法
      ToastUtils.showLong("注册成功！");
    } catch (HyphenateException e) {
      e.printStackTrace();
      ToastUtils.showLong("注册失败"+e.getMessage()+e.getErrorCode());

    }
  }
}).start();
```

夸一下环信

API文档太详细了

用得相当舒爽

此处diss一万遍阿里云视频会议SDK

PS: ScreenCaptureManager要记得在onActivityResult做判断啊兄弟

## **Android Error**

1. Can't create handler inside thread that has not called Looper.prepare()
[https://blog.csdn.net/sun_promise/article/details/45168027](https://blog.csdn.net/sun_promise/article/details/45168027)
2. 使用AlertDialog报错 You need to use a Theme.AppCompat theme (or descendant) with this activity.之解决
[https://blog.csdn.net/tiankongcheng6/article/details/78133028](https://blog.csdn.net/tiankongcheng6/article/details/78133028)
3. Unable to add window -- token null is not for an application
[https://stackoverflow.com/questions/5796611/dialog-throwing-unable-to-add-window-token-null-is-not-for-an-application-wi](https://stackoverflow.com/questions/5796611/dialog-throwing-unable-to-add-window-token-null-is-not-for-an-application-wi)
4. surfaceViewAlready initialized
publishDesktop之前不要publishCamera就好啦！重复publish就出错了

## **Handler**

[https://juejin.im/post/5910533dac502e006cfe01cd](https://juejin.im/post/5910533dac502e006cfe01cd)

## **杂**

写代码态度有变端正哦zxq

稳住稳住

下一步是好好睡觉

这周晚上还是睡太晚

争取11点30上床

玩一会就睡觉

晚安😴

# 2020-03-14
## **Hexo Theme**

知乎突然给我推送了个问题：[求推荐一款hexo博客主题？](https://www.zhihu.com/question/316666767)

在里头看到了看到[icarus](https://github.com/ppoffice/hexo-theme-icarus)一见钟情于是又换主题了

换的时候碰到一系列莫名其妙小问题

然后

我就

直接

重装hexo了哈哈哈哈哈哈哈

## **访问速度优化**

搞不懂为什么会慢

已经用Dnspod解析了哇

明天看看

[Hexo博客访问速度优化](https://github.com/SimpleJian/Hexo/blob/master/source/_posts/Hexo%E5%8D%9A%E5%AE%A2%E8%AE%BF%E9%97%AE%E9%80%9F%E5%BA%A6%E4%BC%98%E5%8C%96.md)

## **环信视频会议集成**

本来想今天搞定，结果今天被博客勾走了

明天做完周一交差！

## **杂**

腾讯企业邮箱有毒哦

上个月我用得好好的

能正常收发邮件

今天闲得无聊给hello@xiaoqizhang.com发了一封邮件结果收不到？？

垃圾箱里也没有

我哭辽

还是乖乖用gmail吧=。=

另外今天凌晨和月月聊了大半天

各种想法完全一致，不愧是睡了三年的对床哈哈哈哈哈！！！

一起冲🦷！

# 2020-03-13
## **Android Error - Missing Library**

[https://blog.csdn.net/zuo_er_lyf/article/details/78593636](https://blog.csdn.net/zuo_er_lyf/article/details/78593636)

如果本来就有其他sdk，且已在src/main/jniLibs下已有文件，那就把环信的sdk也塞到里头去，然后就ok啦。

# 2020-03-12
## **Android Error - Duplicate Class**

Duplicate class com.hyphenate.EMChatRoomChangeListener found in modules classes.jar (com.hyphenate:hyphenate-sdk:3.6.1) and hyphenatechat_3.6.4.jar (hyphenatechat_3.6.4.jar)
Duplicate class com.hyphenate.EMClientListener found in modules classes.jar (com.hyphenate:hyphenate-sdk:3.6.1) and hyphenatechat_3.6.4.jar (hyphenatechat_3.6.4.jar)

[https://developer.android.com/studio/build/dependencies#duplicate_classes](https://developer.android.com/studio/build/dependencies#duplicate_classes)

找到冲突的删掉就好了

## **Android Error - Program type already present**

[https://www.jianshu.com/p/eee41ec17606](https://www.jianshu.com/p/eee41ec17606)

[https://blog.csdn.net/qq_35008279/article/details/86310339](https://blog.csdn.net/qq_35008279/article/details/86310339)

[https://blog.csdn.net/Calvin_zhou/article/details/80880501](https://blog.csdn.net/Calvin_zhou/article/details/80880501) ⭐️

该做的都做了之后，如果还是报错，rebuild一下就ok了！

# 2020-03-09
## **Roadmap**

[Android App Developer Roadmap Curated by the Programming Community | Hackr.io](https://hackr.io/roadmaps/android-app-developer-roadmap)

[Android Development Learning Path - 2020 Edition](https://medium.com/mindorks/android-development-learning-path-2020-edition-3f464ac56dbf)

## **Interview Questions**

[Android-interview-questions](https://github.com/MindorksOpenSource/android-interview-questions)

# 2020-03-03
## **Kotlin**

[English Version](https://kotlinlang.org/)

[Chinese Version](https://www.kotlincn.net/)

[Smart cast to 'XXX' is impossible](https://blog.csdn.net/shichimiyasatone/article/details/97917106)

# 2020-03-02
## **SS**

用了好几年一直没在意PAC和全局的区别，哪个舒畅选哪个，今天突然google了一下

[SS的PAC模式与全局模式](https://www.yuque.com/xiaoqizhang/techdiary/50674685f8d4ec76bc653d7bbf3600be)

[SS PAC模式和全局模式的区别](https://www.zybuluo.com/gongzhen/note/472805)

另外ssrcloud涨价了，原来10RMB-100G，现在10元20G，好的我溜了换下一个机场✈️

这位兄弟总结的巨全

[浅谈部分机场（SS/SSR提供商）的使用感受--毒药笔记持续更新中](https://www.evernote.com/shard/s609/client/snv?sn=https://www.evernote.com/shard/s609/sh/087d120a-d07f-4b13-95d4-95af5d573db5%2F43c350e6c55ac4c3)