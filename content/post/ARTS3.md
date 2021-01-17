---
title: "ARTS 3"
date: 2021-01-11T00:19:11+08:00
draft: false
tags:
- ARTS
categories: 
- 周报打卡
---

第三周

最近好冷

//

周三开始暖起来啦～

<!--more-->

> A: Algorithm，每周至少做一道 Leetcode
>
> R: Review，阅读并点评至少一篇英文文章
>
> T: Tips，学习至少一个技术技巧
>
> S: Share，分享一篇有观点和思考的技术文章

<p align="right">2021/01/11 - 2021/01/17</p>

## Algorithm

- [LeetCode 19. 删除链表的倒数第N个节点](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/link/leetcode-19)

  - 快慢指针
- [LeetCode 62. 不同路径](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/dp/leetcode-62)
  - 动态规划
- [LeetCode 75. 颜色分类](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/array/leetcode-75)
  - 双指针
- [LeetCode 560. 和为K的子数组](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/hashmap/leetcode-560)
  - 哈希表，前缀和
- [LeetCode 494. 目标和](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/dp/leetcode-494)
  - 动态规划，DFS
- [LeetCode 617. 合并二叉树](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/binarytree/leetcode-617)
  - DFS
- [LeetCode 461. 汉明距离](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/bit/leetcode-461)
  - 位运算
- [LeetCode 448. 找到所有数组中消失的数字](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/array/leetcode-448)
  - 数组，哈希表
- [LeetCode 94. 二叉树的中序遍历](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/binarytree/leetcode-94)
  - 递归，栈
- [LeetCode 46. 全排列](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/backtrack/leetcode-46.-quan-pai-lie)
  - 回溯，题解里为了节省空间把 visited 扔掉了，我还是更喜欢有 visited 数组的解法，比较清晰直观。
- [LeetCode 165. 比较版本号](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/string/leetcode-165)
  - 字符串分割，双指针（双指针解法的还没看）
- [LeetCode 24. 反转链表](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/link/lcof-24)
  - 基础链表题
- [LeetCode 543. 二叉树的直径](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/binarytree/leetcode-543)
  - 典型 DFS
- [LeetCode 112. 路径总和](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/binarytree/leetcode-112)
  - 递归简单，BFS的话利用队列完成即可。
- [LCOF 58-I. 翻转单词顺序](https://hishark777.gitbook.io/777-interview-notes/algorithm/lcof/lcof-58-1)
  - 字符串，双指针

## Review

[Impressive Source Codes That Every Developer Should See](https://medium.com/swlh/impressive-sources-codes-that-every-developer-should-see-b68028b36da5)

> Past developers have done great work to give a peaceful world for modern developers.

## Tips

AS 里  `Download gradle` 半天下不下来就打开 `gradle-wrapper.properties` ：

```properties
#Sun Mar 15 19:17:15 CST 2020
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
#distributionUrl=https\://services.gradle.org/distributions/gradle-5.4.1-all.zip
distributionUrl=gradle-5.4.1-all.zip
```

访问 `distributionUrl` 下的地址 `https://services.gradle.org/distributions/gradle-5.4.1-all.zip` 把 zip 包下载下来放到 `/gradle/wrapper`  下，然后修改 `distributionUrl` 的值即可。

## Share

[Git各指令的本质，真是通俗易懂啊](https://juejin.cn/post/6895246702614806542)

- 不管是`HEAD`还是`分支`，它们都只是`引用`而已，`引用`+`节点`是 Git 构成分布式的关键
- `merge`相比于`rebase`有更明确的时间历史，而`rebase`会使提交更加线性应当优先使用
- 通过移动`HEAD`可以查看每个提交对应的代码
- `clone`或`fetch`都会将远程仓库的所有`提交`、`引用`保存在本地一份
- `pull`的本质其实就是`fetch`+`merge`，也可以加入`--rebase`通过rebase方式合并

## 本周时间轴

