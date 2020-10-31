---
title: AS - Github踩坑
date: 2018-03-18 20:14:40
tags: 
- git
categories: 学习笔记
thumbnail: 
---
踩了一点坑记一下
<!--more-->
##### Q1
报错
>Can't finish GitHub sharing process
Successfully created project 'CHICHU' on GitHub, but initial push failed:
unable to access 'https://github.com/hishark/CHICHU.git/': error setting certificate verify locations:

这个错误是系统证书的问题，系统判断到这个行为会造成不良影响，所以进行了阻止，只要设置跳过SSL证书验证就可以了，用以下命令即可。
>$ git config --global http.sslVerify false

##### Q2
报错
>remote with selected name already exists

<center>![](https://ws1.sinaimg.cn/large/0068SXX6gy1fph90hmbn4j30b107hjrh.jpg)
*网上找的别人的图 出问题的时候忘记截图了*</center>
因为之前第一次创建仓库时出现了Q1的问题，导致remote name已经用过了一次github，所以才会报错。

**解决方法**
去项目根目录下右键git bash here，然后输入以下命令即可。
>$ git remote rm github
