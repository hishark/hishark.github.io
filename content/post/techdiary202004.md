---
title: 四月 の 技术日记
date: 2020-04-01 22:27:09
tags:
- TechDiary
categories: 
- 技术日记
authors: 
- hishark777
---
这里是777的四月份bb日记
<!--more-->

<!-- # 日记打卡
|  一  |  二  |  三  |  四  |  五  |  六  |  日  |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: |
|      |      |  <font color="#B22222">**1**   |  <font color="#B22222">**2**   |  <font color="#B22222">**3**   |  <font color="#B22222">**4**   |  5   |
|  <font color="#B22222">**6**   |  7   |  <font color="#B22222">**8**   |  9   |  10  |  11  |  12  |
|  13  |  <font color="#B22222">**14**  |  <font color="#B22222">**15**  |  <font color="#B22222">**16**  |  <font color="#B22222">**17**  |  18  |  19  |
|  20  |  <font color="#B22222">**21**  |  22  |  <font color="#B22222">**23**  |  <font color="#B22222">**24**  |  25  |  26  |
|  27  |  <font color="#B22222">**28**  |  <font color="#B22222">**29**  |  30  |      |      |      | -->


## 2020-04-29
### **Educative**

种草了几门课 观望一下

### **En**

> Educative’s courses were made to help you learn faster, and get your hands dirty along the way.

我想了半天怎么会帮我弄脏手，查了一下是亲身体验的意思。
## 2020-04-28
### **Room Database Viewer**

