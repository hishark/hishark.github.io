---
title: "Hugo 安装指定版本"
date: 2020-10-27T15:00:32+08:00
categories: 
- 学习笔记
tags:
- hugo
draft: false
authors:
- hishark777
description: 从 Hexo 搬到 Hugo 啦。
---

前些天逛博客看到 [Hugo](https://gohugo.io/) 觉得不错，然后就去官网逛了逛，看到了一个喜欢的主题 [Eureka](https://github.com/wangchucheng/hugo-eureka)，且 Hugo 的构建时间秒杀 Hexo 也是个亮点，于是琢磨着转移一下博客，Hugo 搭建起来挺快的，但是遇到了一点版本升级与降级的小问题，记录一下。

<!--more-->

## 1. 起因

> 我真是浪费了无数时间在折腾博客上- - 不过真好玩哈哈

电脑系统为 MacOS，直接执行了 `brew install hugo` 安装了 Hugo，装完之后按照 [Eureka 的文档](https://www.wangchucheng.com/zh/docs/) 一步步来配置，最后快乐的执行  `hugo server` 收到了一大串报错，现场未保留，总之是对主题中的一些文件进行了报错。

接着回头思考是哪一步出了错，发现在[前提](https://www.wangchucheng.com/zh/docs/eureka/getting-started/#%E5%89%8D%E6%8F%90)中提到了 Eureka 需要安装 v0.74.0 的 Hugo，瞅了瞅 Hugo 官方[最新发布的版本](https://github.com/gohugoio/hugo/releases/tag/v0.76.5)是 v0.76.5，错以为自己电脑上的版本就是 v0.76.5，然后开始 Google 要如何对 Hugo 进行降级。

## 2. 经过

经过 Google 找到了一篇靠谱的教程来安装旧版本的 Hugo：

[Homebrew 安装旧版本软件 - 狂飙](https://networm.me/2019/10/27/installing-old-homebrew-formulas/)

<!-- 这里闲下来也写一下详细的步骤 -->

之前这个方法应该是管用的，毕竟评论区中前排的评论都在感谢作者哈哈，但是现在按照这个流程来做会出现报错：

```txt
Error: Calling Non-checksummed download of hugo formula file 
from an arbitrary URL is disabled! Use 'brew extract' 
or 'brew create' and 'brew tap-new' to create a formula file 
in a tap on GitHub instead.
```

这个时候，我起身去了一趟洗手间 🚻 ，回来随手在终端敲下了一句 `hugo version`，然后发现自己电脑上 Hugo 的版本实际上是 v0.73.0。

行。

所以我应该升级而不是降级。

## 3. 究极解决方案

想升级很简单，直接执行 `brew upgrade hugo` 就好啦，会自动给你的电脑安装 hugo 的最新稳定版本。但是问题又来了，目前通过 brew 成功安装到的 Hugo 版本为 v0.73.0，比我需要的 v0.74.0更低，所以我执行该条指令并没有任何帮助。

最后，我需要解决的问题应该是——如何安装指定版本的 Hugo。很简单，根据 [How to install a specific version of gohugo ](https://discourse.gohugo.io/t/how-to-install-a-specific-version-of-gohugo/23542)这个问题中的第二个评论找到了解决方案：

1. 去 Hugo-Github 的 [Releases](https://github.com/gohugoio/hugo/releases) 页面找到你需要的指定版本

2. 根据电脑系统定位到对应的压缩包进行下载（我的电脑系统为 MacOS 所以选择的是 [hugo_0.74.0_macOS-64bit.tar.gz](https://github.com/gohugoio/hugo/releases/download/v0.74.0/hugo_0.74.0_macOS-64bit.tar.gz)）

3. 解压该压缩包，用其中名为 `hugo` 的可执行文件去替换当前电脑中已有的 `hugo` 可执行文件，MacOS 下 hugo 所在的路径为 `/usr/local/bin`。

替换后就成功装上想要的版本啦～

## 4. 注意

另外有个要注意的小问题是 MacOS 使用 homebrew 安装的话默认会安装 extended 版本。发现这个问题是还看上了另外一款主题 [MemE](https://github.com/reuixiy/hugo-theme-meme)，这款主题要求安装 extended 版本的 Hugo，而我在 [Install-Hugo](https://gohugo.io/getting-started/installing/) 中也没有查找到 MacOS 中要如何安装 extended 版本，最后在 Hugo 的 Github 库中看到了一个 [issue](https://github.com/gohugoio/hugoDocs/issues/823)，里面提到：

> An extended is default on macOS with `brew install hugo`

所以 MacOS 中使用 homebrew 安装 Hugo 的话是默认安装 extended 版本的。

## 参考

- [How to install a specific version of gohugo ](https://discourse.gohugo.io/t/how-to-install-a-specific-version-of-gohugo/23542)
- [Homebrew 安装旧版本软件 - 狂飙](https://networm.me/2019/10/27/installing-old-homebrew-formulas/)