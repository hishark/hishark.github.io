---
title: 又一年末
date: 2019-12-01 22:54:01
tags:
- TechDiary
categories: 技术日记
excerpt: 这里是777的十二月份bb日记
authors: 
- hishark777
---
2019拜拜

2020加油啦
<!--more-->

# 2019-12-23
医疗项目开会听到的

[DICOM baidu](https://baike.baidu.com/item/DICOM)

[DICOM wiki](https://zh.wikipedia.org/wiki/DICOM)

# 2019-12-21
## **Roadmap**

嗨呀下周一要对需求
然而我安卓差不多忘光了OTZ

[Android developer Roadmap for 2019](https://android.jlelse.eu/android-developer-roadmap-for-2019-14eacb0d0a2)

Improving yourself as an Android developer

- Understand the Activity Lifecycle to push a bug free application
- Leverage dynamic and flexible and dynamic UI designs using Fragments
- Learn how to debug your Android app — use Android Studio debugger
- Master Android activities to build screens that you want a user to navigate through
- Gain an understanding of context in Android
- Learn REST and HTTP — Most pro devs are extremely good at understanding all aspects of REST and HTTP
- Learn how to take advantage of multithreading
- Be an expert at handling configuration changes
- Learn Database and SQL
- Content providers
- Learn about the top Android 3rd party libraries — The most [helpful and used ones are](https://android.jlelse.eu/7-third-party-dependencies-every-android-developer-should-know-a751f009ff58): OkHttp, GSON, Retrofit, Glide, Butter Knife, Crashlytics, Guava

# 2019-12-19
## **Android**

才多久没关注就10了

[Android 10 for Developers](https://developer.android.com/about/versions/10/highlights)

Android10主要关注点——隐私权&安全性

- 可折叠设备 //正好刚看完[何同学的视频](https://www.bilibili.com/video/av79091085)，感觉好鸡肋哦。
- 5G //该来的还是要来的
- 通知中的智能回复
- 深色主题 //👍
- 手势导航 //看动图和iphone一样奥
- 设置面板
- 共享快捷方式
- 照片的动态深度 // 看不懂了
- 捕获播放的音频 //wow这个ios肯定干不了
- 新的音频和视频编解码器
- 可缩放的定向麦克风
- Vulkan //查了一下是一个跨平台的2D和3D绘图应用程序接口
- 通过公共API实现兼容性
- ...

其实我觉得android最繁杂的一点就是适配，实习的时候看到组里一个输入法的适配都很折腾人-。-

## **杂**

不要把自己局限在一个框里

# 2019-12-18
## **Programming language**

有点意思奥
太酷了点吧回寝室用电脑试试

[wenyan-lang](https://github.com/LingDong-/wenyan-lang)

# 2019-12-16
## **Javascript**

[4 Ways to Populate an Array in JavaScript](https://medium.com/@wisecobbler/4-ways-to-populate-an-array-in-javascript-836952aea79f)

# 2019-12-15
## **VS Code Theme**

发现了一组喜欢的主题[Noctis](https://marketplace.visualstudio.com/items?itemName=liviuschera.noctis)，看着巨舒服！！

> Noctis is a collection of light & dark themes with a well balanced blend of warm and cold medium contrast colors.

## **Font**

[Cartograph Mono CF](https://connary.com/cartograph.html)

喜欢这个字体，网站也很好看，搞完报告再来瞅瞅

# 2019-12-14
## **JS - forEach**

[3 things you didn’t know about the forEach loop in JS](https://medium.com/front-end-weekly/3-things-you-didnt-know-about-the-foreach-loop-in-js-ff02cec465b1)

- There is no way to stop or break a forEach() loop other than by throwing an exception
- ‘return’ doesn’t stop looping
- You cannot ‘break’
- You cannot ‘continue’

## **Slides**

发现一个好用的ppt模版网站[slidesgo](https://slidesgo.com/)

# 2019-12-13
## **Debug**

[How to stop using console.log() and start using your browser’s debugger](https://medium.com/datadriveninvestor/stopping-using-console-log-and-start-using-your-browsers-debugger-62bc893d93ff)

console.log(‘Total Price:’, total) //In an effort to see if the value was stored
console.log(‘Here’) //If my program execution reached a certain function

乐死我了这不就是我吗哈哈哈哈哈哈，但是有时候console.log还是很方便奥。

从评论get了不少

- [debugger](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/debugger) 下次试试这个
- [another tip](https://medium.com/@martinczerwi/just-another-tip-i-found-highly-valuable-cf38f1077207)
- Vue Chrome Devtools + console.log

看到一个[write tests>debug](https://medium.com/@michael_volz/i-personally-think-that-debugging-is-a-sign-of-bad-code-2e2b93181008)的评论，也有点道理。

# 2019-12-12
## **Javascript**

[Why ['1', '7', '11'].map(parseInt) returns [1, NaN, 3] in Javascript](https://medium.com/dailyjs/parseint-mystery-7c4368ef7b21)

- [Array map()](https://www.runoob.com/jsref/jsref-map.html)
- [parseInt()](https://www.runoob.com/jsref/jsref-parseint.html)
- All values are truthy except for: false, 0, ""(empty string), null, undefined, NaN. Which means the string "false", the string "0", an empty object {}, and and an empty array [] are all truthy.

> ['1', '7', '11'].map(parseInt) doesn’t work as intended because map passes three arguments into parseInt() on each iteration. The second argument index is passed into parseInt as a radix parameter. So, each string in the array is parsed using a different radix. '7' is parsed as radix 1, which is NaN, '11' is parsed as radix 2, which is 3. '1' is parsed as the default radix 10, because its index 0 is falsy.

文中有句`fire up your console`好可爱哈哈哈哈

## **Algorithm**

[LeetCode-226](https://leetcode-cn.com/problems/invert-binary-tree/)题的备注里看到了有意思的东西

Homebrew的作者Max Howell去谷歌面试，没写出翻转二叉树，Google：我们90％的工程师使用您编写的软件(Homebrew)，但是您却无法在面试时在白板上写出翻转二叉树这道题，这太糟糕了。

# 2019-12-11
## **cool site**

好久没有看anyway邮报，今天整理邮箱看到了两个有意思的网站。

- [Bruno Simon](https://bruno-simon.com/) 点开就可以开一辆小车瞎撞啦！[戳这里](https://medium.com/@bruno_simon/bruno-simon-portfolio-case-study-960402cc259b)瞅瞅作者的设计、开发过程。
- [Alex Pierce](https://thegeekdesigner.com/) 像素风格的个人网站

# 2019-12-10
## **杂**

"An algorithm is a finite, definite, effective procedure, with some input and some output."

"Algorithms are the life-blood of computer science... the common denominator that underlies and unifies the different branches."

--Donald Knuth

# 2019-12-09
## **CSS SANS**

CSS SANS is the font created by CSS, the programming language for web designing and typesetting.

It is an unprecedented font that reflects history and evolution of the Web, and even changes its own shape.

[https://yusugomori.com/projects/css-sans/](https://yusugomori.com/projects/css-sans/)

有点意思

## **ICON**

[How to use Font Awesome 5 on VueJS Project](https://medium.com/front-end-weekly/how-to-use-fon-awesome-5-on-vuejs-project-ff0f28310821)

[fontawesome](https://fontawesome.com/) 怎么翻了墙都打开巨慢- - 实验室今天网好像很垃圾

## **杂**

看到[这位哥](https://github.com/ittus)的简介是bugs producer哈哈哈乐了
我是shit producer!

# 2019-12-08
## **GitHut**

[GitHut](https://githut.info/) A SMALL PLACE TO DISCOVER LANGUAGES IN GITHUB

这个网站是在[@joyeecheung](https://joyeecheung.github.io/diary)里看到的，有点意思，没想到第一居然是javascript，牛批👍

## **Gulp**

先是在joyee的[这篇blog](https://www.cnblogs.com/joyeecheung/p/4555802.html)里看到了gulp，然后去查了一下是个什么东西：[gulp](https://www.gulpjs.com.cn/)将开发流程中让人痛苦或耗时的任务自动化，从而减少你所浪费的时间、创造更大价值。

主页有一句——"Builds can be the most awful sinkhole for teams to waste their time with - gulp is a serious win for any project."
好的下次试试

## **FrontEnd**

[Front-end Developer Handbook 2019](https://frontendmasters.com/books/front-end-handbook/2019/)

[Frontend Weekly](https://medium.com/front-end-weekly)

[Learn to become a modern Frontend Developer in 2019](https://medium.com/@kamranahmedse/modern-frontend-developer-in-2018-4c2072fa2b9c)

## **Redis**

突然发现Card-Campus里有个[去年的issue](https://github.com/hishark/Card-Campus/issues/1)没注意，这位朋友提到了redis于是查了一下。

[Redis简介](https://www.runoob.com/redis/redis-intro.html)