[Database Navigator](https://plugins.jetbrains.com/plugin/1800-database-navigator)

[SQLite Browser](https://sqlitebrowser.org/dl/)

[View contents of database created with Room Persistence Library](https://stackoverflow.com/questions/44429372/view-contents-of-database-created-with-room-persistence-library)

[Android Debug Database无法浏览Android Room创建的数据库信息](https://my.oschina.net/u/3157597/blog/1790201) - 奇怪哦 我就是databaseBuilder可是没用？而且ADD现在github上写的是支持Room inMemory诶？ 破案了，不能自定义路径！！

[How can I use Stetho with RoomDataBase in Android Studio?](https://stackoverflow.com/questions/54424594/how-can-i-use-stetho-with-roomdatabase-in-android-studio)

### **Other**

[执行 brew install 命令长时间卡在 Updating Homebrew 的解决方法](https://learnku.com/articles/18908)

### **Room**

[Android room persistent library - TypeConverter error of error: Cannot figure out how to save field to database"](https://stackoverflow.com/questions/44582397/android-room-persistent-library-typeconverter-error-of-error-cannot-figure-ou) - List

[定义对象之间的关系](https://developer.android.com/training/data-storage/room/relationships?hl=zh-cn) - Room不允许实体对象互相引用哦 和大多数ORM框架不一样！

## 2020-04-24
### **ConstraintLayout**

下面两篇杠上了啊哈哈哈哈哈哈

[约束布局ConstraintLayout看这一篇就够了](https://www.jianshu.com/p/17ec9bd6ca8a)

[ConstraintLayout,看完一篇真的就够了么？](https://juejin.im/post/5d12c4146fb9a07ea33c24b7)

话说ConstraintLayout里面是不支持嵌套LinearLayout嘛目前没用

之后看看

### **Bug**

[关于Linearlayout中控件设置为其底部的问题,android:layout_gravity="bottom"没效果](https://blog.csdn.net/y_panda520/article/details/50952438)

[http://awuxiaolong.me/2017/07/19/mac-adb-gradlew/](http://awuxiaolong.me/2017/07/19/mac-adb-gradlew/)

[https://blog.csdn.net/Picasso_L/article/details/53085299](https://blog.csdn.net/Picasso_L/article/details/53085299)

### **坑**

app:layout_constraintBottom_toBottomOf="@+id/ll_record_pic"

app:layout_constraintTop_toBottomOf="@+id/ll_record_pic"

两个效果不一样啊看清楚了

### **Android**

[Android中修改ArrayAdapter字体以及颜色](https://www.cnblogs.com/macher/p/5077388.html)

### **AndroidX**

glide最新4.0的版本是用的androidX

掌超项目之前用的都是surpport

这样很多类都冲突了很麻烦

所以glide用3.7就好了哈哈哈哈

implementation 'com.github.bumptech.glide:glide:3.7.0'
implementation 'com.android.support:support-v4:23.2.1'

### **杂**

我觉得我还是少运行

不要加一两行代码就运行

至少写完一整个功能再去测试

不然运行n次好浪费时间

## 2020-04-23
### **Kotlin**

[2D Array in Kotlin](https://stackoverflow.com/questions/34145495/2d-array-in-kotlin)

[Kotlin Queue tutorial with examples](https://bezkoder.com/kotlin-queue/)

### **AS**

as新建一个java括号莫名其妙跑到新的一行了 改回end of line

[Android Studio修改大括号位置](https://blog.csdn.net/tyndale1993/article/details/50369954)

### **Android**

[ConstraintLayout](https://www.jianshu.com/p/17ec9bd6ca8a) 稳定版1.1.3，出了2.0beta：[https://developer.android.com/jetpack/androidx/releases/constraintlayout](https://developer.android.com/jetpack/androidx/releases/constraintlayout)

[Android—Room数据库](https://www.jianshu.com/p/cfde3535233d)

[Android 设置横屏或竖屏 设置全屏](https://blog.csdn.net/bear_huangzhen/article/details/46618475)

### **Error**

[You need to use a Theme.AppCompat theme (or descendant) with this activity.](https://blog.csdn.net/ouyang_peng/article/details/51334761)

### **Room**

@Dao
public interface PatientDao { ...
}
不要extends Dao，CURD不写全会报错

## 2020-04-21
### **讯飞语音听写**

[https://www.xfyun.cn/doc/asr/voicedictation/Android-SDK.html](https://www.xfyun.cn/doc/asr/voicedictation/Android-SDK.html)

集成到新增病历里头去

### **Algorithm**

看到好几个位运算题目都不想做，囤一下之后一次多做几个

### **Kotlin**

[https://try.kotlinlang.org/](https://try.kotlinlang.org/)

[https://www.yiibai.com/kotlin/kotlin-hashmap.html](https://www.yiibai.com/kotlin/kotlin-hashmap.html)

在看郭霖新出的第一行代码

新增了Kotlin的内容

郭神还是稳

写得好好

不过书好厚啊 要有电子版就更好看了OTZ

另外感觉之后做leetcode一个题可以分别用java和kotlin实现一下

或许可以建一个新仓库

建好了嘎嘎嘎 [LeetCode J&K](https://www.yuque.com/xiaoqizhang/leetcode)

### **Bug**

[https://stackoverflow.com/questions/57664688/kotin-type-mismatch-inferred-type-is-int-but-int-was-expected](https://stackoverflow.com/questions/57664688/kotin-type-mismatch-inferred-type-is-int-but-int-was-expected)

[https://stackoverflow.com/questions/9562315/in-kotlin-how-can-i-convert-an-int-to-an-int](https://stackoverflow.com/questions/9562315/in-kotlin-how-can-i-convert-an-int-to-an-int) ⭐️

### **杂**

之前做阿里云直播/视频会议/环信视频会议的时候

都忘记记下集成的流程以及途中遇到的坑

这次搞讯飞语音听写要记录下来

每发现一个好用的软件我都要开心一会儿

toggl本周最佳

全平台同步而且同步太牛批了👍

## 2020-04-17
### **Android**

[事件处理之onTouchEvent()和onTouch()方法精炼详解](https://blog.csdn.net/weixin_41101173/article/details/80460632)

[Android 画直线并实现拖动](https://www.bbsmax.com/A/gVdnEKVN5W/)

[paint画虚线的问题](https://blog.csdn.net/sollian/article/details/38038377)

[PathEffect类简单认识](https://www.iteye.com/blog/androidbin-1487567)

[Android 自定义View之绘图](https://www.jianshu.com/p/76603b122fb4)

[教程 挺全](https://www.twle.cn/l/yufei/android/android-basic-index.html)

### **Other**

找了一晚上bug结果是width和height两个为0所以看不到线

我吐血啦

## 2020-04-16
### **Canvas**

[可绘制对象概览](https://developer.android.com/guide/topics/graphics/drawables)

onTouchEvent 解决移动的问题

### **Other**

微博上看到一个好的idea

想要尝试做出来

have a try!

## 2020-04-15
### **Spinner**

这玩意官方中文名居然叫微调框 怎么不叫下拉框！

[https://developer.android.com/guide/topics/ui/controls/spinner?hl=zh-cn](https://developer.android.com/guide/topics/ui/controls/spinner?hl=zh-cn)

### **Canvas**

- 🔲[https://developer.android.com/reference/android/graphics/Canvas](https://developer.android.com/reference/android/graphics/Canvas)

[https://juejin.im/post/5be29aa2e51d45228170ff33](https://juejin.im/post/5be29aa2e51d45228170ff33)

### **View**

- ✅[https://blog.csdn.net/carson_ho/article/details/56009827](https://blog.csdn.net/carson_ho/article/details/56009827)

### **杂**

最近老跑医院啊...

希望家人都平平安安

## 2020-04-14
### **Android**

[Android入门——利用Canvas完成绘制点、圆、直线、路径、椭圆、多边形等2D图形](https://blog.csdn.net/CrazyMo_/article/details/48931681)

### **Other**

[mkdocs-material](https://github.com/squidfunk/mkdocs-material) 这个看起来不错诶，有空试试


## 2020-04-08
### **Android**

1. 在android开发时，很多时候我们会使用可视化界面创建数据库，或者拿到别人的数据库使用，这时就需要我们将db文件手动加入到文件夹中并读取。但是当我们把应用的apk部署到真机上的时候，已经创建好的数据库及其里边的数据是不能随着apk一起安装到真机上的。

[https://blog.csdn.net/x15037308498/article/details/79458655](https://blog.csdn.net/x15037308498/article/details/79458655)

1. [Android SharedPreferences 卸载 App 后还存在如何解决](https://blog.csdn.net/guozhaohui628/article/details/88936079)
2. APP卸载后，如果数据库在默认的`/data/data`路径下，那么数据库也会被清除。如果在自定义到`/sdcard/`目录下就不会被清除。
3. Room升级数据库时，如果不需要保留数据，可以直接使用`fallbackToDestructiveMigration`。
4. [How to change the default database file location of Room DataBase](https://stackoverflow.com/questions/48903918/how-to-change-the-default-database-file-location-of-room-database)?

自定义room数据库存储的位置（不用root）

1. Room数据库数据导出后在Project目录下才找得到，Android目录下找不到哈。

![https://cdn.nlark.com/yuque/0/2020/png/1063797/1586329205542-5733176f-562e-4a69-89d8-8dad8acb4898.png](https://cdn.nlark.com/yuque/0/2020/png/1063797/1586329205542-5733176f-562e-4a69-89d8-8dad8acb4898.png)

1. 开发时，不停的重新build app，数据库db和自动生成的db-wal不变，db-shm随着每次重新build而更新，我还不知道这俩的作用和区别。先放着。

    ![https://cdn.nlark.com/yuque/0/2020/png/1063797/1586331394783-7f114584-77e6-4316-995b-801dd93e22af.png](https://cdn.nlark.com/yuque/0/2020/png/1063797/1586331394783-7f114584-77e6-4316-995b-801dd93e22af.png)

2. [ToggleButton](https://developer.android.com/guide/topics/ui/controls/togglebutton)

A toggle button allows the user to change a setting between two states.

1. 适配问题

[https://www.jianshu.com/p/1302ad5a4b04](https://www.jianshu.com/p/1302ad5a4b04)

- 🔲搞清楚dimens适配

### **Error**

有个报错一闪而过

先复制过来记一下明天看

```java
I/Choreographer: Skipped 42 frames! The application may be doing too much work on its main thread.
I/super.usb.debu: Compiler allocated 5370KB to compile void com.viewphii.ussuper.MsActivity.onCreate(android.os.Bundle)
D/MesureSurfaceView: surfaceCreated() surfaceChanged() w = 0 -> 1045
D/ViewphiiUSSuper: .MsSurfaceView#surfaceChanged[268] Enter
D/MesureSurfaceView: doDraw()
D/MesureSurfaceView: doDraw() : canvas(w, h) = (1045, 888) doDraw() : canvas_W = 1045 doDraw() : centerLine = 0 doDraw() : drawBmp == null
D/ViewphiiUSSuper: .MsSurfaceView#surfaceChanged[268] Leave
E/ActivityThread: Activity com.viewphii.ussuper.MsActivity has leaked IntentReceiver com.viewphii.ussuper.MsActivity$6@6f85294 that was originally registered here. Are you missing a call to unregisterReceiver()? android.app.IntentReceiverLeaked: Activity com.viewphii.ussuper.MsActivity has leaked IntentReceiver com.viewphii.ussuper.MsActivity$6@6f85294 that was originally registered here. Are you missing a call to unregisterReceiver()? at android.app.LoadedApk$ReceiverDispatcher.<init>(LoadedApk.java:1588) at android.app.LoadedApk.getReceiverDispatcher(LoadedApk.java:1368) at android.app.ContextImpl.registerReceiverInternal(ContextImpl.java:1515) at android.app.ContextImpl.registerReceiver(ContextImpl.java:1488) at android.app.ContextImpl.registerReceiver(ContextImpl.java:1476) at android.content.ContextWrapper.registerReceiver(ContextWrapper.java:627) at com.viewphii.ussuper.MsActivity.onCreate(MsActivity.java:1651) at android.app.Activity.performCreate(Activity.java:7825) at android.app.Activity.performCreate(Activity.java:7814) at android.app.Instrumentation.callActivityOnCreate(Instrumentation.java:1306) at android.app.ActivityThread.performLaunchActivity(ActivityThread.java:3245) at android.app.ActivityThread.handleLaunchActivity(ActivityThread.java:3409) at android.app.servertransaction.LaunchActivityItem.execute(LaunchActivityItem.java:83) at android.app.servertransaction.TransactionExecutor.executeCallbacks(TransactionExecutor.java:135) at android.app.servertransaction.TransactionExecutor.execute(TransactionExecutor.java:95) at android.app.ActivityThread$H.handleMessage(ActivityThread.java:2016) at android.os.Handler.dispatchMessage(Handler.java:107) at android.os.Looper.loop(Looper.java:214) at android.app.ActivityThread.main(ActivityThread.java:7356) at java.lang.reflect.Method.invoke(Native Method) at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:492) at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:930)
D/History#: doSort() : 0 doSortDate() : false
D/History#: doSort() : Loop END doSort() : View Start setGridView()
D/History#: setListView()
D/History#: doSort() : View END
I/OpenGLRenderer: Davey! duration=862ms; Flags=1, IntendedVsync=617069625672818, Vsync=617070325672790, OldestInputEvent=9223372036854775807, NewestInputEvent=0, HandleInputStart=617070332748090, AnimationStart=617070332853871, PerformTraversalsStart=617070332898194, DrawStart=617070443047163, SyncQueued=617070450537685, SyncStart=617070450742945, IssueDrawCommandsStart=617070451586643, SwapBuffers=617070484228782, FrameCompleted=617070488713209, DequeueBufferDuration=3021000, QueueBufferDuration=208000,
D/ViewphiiUSSuper: .MsActivity#changeStartStopButton172[7839] Enter .SettingsParamSharedPreferences#<init>[24] Enter
D/ViewphiiUSSuper: .SettingsParamSharedPreferences#<init>[24] Leave
D/ViewphiiUSSuper: .MsActivity#changeStartStopButton172[7839] Leave
D/ViewphiiUSSuper: .MsActivity#changeStartStopButton172[7839] Enter .SettingsParamSharedPreferences#<init>[24] Enter
D/ViewphiiUSSuper: .SettingsParamSharedPreferences#<init>[24] Leave .MsActivity#changeStartStopButton172[7839] Leave
D/ViewphiiUSSuper: .MsActivity#changeStartStopButton172[7839] Enter
D/ViewphiiUSSuper: .SettingsParamSharedPreferences#<init>[24] Enter .SettingsParamSharedPreferences#<init>[24] Leave
D/ViewphiiUSSuper: .MsActivity#changeStartStopButton172[7839] Leave
D/ViewphiiUSSuper: com.viewphii.customview.SettingView#updateWpsBtn[252] Enter
D/ViewphiiUSSuper: .SettingsParamSharedPreferences#<init>[24] Enter .SettingsParamSharedPreferences#<init>[24] Leave
D/ViewphiiUSSuper: com.viewphii.customview.SettingView#updateWpsBtn[252] Leave com.viewphii.customview.SettingView#updateWpsBtn[253] Enter
D/ViewphiiUSSuper: com.viewphii.customview.SettingView#updateWpsBtn[253] Leave
D/ViewphiiUSSuper: .MsActivity#changeStartStopButton172[7839] Enter .SettingsParamSharedPreferences#<init>[24] Enter .SettingsParamSharedPreferences#<init>[24] Leave .MsActivity#changeStartStopButton172[7839] Leave
D/ViewphiiUSSuper: .MsActivity#changeStartStopButton172[7839] Enter .SettingsParamSharedPreferences#<init>[24] Enter .SettingsParamSharedPreferences#<init>[24] Leave .MsActivity#changeStartStopButton172[7839] Leave
D/ViewphiiUSSuper: .MsActivity#changeStartStopButton172[7839] Enter .SettingsParamSharedPreferences#<init>[24] Enter
D/ViewphiiUSSuper: .SettingsParamSharedPreferences#<init>[24] Leave .MsActivity#changeStartStopButton172[7839] Leave
D/ViewphiiUSSuper: com.viewphii.customview.SettingView#updateWpsBtn[252] Enter .SettingsParamSharedPreferences#<init>[24] Enter .SettingsParamSharedPreferences#<init>[24] Leave com.viewphii.customview.SettingView#updateWpsBtn[252] Leave
D/ViewphiiUSSuper: com.viewphii.customview.SettingView#updateWpsBtn[253] Enter com.viewphii.customview.SettingView#updateWpsBtn[253] Leave
D/### MsActivity ###: RequestPowerOff()
D/WifiControl: ReqWait()#commandId：15 getRequestNumber() sendMsg★ ① mUSSocket が NULLではない★ sendMsg★ ②
D/SensorParameter: loadPreset(name, send) = (Unconnected, false)
D/ViewphiiUSSuper: .MsActivity$117#run[6262] Enter
D/WifiControl: reqDisconnection() reqWiFiDisconnection()★mUSSocket が NULLでない reqDisconnection()#① reqWiFiDisconnection()# successfully?：true
D/ViewphiiUSSuper: .MsActivity$117#run[6262] Leave
D/WifiControl: terminate()
D/ViewphiiUSSuper: .ViewphiiApplication#terminate[248] Enter
D/ViewphiiUSSuper: .WifiControl#terminate[917] Enter
E/ViewphiiUSSuper: .BaseSocket#terminate[182] disconnect java.lang.NullPointerException: Attempt to invoke virtual method 'void android.hardware.usb.UsbDeviceConnection.close()' on a null object reference
D/ViewphiiUSSuper: .WifiControl#terminate[917] Leave .ViewphiiApplication#terminate[248] Leave
D/ViewphiiApplication: ┌──────────────────────────────────────────────────────────────────────────────────────────────────────────────── │ main, com.viewphii.ussuper.ViewphiiApplication.setSsid(ViewphiiApplication.java:287) ├┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄ │ args[0] = ViewphiiApplication │ args[1] = setSsid() └────────────────────────────────────────────────────────────────────────────────────────────────────────────────
D/WifiControl: CONNECTION：切断
D/ViewphiiUSSuper: .MsActivity#changeStartStopButton172[7839] Enter .SettingsParamSharedPreferences#<init>[24] Enter .SettingsParamSharedPreferences#<init>[24] Leave .MsActivity#changeStartStopButton172[7839] Leave
D/ViewphiiUSSuper: .MsActivity#changeStartStopButton172[7839] Enter .SettingsParamSharedPreferences#<init>[24] Enter .SettingsParamSharedPreferences#<init>[24] Leave
D/ViewphiiUSSuper: .MsActivity#changeStartStopButton172[7839] Leave
D/WifiControl: CONNECTION：切断
D/ViewphiiUSSuper: .MsActivity#changeStartStopButton172[7839] Enter .SettingsParamSharedPreferences#<init>[24] Enter .SettingsParamSharedPreferences#<init>[24] Leave .MsActivity#changeStartStopButton172[7839] Leave
D/ViewphiiUSSuper: .MsActivity#changeStartStopButton172[7839] Enter .SettingsParamSharedPreferences#<init>[24] Enter .SettingsParamSharedPreferences#<init>[24] Leave .MsActivity#changeStartStopButton172[7839] Leave
D/WifiControl: CONNECTION：切断
D/ViewphiiUSSuper: .MsActivity#prepareForReconnect[10369] Enter
D/WifiControl: reqDisconnection() reqWiFiDisconnection()★mUSSocket が NULLでない reqDisconnection()#①
D/AndroidRuntime: Shutting down VM
E/AndroidRuntime: FATAL EXCEPTION: main Process: com.viewphii.ussuper.usb.debug, PID: 4601 java.lang.NullPointerException: Attempt to invoke virtual method 'android.os.Message android.os.Handler.obtainMessage(int, java.lang.Object)' on a null object reference at com.viewphii.ussuper.BaseSocket.disconnect(BaseSocket.java:428) at com.viewphii.ussuper.WifiControl.reqWifiDisconnection(WifiControl.java:864) at com.viewphii.ussuper.WifiControl.reqDisconnection(WifiControl.java:839) at com.viewphii.ussuper.MsActivity.prepareForReconnect(MsActivity.java:10369) at com.viewphii.ussuper.WifiControl$WifiConHandler$1.run(WifiControl.java:547) at android.app.Activity.runOnUiThread(Activity.java:6923) at com.viewphii.ussuper.WifiControl$WifiConHandler.handleMessage(WifiControl.java:544) at android.os.Handler.dispatchMessage(Handler.java:107) at android.os.Looper.loop(Looper.java:214) at android.app.ActivityThread.main(ActivityThread.java:7356) at java.lang.reflect.Method.invoke(Native Method) at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:492) at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:930)
D/CrashHandler: 异常信息->com.viewphii.ussuper.BaseSocket.disconnect(BaseSocket.java:428)
W/CrashHandler: ┌──────────────────────────────────────────────────────────────────────────────────────────────────────────────── │ Thread-5, com.viewphii.ussuper.CrashHandler$1.run(CrashHandler.java:164) ├┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄ │ Exception:+ │ java.lang.NullPointerException: Attempt to invoke virtual method 'android.os.Message android.os.Handler.obtainMessage(int, java.lang.Object)' on a null object reference │ at com.viewphii.ussuper.BaseSocket.disconnect(BaseSocket.java:428) │ at com.viewphii.ussuper.WifiControl.reqWifiDisconnection(WifiControl.java:864) │ at com.viewphii.ussuper.WifiControl.reqDisconnection(WifiControl.java:839) │ at com.viewphii.ussuper.MsActivity.prepareForReconnect(MsActivity.java:10369) │ at com.viewphii.ussuper.WifiControl$WifiConHandler$1.run(WifiControl.java:547) │ at android.app.Activity.runOnUiThread(Activity.java:6923) │ at com.viewphii.ussuper.WifiControl$WifiConHandler.handleMessage(WifiControl.java:544) │ at android.os.Handler.dispatchMessage(Handler.java:107) │ at a └──────────────────────────────────────────────────────────────────────────────────────────────────────────────── ┌──────────────────────────────────────────────────────────────────────────────────────────────────────────────── │ ndroid.os.Looper.loop(Looper.java:214) │ at android.app.ActivityThread.main(ActivityThread.java:7356) │ at java.lang.reflect.Method.invoke(Native Method) │ at com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:492) │ at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:930) └────────────────────────────────────────────────────────────────────────────────────────────────────────────────
I/Process: Sending signal. PID: 4601 SIG: 9
```

## 2020-04-06
### **ORM**

Object Relation Mapping 对象关系映射

简单来讲，我们使用的编程语言是面向对象语言，而使用的数据库则是关系型数据库，将面向对象的语言和面向关系的数据库之间建立一种映射关系，这就是ORM了。

使用ORM框架的好处：可以用面向对象的思维来和数据库进行交互，绝大多数情况下不用在再和SQL语句打交道了，同时也不用担心操作数据库的逻辑会让项目的整体代码变得混乱。

### **Java**

[varargs 可变参数使用](https://www.runoob.com/java/method-varargs.html)

# 2020-04-04
> 404 Not Found

### **Blog**

昨晚通宵了

1. 把Gitbook迁移到语雀（语雀牛批
2. 更换为国内CDN（访问速度变快太多了TuT
3. 添加评论系统（果然还是valine最快最好用！
4. 添加不蒜子访问统计（换了个域名都清零了 重新来过啦
5. 修改默认的配色（icarus好像没有一键修改主题色的选项 于是一边F12一边在css文件里修改
6. 买了本书（刷到郭神的公众号发现出新书了 用kotlin更新了《第一行代码》正好买来边学kotlin边复习一下android一些基础知识

### **Color**

修改配色的时候发现[w3school的颜色转换](https://www.w3schools.com/colors/colors_hexadecimal.asp)特别好用

以前在用的还有[RGB转16进制](https://www.sioe.cn/yingyong/yanse-rgb-16/)

### **Algorithm**

以前做算法题老是有意无意的无视题解下方的复杂度分析

不能这样子啦以后每次都好好看一下！

Github的Algorithm仓库慢慢被我堆起来了

每天一题感觉好像有点太少啊

有时间的话就多做两题

### **Java**

[Stack](https://www.runoob.com/java/java-stack-class.html)

### **Other**

时间真的是海绵🧽

挤一挤一定会有的

我还以为语雀这边是markdown编辑器结果原来是富文本编辑器

不过也挺好用的

## 2020-04-03
### **CDN**

今天突然发现icarus官网上的这篇blog：[Speed up Your Site with Custom CDN](https://blog.zhangruipeng.me/hexo-theme-icarus/Configuration/Theme/speed-up-your-site-with-custom-cdn/)

然后照着[hexo-theme-icarus 国内加速](https://www.hongfs.cn/2019/01/javascript/hexo-theme-icarus-domestic-acceleration/)修改了一下博客配置

访问速度chuachua的上去了555开心

## 2020-04-02
### **Icon**

使用Image Asset Studio创建应用图标

以前都没怎么用过这个

[https://developer.android.com/studio/write/image-asset-studio?hl=zh-cn](https://developer.android.com/studio/write/image-asset-studio?hl=zh-cn)

### **androidx**

[https://www.jianshu.com/p/41de8689615d](https://www.jianshu.com/p/41de8689615d)

### **杂**

感觉每周可以用周末的空闲时间来把这边记的一些东西给看了

看完标个已读哈哈

### **Room对比其他数据库框架**

[https://android.ctolib.com/EdisonLiao-DBDemo.html](https://android.ctolib.com/EdisonLiao-DBDemo.html)

## 2020-04-01
### **Android**

1. [https://juejin.im/post/5bac92f2f265da0aba70c1bf](https://juejin.im/post/5bac92f2f265da0aba70c1bf)找时间补一下这个
2. [https://www.jianshu.com/p/7286e1be14fa](https://www.jianshu.com/p/7286e1be14fa)相对布局 有些记不清楚

### **RxJava**

[https://github.com/ReactiveX/RxJava](https://github.com/ReactiveX/RxJava)