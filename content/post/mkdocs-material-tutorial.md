---
title: Mkdocs-Material Tutorial
date: 2020-09-07 20:06:19
tags: 
- markdown
categories: 
- 学习笔记
hide: false
authors: 
- hishark777
---
总喜欢折腾一些没什么用的东西，我又开始了。年初给自己整了个[Gitbook](https://hishark777.com/777-Tech-Diary/)放~~技术日记~~乱七八糟的碎碎念，最后迁移到了[博客](http://localhost:4000/categories/%E6%8A%80%E6%9C%AF%E6%97%A5%E8%AE%B0/)。前阵子看到有人用[Mkdocs-Material](https://squidfunk.github.io/mkdocs-material/)写博客，转了一圈官网觉得有点意思，~~也比Gitbook更好看~~（比以前的Gitbook好看），于是来整一个做校招笔记。



## 1. 安装
输入以下命令：
```
pip install mkdocs-material
```
## 2. 创建站点
在Github上创建一个仓库，比如我的：[Android-Interview](https://github.com/hishark/Android-Interview/tree/master)，拉到本地之后在根目录下输入以下命令：
```shell
mkdocs new .
```

输入这个命令之后会生成如下的目录结构
```
.
├─ docs/
│  └─ index.md
└─ mkdocs.yml
```

## 3. 配置
打开`mkdocs.yml`，添加主题：
```
site_name: Android Interview
theme:
  name: material
```

添加扩展：
```
markdown_extensions:
  - admonition
  - codehilite:
      guess_lang: false
      linenums: false
  - toc:
      permalink: true
  - footnotes
  - meta
  - def_list
  - pymdownx.arithmatex
  - pymdownx.betterem:
      smart_enable: all
  - pymdownx.caret
  - pymdownx.critic
  - pymdownx.details
  - pymdownx.emoji:
      emoji_generator: !!python/name:pymdownx.emoji.to_png
  - pymdownx.inlinehilite
  - pymdownx.magiclink
  - pymdownx.mark
  - pymdownx.smartsymbols
  - pymdownx.superfences
  - pymdownx.tasklist
  - pymdownx.tilde
```

其他配置可以在这里看到：[Advanced configuration](https://squidfunk.github.io/mkdocs-material/creating-your-site/#advanced-configuration)

## 4. 预览
输入以下命令：
```shell
mkdocs serve
```

于是你就得到了一个乖巧的静态网站，在`docs/`目录下创建markdown文件就可以愉快的瞎写了。

## 5. 部署
在包含`mkdocs.yml`文件的路径下输入以下命令：
```shell
mkdocs gh-deploy --force
```

就可以在`https://yourname.github.io/repo_name`下看到生成的Mkdocs啦~其中`yourname`是Github的用户名，`repo_name`就是第二步中创建的仓库名称。

[校招笔记](https://hishark777.com/Android-Interview/)启动！

## 6. 搬回Gitbook
偶然发现Gitbook现在非常好！看！了！
于是我又搬回去了：
- [Gitbook-Android-Interview](https://hishark777.gitbook.io/android-interview/)

## 参考
- [https://squidfunk.github.io/mkdocs-material/](https://squidfunk.github.io/mkdocs-material/)