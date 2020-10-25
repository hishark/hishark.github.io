---
title: MacOS Python2.7->3.7
date: 2019-09-28 15:08:48
tags: 
- MacOS
categories: 学习笔记
hide: true
---
>已经有两位朋友来跟我说用homebrew了，dbq我真的智障🤦🏻‍♀️
brew install python3就好啦！

以防万一还是没动系统自带的2.7

1. 官网下3.7.4
    https://www.python.org/downloads/

2. open ~/.bash_profile加几行代码
    ```bash
    export PATH=$PATH:/Library/Frameworks/Python.framework/Versions/3.7/bin:
    alias python="/Library/Frameworks/Python.framework/Versions/3.7/bin/python3.7"
    alias python2='/usr/bin/python2.7'
    ```

3. pip也记得在bash_profile里加一下
    ```bash
    alias pip='/Library/Frameworks/Python.framework/Versions/3.7/bin/pip3.7'
    ```

4. source ~/.bash_profile
<!--more-->

