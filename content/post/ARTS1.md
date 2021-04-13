---
title: "ARTS 1"
date: 2020-12-28T09:29:49+08:00
draft: false
tags:
- ARTS
categories: 
- 周报打卡
description: 2020 年的最后一周，不如就来开启第一个 ARTS 吧。
---

> A: Algorithm，每周至少做一道 Leetcode
>
> R: Review，阅读并点评至少一篇英文文章
>
> T: Tips，学习至少一个技术技巧
>
> S: Share，分享一篇有观点和思考的技术文章

<p align="right">2020/12/28 - 2021/1/3</p>

## Algorithm

这周做了几个算法题

[LeetCode 122. 买卖股票的最佳时机 II](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/greedy/leetcode-122)

因为交易次数不受限，如果可以把所有的上坡全部收集到，一定是利益最大化的。——[seven](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/solution/mai-mai-gu-piao-de-zui-jia-shi-ji-ii-by-leetcode-s/658886)

[LeetCode 316. 去除重复字母](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/greedy/leetcode-316)

这个有点难想嗷

[LeetCode 605. 种花问题](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/greedy/leetcode-605)

这个判断条件官方题解写太好了

[LeetCode 860. 柠檬水找零](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/greedy/leetcode-860)

核心是模拟

[LeetCode 239. 滑动窗口最大值](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/slidewindow/leetcode-239)

如题

[LeetCode 86. 分隔链表](https://hishark777.gitbook.io/777-interview-notes/algorithm/tag/pointer/leetcode-86)

双指针

## Review

Medium 上的优质文章有很多，找了一篇对比 MVC、MVP、MVVM 的文章看看：[MVC vs MVP vs MVVM](https://levelup.gitconnected.com/mvc-vs-mvp-vs-mvvm-35e0d4b933b4)

不过类似的 MVX 的总结其实看过不少了

文末提到三者最主要的区别：

**Performance Evaluation** — When we are testing the UI performance, MVP turns out to be the one with the highest reliability and lowest hindrance when it comes to rendering frames. Data binding in MVVM creates an additional overload that could drastically affect its performance when performing complex tasks.

**Compatibility** — When testing the patterns based on their compatibility, MVVM was the best of the lot due to its data binding which had a positive impact. MVP fared better than MVC, which had serious restating issues.

**Modifiability** — When we talk about design patterns, it is evident that it should be modifiable since that gives us the option of adding new features and strategies into our app.

- Based on these factors, we observed that changes are very less in MVP and MVVM, with MVVM contributing a lot towards maintainability.
- MVC tends to increase the number of changes in the majority of the cases.

**References** — In MVC, the View doesn’t have reference to the Controller while in MVP, the View has reference to the presenter and in MVVM, the View has reference to the View-Model.

**Entry Point** — For MVC, the entry point to the application is the Controller whereas, for MVP and MVVM, the entry point is the View.

## Tips

一直看人使用 Markdown 的脚注

自己还没用过，来学一下

使用方法很简单：

- 在正文中想要添加脚注的地方加上 `[^1]`
- 在文章末尾加上 `[^1]: Hello Footnote`

然后就可以愉快地使用脚注啦[^1]

## Share

[要想读懂HashMap的源码，你得这样看](https://mp.weixin.qq.com/s/WDEnG3KroN5D0xbQxe-WBg)

- HashMap 允许空键和空值。
- 最多允许一条记录的键为空，允许多条记录的值为空。
- HashMap 为基本操作（get 和 put）提供了恒定时间的性能。
- HashMap 实例有两个影响其性能的参数：初始容量（initial capacity）和负荷系数（load factor）。通常，默认的负荷系数（0.75）在时间和空间成本之间提供了一个很好的权衡，在大部分下情况下，不建议修改该值。如果设为较高的值，可以减少空间开销，但是会增加查找成本。
- HashMap 是线程不安全的，可以使用 Collections 的 synchronizedMap 来使 HashMap 具备线程安全的能力，或者使用 ConcurrentHashMap。
- 有个很重要的字段table数组，类型是Node<K,V>[]，也就是哈希桶数组，table 数组的初始长度是 16，负荷系数（load factor）默认值是0.75f，threshold 是 HashMap 所能容纳的最大数据量的节点（Node）个数，有如下公式：`threshold = loadFactor * length`，loadFactor是负荷系数，length 是数组长度，也就是数组在定义好长度后，负荷系数越大，所能容量的节点就越多，前面也提到了，当节点个数超过这个数值时，HashMap 就会扩容，扩容后的容量是原来的两倍。
- HashMap 使用哈希表存储数据。哈希表可以使用四种方式来解决哈希冲突。
- HashMap 是使用链地址法来解决哈希冲突的。
- Map 是一个接口，它是将键映射到值的对象，映射不能包含重复的键，每个键最多可以映射一个值，常见的 Map 实现类有 HashMap、ConcurrentHashMap、Hashtable、LinkedHashMap 和 TreeMap 等。
- ConcurrentHashMap 是线程安全的 HashMap，JDK1.8 之前使用分段锁，JDK1.8 之后抛弃了分段锁，利用内置锁 synchronized 和 CAS 来保证线程安全。
- Hashtable 是线程安全的，但是并发性不如 ConcurrentHashMap，不建议使用。
- LinkedHashMap 通过维护一个双向链表来保证迭代顺序，可以实现 LRU 算法。
- TreeMap 基于红黑树。
- 解决哈希冲突的四种方法：开放地址法、链地址法、再哈希法、建立公共溢出区。

[用烂的LruCache，你真的完全懂了么？](https://mp.weixin.qq.com/s/5hK2JFghfh4JTnxrqBurHg)

> 看到这篇想起了三年前写的一篇博客：
>
> 当时用 ListView 的时候一滑动就崩溃 搞得糊里糊涂的
>
> 后面一查才知道是加载图片导致的 OOM
>
> 使用 LruCache 来缓存图片就可以避免 OOM 的发生

Glide 的内存缓存就是通过 LruCache 实现的，LruCache 内部持有的是 LinkedHashMap。

[^1]: Hello Footnote

