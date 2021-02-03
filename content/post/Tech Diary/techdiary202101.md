---
title: "Tech Diary | 2021.01"
date: 2021-01-03T12:38:50+08:00
draft: false
categories: 
- 技术日记
tags:
- TechDiary
description: 2021 年要好好学习天天向上
---

## 2021-01-18 Mon

### ExoPlayer

[Doc](https://exoplayer.dev/hello-world.html)

这文档看着是真舒服

[Android文件列表RecyclerView中点击视频播放](https://blog.csdn.net/greatyoulv/article/details/104066787)

## 2021-01-17 Sun

### Git

[Git各指令的本质，真是通俗易懂啊](https://juejin.cn/post/6895246702614806542)

### SSL Error

[javax.net.ssl.SSLHandshakeException: Chain validation failed](https://blog.csdn.net/weixin_39397471/article/details/103877854)

- Pixel 的时间一直没对上，修改为正确时间后就好了。

### Gradle

[Android Studio 下载Gradle 超时解决方案](https://www.cnblogs.com/emanlee/p/13263457.html)

### RecyclerView

[RecyclerView/ListView嵌套CheckBox选中状态错乱解决方案](https://blog.csdn.net/qq_20521573/article/details/52655570)

[RecyclerView-->点击和长按事件](https://www.jianshu.com/p/1b7dd65a7e65?utm_campaign=maleskine&utm_content=note&utm_medium=seo_notes&utm_source=recommendation)

### Glide

[加载本地图片](https://blog.csdn.net/yulyu/article/details/55056352)

- 没差，就 new 个 File

### AS

我真的要被这个卡死的问题烦死了

过两天抽空把AS全部卸掉重装

[Mac Big Sur version 11.0.1 java.lang.UnsatisfiedLinkError: Unable to load library 'CoreFoundation'](https://stackoverflow.com/questions/64954777/mac-big-sur-version-11-0-1-java-lang-unsatisfiedlinkerror-unable-to-load-librar)

```java
java.lang.UnsatisfiedLinkError: Unable to load library 'CoreFoundation':
dlopen(libCoreFoundation.dylib, 9): image not found
dlopen(libCoreFoundation.dylib, 9): image not found
Native library (darwin/libCoreFoundation.dylib) not found in resource path (/Applications/Android Studio 2.app/Contents/lib/bootstrap.jar:/Applications/Android Studio 2.app/Contents/lib/extensions.jar:/Applications/Android Studio 2.app/Contents/lib/util.jar:/Applications/Android Studio 2.app/Contents/lib/jdom.jar:/Applications/Android Studio 2.app/Contents/lib/log4j.jar:/Applications/Android Studio 2.app/Contents/lib/trove4j.jar:/Applications/Android Studio 2.app/Contents/lib/jna.jar:/Applications/Android Studio 2.app/Contents/jre/jdk/Contents/Home/lib/tools.jar)
	at com.sun.jna.NativeLibrary.loadLibrary(NativeLibrary.java:302)
	at com.sun.jna.NativeLibrary.getInstance(NativeLibrary.java:455)
	at com.sun.jna.Library$Handler.<init>(Library.java:192)
	at com.sun.jna.Native.load(Native.java:596)
	at com.sun.jna.Native.load(Native.java:570)
	at com.intellij.util.text.DateFormatUtil.getMacFormats(DateFormatUtil.java:345)
	at com.intellij.util.text.DateFormatUtil.getDateTimeFormats(DateFormatUtil.java:284)
	at com.intellij.util.text.DateFormatUtil.<clinit>(DateFormatUtil.java:45)
	at com.intellij.vcs.log.ui.table.VcsLogGraphTable.getColumnWidthFromData(VcsLogGraphTable.java:348)
	at com.intellij.vcs.log.ui.table.VcsLogGraphTable.updateAuthorAndDataWidth(VcsLogGraphTable.java:296)
	at com.intellij.vcs.log.ui.table.VcsLogGraphTable.reLayout(VcsLogGraphTable.java:259)
	at com.intellij.vcs.log.ui.table.VcsLogGraphTable.onColumnOrderSettingChanged(VcsLogGraphTable.java:208)
	at com.intellij.vcs.log.ui.table.VcsLogGraphTable.initColumns(VcsLogGraphTable.java:157)
	at com.intellij.vcs.log.ui.table.VcsLogGraphTable.<init>(VcsLogGraphTable.java:122)
	at com.intellij.vcs.log.ui.frame.MainFrame$MyVcsLogGraphTable.<init>(MainFrame.java:366)
	at com.intellij.vcs.log.ui.frame.MainFrame.<init>(MainFrame.java:88)
	at com.intellij.vcs.log.ui.VcsLogUiImpl.<init>(VcsLogUiImpl.java:55)
	at com.intellij.vcs.log.impl.VcsLogManager$MainVcsLogUiFactory.createLogUi(VcsLogManager.java:249)
	at com.intellij.vcs.log.impl.VcsLogManager$MainVcsLogUiFactory.createLogUi(VcsLogManager.java:229)
	at com.intellij.vcs.log.impl.VcsLogManager.createLogUi(VcsLogManager.java:115)
	at com.intellij.vcs.log.impl.VcsLogManager.createLogUi(VcsLogManager.java:105)
	at com.intellij.vcs.log.impl.VcsLogContentProvider.addMainUi(VcsLogContentProvider.java:73)
	at com.intellij.vcs.log.impl.VcsLogContentProvider.<init>(VcsLogContentProvider.java:60)
	at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
	at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
	at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
	at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
	at org.picocontainer.defaults.InstantiatingComponentAdapter.newInstance(InstantiatingComponentAdapter.java:193)
	at com.intellij.util.pico.CachingConstructorInjectionComponentAdapter.doGetComponentInstance(CachingConstructorInjectionComponentAdapter.java:88)
	at com.intellij.util.pico.CachingConstructorInjectionComponentAdapter.instantiateGuarded(CachingConstructorInjectionComponentAdapter.java:66)
	at com.intellij.util.pico.CachingConstructorInjectionComponentAdapter.getComponentInstance(CachingConstructorInjectionComponentAdapter.java:48)
	at com.intellij.openapi.vcs.changes.ui.ChangesViewContentEP.newClassInstance(ChangesViewContentEP.java:92)
	at com.intellij.openapi.vcs.changes.ui.ChangesViewContentEP.getInstance(ChangesViewContentEP.java:68)
	at com.intellij.openapi.vcs.changes.ui.ChangesViewContentManager$MyContentManagerListener.selectionChanged(ChangesViewContentManager.java:248)
	at sun.reflect.GeneratedMethodAccessor67.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at com.intellij.util.EventDispatcher.dispatchVoidMethod(EventDispatcher.java:130)
	at com.intellij.util.EventDispatcher.access$000(EventDispatcher.java:24)
	at com.intellij.util.EventDispatcher$1.invoke(EventDispatcher.java:88)
	at com.sun.proxy.$Proxy102.selectionChanged(Unknown Source)
	at com.intellij.ui.content.impl.ContentManagerImpl.fireSelectionChanged(ContentManagerImpl.java:554)
	at com.intellij.ui.content.impl.ContentManagerImpl.addSelectedContent(ContentManagerImpl.java:370)
	at com.intellij.ui.content.impl.ContentManagerImpl$1.run(ContentManagerImpl.java:461)
	at com.intellij.ui.content.impl.ContentManagerImpl.setSelectedContent(ContentManagerImpl.java:477)
	at com.intellij.ui.content.impl.ContentManagerImpl.setSelectedContentCB(ContentManagerImpl.java:428)
	at com.intellij.ui.content.impl.ContentManagerImpl.setSelectedContentCB(ContentManagerImpl.java:417)
	at com.intellij.ui.content.impl.ContentManagerImpl.setSelectedContentCB(ContentManagerImpl.java:495)
	at com.intellij.ui.content.impl.ContentManagerImpl.setSelectedContent(ContentManagerImpl.java:500)
	at com.intellij.ui.content.impl.ContentManagerImpl.doAddContent(ContentManagerImpl.java:152)
	at com.intellij.ui.content.impl.ContentManagerImpl.addContent(ContentManagerImpl.java:129)
	at com.intellij.openapi.vcs.changes.ui.ChangesViewContentManager.addIntoCorrectPlace(ChangesViewContentManager.java:307)
	at com.intellij.openapi.vcs.changes.ui.ChangesViewContentManager.setUp(ChangesViewContentManager.java:70)
	at com.intellij.openapi.vcs.changes.ui.ChangesViewToolWindowFactory.createToolWindowContent(ChangesViewToolWindowFactory.java:30)
	at com.intellij.openapi.wm.impl.ToolWindowImpl.ensureContentInitialized(ToolWindowImpl.java:533)
	at com.intellij.openapi.wm.impl.ToolWindowImpl.getContentManager(ToolWindowImpl.java:356)
	at com.intellij.vcs.log.impl.VcsLogTabsWatcher.installContentListener(VcsLogTabsWatcher.java:76)
	at com.intellij.vcs.log.impl.VcsLogTabsWatcher.lambda$new$0(VcsLogTabsWatcher.java:51)
	at com.intellij.openapi.application.TransactionGuardImpl$2.run(TransactionGuardImpl.java:312)
	at com.intellij.openapi.application.impl.LaterInvocator$FlushQueue.doRun(LaterInvocator.java:433)
	at com.intellij.openapi.application.impl.LaterInvocator$FlushQueue.runNextEvent(LaterInvocator.java:416)
	at com.intellij.openapi.application.impl.LaterInvocator$FlushQueue.run(LaterInvocator.java:399)
	at java.awt.event.InvocationEvent.dispatch(InvocationEvent.java:311)
	at java.awt.EventQueue.dispatchEventImpl(EventQueue.java:764)
	at java.awt.EventQueue.access$500(EventQueue.java:98)
	at java.awt.EventQueue$3.run(EventQueue.java:715)
	at java.awt.EventQueue$3.run(EventQueue.java:709)
	at java.security.AccessController.doPrivileged(Native Method)
	at java.security.ProtectionDomain$JavaSecurityAccessImpl.doIntersectionPrivilege(ProtectionDomain.java:74)
	at java.awt.EventQueue.dispatchEvent(EventQueue.java:734)
	at com.intellij.ide.IdeEventQueue.defaultDispatchEvent(IdeEventQueue.java:878)
	at com.intellij.ide.IdeEventQueue._dispatchEvent(IdeEventQueue.java:827)
	at com.intellij.ide.IdeEventQueue.lambda$dispatchEvent$8(IdeEventQueue.java:466)
	at com.intellij.openapi.progress.impl.CoreProgressManager.computePrioritized(CoreProgressManager.java:704)
	at com.intellij.ide.IdeEventQueue.dispatchEvent(IdeEventQueue.java:465)
	at java.awt.EventDispatchThread.pumpOneEventForFilters(EventDispatchThread.java:205)
	at java.awt.EventDispatchThread.pumpEventsForFilter(EventDispatchThread.java:116)
	at java.awt.EventDispatchThread.pumpEventsForHierarchy(EventDispatchThread.java:105)
	at java.awt.EventDispatchThread.pumpEvents(EventDispatchThread.java:101)
	at java.awt.EventDispatchThread.pumpEvents(EventDispatchThread.java:93)
	at java.awt.EventDispatchThread.run(EventDispatchThread.java:82)
	Suppressed: java.lang.UnsatisfiedLinkError: dlopen(libCoreFoundation.dylib, 9): image not found
		at com.sun.jna.Native.open(Native Method)
		at com.sun.jna.NativeLibrary.loadLibrary(NativeLibrary.java:191)
		... 80 more
	Suppressed: java.lang.UnsatisfiedLinkError: dlopen(libCoreFoundation.dylib, 9): image not found
		at com.sun.jna.Native.open(Native Method)
		at com.sun.jna.NativeLibrary.loadLibrary(NativeLibrary.java:204)
		... 80 more
	Suppressed: java.io.IOException: Native library (darwin/libCoreFoundation.dylib) not found in resource path (/Applications/Android Studio 2.app/Contents/lib/bootstrap.jar:/Applications/Android Studio 2.app/Contents/lib/extensions.jar:/Applications/Android Studio 2.app/Contents/lib/util.jar:/Applications/Android Studio 2.app/Contents/lib/jdom.jar:/Applications/Android Studio 2.app/Contents/lib/log4j.jar:/Applications/Android Studio 2.app/Contents/lib/trove4j.jar:/Applications/Android Studio 2.app/Contents/lib/jna.jar:/Applications/Android Studio 2.app/Contents/jre/jdk/Contents/Home/lib/tools.jar)
		at com.sun.jna.Native.extractFromResourcePath(Native.java:1095)
		at com.sun.jna.NativeLibrary.loadLibrary(NativeLibrary.java:276)
		... 80 more
```

## 2021-01-14 Thu

### NCM

fcp 不能直接添加 ncm 格式的音频

这个网站方便

[NCM TO MP3](https://ncm.worthsee.com/)

### Android 

[轮子收集仓库](https://github.com/Vension/V-AndroidCollectSources)

### Android File

[Android7.0以上通过FileProvider访问文件](https://www.jianshu.com/p/bd8a80ecba3f)

[Android遍历某个文件夹的图片并实现滑动查看的的Gallery](https://www.cnblogs.com/sfshine/archive/2012/06/26/2742899.html)

[加载本地图片模糊，Glide加载网络图片却很清晰](https://blog.csdn.net/weixin_33998125/article/details/91362039?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-1.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-1.control)

### Archive

[ibiblio - The Public's Library and Digital Archive](https://www.ibiblio.org/)

## Apollo-11

cool

[Github Repo](https://github.com/chrislgarry/Apollo-11)

## Git

[Linus Torvalds](https://zh.wikipedia.org/wiki/%E6%9E%97%E7%BA%B3%E6%96%AF%C2%B7%E6%89%98%E7%93%A6%E5%85%B9)

## 2021-01-09 Sat

### Hugo

[hugo编译出的页面没有样式怎么办？](https://www.zhihu.com/question/414295803/answer/1410344932)

- 智障了忘记改baseurl

`single.html` 要放到 `layouts/_default/` 下

### favicon

[https://realfavicongenerator.net/](https://realfavicongenerator.net/)

这个生成 favicon 也太方便了8

## 2021-01-08 Fri

### Android 技术博客

[这些年“崛起”的Android技术博主们](https://mp.weixin.qq.com/s?__biz=MzAxMTI4MTkwNQ==&mid=2650830613&idx=1&sn=9bb52bde515a787f3bb3e46a45baf221&chksm=80b7a38bb7c02a9d9905903eb035cd9e85de9f0cce52c768e27fc84640eff291d1ade82fa211&scene=178&cur_album_id=1374912898463776768#rd)

感觉我现在还没有足够的输出能力

先加油输入吧=。=

### 杂

[【何同学】这视频能让你戒手机](https://www.bilibili.com/video/BV1ev411x7en)

属实，最有效的方法就是在拿起手机后不解锁又放下

把小何说的三句话加到了我的壁纸上

- 你为什么要打开手机
- 你要看多长时间
- 你还能去做什么

## 2021-01-04 Mon

### Keynote

[在 Mac 上用 Keynote 讲演将演示文稿发布到博客中](https://support.apple.com/zh-cn/guide/keynote/tan256005c23/mac)

- cool 巨方便
- 感觉比 PPT 的那个共享好用点

## 2021-01-03 Sun

### Money Wiz

开始用号称最厉害的记账软件？

[从零开始搭建完善的记账体系](https://sspai.com/post/58025)

- 啊，上手之后真滴很好用

