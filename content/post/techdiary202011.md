---
title: "十一月学习废话集"
date: 2020-11-02T14:27:04+08:00
draft: false
categories: 
- 技术日记
tags:
- TechDiary
draft: false
authors:
- hishark777
---

2020年倒计时开始

<!--more-->

## 2020-11-11

### java xml



### dicom

[dicom 文件 tag 详解](https://blog.csdn.net/wenzhi20102321/article/details/75127101)

[dicom view](https://www.dicomgo.com/dgv/viewer#/view)

## 2020-11-10

### jpg png

[invalid JPEG format: missing SOI marker](https://stackoverflow.com/questions/50358935/invalid-jpeg-format-missing-soi-marker)

- 好不容易找到个回答结果发现带jpg后缀的图片实际上是个 png - -爷吐辽

[PNG文件头格式解析](https://blog.csdn.net/u013943420/article/details/76855416)

[JPEG文件编/解码详解](https://blog.csdn.net/yuan892173701/article/details/8710316)

- 我用 HexFriend 打开了一个带 jpg 后缀的图片看到了 PNG 的文件头 苍天啊

哦，原有代码太奇怪了为什么按照 PNG 的格式生成但是又给个 jpg 后缀，奇奇怪怪

不管了反正找到问题了改好了- - 

### jar

[android 添加 jar 包](https://www.cnblogs.com/candyzhmm/p/11721557.html)

### 杂

明天双十一

还没想好买啥 

想买个灰色牛角扣咧

## 2020-11-09

### 设计模式

[说说MVP](https://xiaozhuanlan.com/topic/0642317958)

### WinHex替代

winhex 只能在 windows 上用，macos上找到了完美替代：

- [HexFriend](https://github.com/ridiculousfish/hexfiend)

### Launchpad

烦死咯啥法子都试了，有个程序就是死活没法显示到启动台里OTZ 

[Apple Doc](https://support.apple.com/zh-cn/guide/mac-help/mh35840/mac)

[MacOS启动台(launchpad)缺少应用软件图标](https://blog.csdn.net/weixin_43735348/article/details/105218458)

### Error

[Unable to resolve dependency for ':app@debug/compileClasspath': Could not resolve com.android.support:appcompat-v7:26.1.0](https://stackoverflow.com/questions/46999594/unable-to-resolve-dependency-for-appdebug-compileclasspath-could-not-resolv)

- File -> invalidate caches/Restart Then select invalidate and restart 妥    

## 2020-11-08

### Java

[compareTo()](https://www.runoob.com/java/java-string-compareto.html)用于两种方式的比较

- 字符串与对象进行比较
- 按照字典顺序比较两个字符串 `a.compareTo(b)`
  - a == b return`0`
  - a < b return `<0`
  - a > b return `>0`

[Comparator - 1](https://www.cnblogs.com/skywang12345/p/3324788.html)

[Comparator - 2](https://zhuanlan.zhihu.com/p/54004622)

## 2020-11-06

### Java

[String.split](https://www.cnblogs.com/wzj4858/p/8204967.html)

- 别忘记转义字符 `.` 和 `|` 

### Android

[CircularArray](https://developer.android.com/reference/androidx/collection/CircularArray)

- 延展：[Circular Buffer - Wiki](https://zh.wikipedia.org/wiki/%E7%92%B0%E5%BD%A2%E7%B7%A9%E8%A1%9D%E5%8D%80)

### Jpeg

[理解jpeg文件头的格式](https://blog.csdn.net/ryfdizuo/article/details/41250775)

[jpeg图片格式详解](https://blog.csdn.net/yun_hen/article/details/78135122)

### Android - OpenCV

[Android OpenCV（零）：OpenCV Android SDK](https://juejin.im/post/6871382621017309197)

### Blog

[网易云音乐大前端团队](https://juejin.im/user/4265760847567016)

### Dicom View

[DicomGo-Web](https://www.dicomgo.com/dgv/viewer#/view)

## 2020-11-05

### adb

[[解决 'adb root' 时提示 'adbd cannot run as root in production builds'](https://www.cnblogs.com/jeason1997/p/12410537.html)](https://www.cnblogs.com/jeason1997/p/12410537.html)

[/system/bin/sh: su: not found的解决办法](https://blog.csdn.net/TheWhiteFox/article/details/84142524)

## 2020-11-03

### 存储

[数据和文件存储概览](https://developer.android.com/guide/topics/data/data-storage?hl=zh-cn)

- 内部文件存储 - 在设备文件系统中存储应用私有文件
- 外部文件存储 - 在共享外部文件系统中
- 共享首选项 - SharedPreferences
- 数据库 - Room

### 建立私密连接

[您的时钟快了](https://blog.csdn.net/qq_43543789/article/details/107858871)

- Pixel 碰到了这个问题，把时间对准了还是没用，琢磨大半天还重置了手机都不行，最后发现是我日期忘记对准了我哭了哈，那么大一个4月我是怎么看成11月的？？

[Android Emulator “Chain Validation Failed” connecting developers machine with self-signed cert](https://stackoverflow.com/questions/45923747/android-emulator-chain-validation-failed-connecting-developers-machine-with-se)

- A cause of this problem can be wrong date time of the device
- Yes

### 粘包现象

[TCP的粘包现象](https://blog.csdn.net/wuxing26jiayou/article/details/79863528)

### 杂

今天和鲂聊了一通

我太佩服会输出的人啦！

加油加油