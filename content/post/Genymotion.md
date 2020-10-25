---
title: 使用Genymotion运行基于ARM架构的APP
date: 2020-04-01 15:55:55
tags:
- Android
categories: 学习笔记
---
前阵子需要做个直播demo，用到了阿里云的直播sdk，阿里云文档中说明了只支持arm架构的cpu，而Android Studio自带的模拟器只能顺畅的跑x86架构的虚拟机，跑arm64架构的简直卡成树懒，查了一下发现Android Studio自带的AVD就是这个德行，遂放弃，转用Genymotion。

二月底决定毕业找Android岗的时候，下单了一台Pixel 2XL做自己以后的测试机，这篇文章写于购入Pixel之前，现在发现真机+模拟器一起用的测试环境还是挺舒服的。BTW谷歌亲儿子是真的好用啊，原生Android太香了，不出啥意外的话我以后就是iPhone主力机+Pixel备用机的快乐配置了哈哈哈哈哈。

好的扯远了，聊正事。
<!--more-->
## 1. Android中的CPU架构
一开始还没弄懂Android里面arm和x86这堆玩意，看到一篇博客说得比较清楚：[说说Android项目中的armeabi，armeabi-v7a和x86](https://www.jianshu.com/p/ed9c3fea3584)。

## 2. 安装Genymotion个人使用版本
Genymotion是一个收费软件，但是[个人使用](https://www.genymotion.com/fun-zone/)是免费的，对个人开发者还是很友好的哈！很喜欢这个页面的slogan：
>Genymotion for fun.

安装和配环境的话谷歌教程一大堆，我记得当初我用windows装的时候还挺曲折，这次在macos上装起来挺顺的。
## 3. 遇到的问题
安装完genymotion后会不可避免地遇到两个问题，逐个进行解决。
### 3.1 模拟器下载过慢
打开Genymotion后，添加新设备会发现下载进程缓慢，进度条卡住不动，这个时候打开terminal进入`/Users/a777/.Genymobile/`路径下，打开`genymotion.log`文件，查看最近的日志记录，找到下面这行：
```
2020-04-02T01:30:18+08:00 [Genymotion:59491] [debug] Starting download of "https://dl.genymotion.com/dists/9.0/ova/genymotion_vbox86p_9.0_190715_123003.ova"
```
从里面揪出下载地址`https://***.ova`，复制之后打开迅雷，迅雷很快就可以下载完成。

接着进入到`/Users/a777/.Genymobile/Genymotion/ova`路径下，会发现有一个名为`genymotion****.ova.partial`的同名文件，把刚刚用迅雷下好的ova文件覆盖掉这个文件即可。
### 3.2 无法支持ARM架构
第一个问题解决之后，就可以顺利打开虚拟机了。但是由于阿里云直播的SDK是针对ARM架构的，而Genymotion的虚拟机和AS中自带的虚拟机一样，都默认为x86架构，所以需要借助第三方工具来实现，有个大佬写了轮子可以让虚拟机完美支持ARM架构：[Genymotion_ARM_Translation](https://github.com/m9rco/Genymotion_ARM_Translation)。

这位哥们至今还在维护，我刚去仓库看了一眼7天前他刚刚更新了针对Android7.x版本的翻译包，天使。

这个轮子使用起来也非常简单，下载好虚拟机对应版本的zip包之后，把zip包拖进虚拟机安装即可，装完再重启虚拟机就可以愉快地使用啦！
## 4. 完
上面这一通走完其实也挺麻烦了，现在Android手机基本上都是ARM架构所以就没啥问题了，直接在真机上运行就好啦～不得不用虚拟机的时候就这么整吧！
## 参考链接
- https://www.jianshu.com/p/df19fa59bf23
- https://www.cnblogs.com/wotoufahaiduo/p/11674449.html
- https://github.com/m9rco/Genymotion_ARM_Translation