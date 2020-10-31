---
title: LeanCloud中国版迁移至国际版
date: 2019-09-30 09:35:44
tags: 
- LeanCloud
- Valine
categories: 学习笔记
authors:
- hishark777
---
昨天小翁提醒我LeanCloud中国版要停止没绑定备案域名的应用服务了，刚打算把评论系统换回来必力，点击详情发现LeanCloud国际版可以用，做个记录。
<!--more-->

## 1. [中国版](leancloud.cn)导出数据
![image.png](https://i.loli.net/2020/03/14/myc683VrqeSNIXv.png)
亲测凌晨零点无法导出数据，今天上午九点成功导出。
**[限定导出数据起止日期]**可选可不选，不选择默认导出所有数据。
导出的数据压缩包解压后如下：
<img src="https://i.loli.net/2020/03/14/OXzMiCyA7H5DL6E.png" width="350">

## 2. [国际版](leancloud.app)导入数据
<img src="https://i.loli.net/2020/03/14/9a4r3PVZzF8eGLK.png" width="350">

进入数据存储页面，选择数据导入

<img src="https://i.loli.net/2020/03/14/aORKH8utd7ikLCe.png" width="500">

valine评论系统实际上只使用了两个Class——Comment和_User，选择之前解压出的JSON文件，导入即可。

## 3. 修改AppId AppKey
在Next主题文件夹下的配置文件`_config.yml`更新Valine的AppId和AppKey为国际版中的值即可。
