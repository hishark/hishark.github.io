---
title: 借助Gitbook搭建一个技术日记簿
date: 2020-02-15 13:24:17
tags:
categories: 学习笔记
authors:
- hishark777
---
整了个Gitbook挂到博客下面 
来写技术日记

去年十二月偶然发现了[joyee的tech-diary](https://www.github.com/joyeecheung/diary)
觉得挺有意思于是依葫芦画瓢也给自己整了个[777-Tech-Diary](https://www.hishark777.com/diary/)
用了大概一个月发现了一些小问题：
1. 查看某日日记时无法直接查看前一日和后一日的内容
2. 日历小bug有点多

第一点是joyee的TODO，但是她好像已经没有维护了，我又是个大懒鬼所以打算另找出路。

找了一圈都没有找到满意的工具，本月初突然想起Gitbook好像很符合我的需求，于是开始动手。
<!--more-->
## 1. 安装Gitbook
跟着[Gitbook入门](https://www.jianshu.com/p/dc53e589897a)把Gitbook装好了在本地跑了起来，安装过程中遇到个[小错误](https://blog.csdn.net/w5688414/article/details/94172354)，重装node解决了。

## 2. 部署到Github
再参照[用gitbook做笔记如何部署到github](https://www.jianshu.com/p/4e109a1113b2)成功把gitbook挂到博客域名下。

## 3. Gitbook更新步骤
上面两步全部做好之后，以后只需要四条指令即可更新日记。
```
1. npm run build
2. git add .
3. git commit -m "update"
4. git push
```

### 4. Done
最后我就拥有了一个写技术日记和瞎bb的小旮旯——[777 Tech Diary](https://hishark777.com/777-Tech-Diary/)。
耶✌️