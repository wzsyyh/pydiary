---
title: 集训队作业做题记录
date: 2021-10-19 15:00:16
tag: 学习笔记
category: 学习笔记
---

> ljc1301 跟 Owen_codeisking 都有推荐做集训队作业，于是决定挑战一下自己。

## IOI2020国家集训队作业

### [CF504E Misha and LCP on Tree](https://codeforces.com/problemset/problem/504/E)

*AC on 2021.10.19 [CODE](/post/code/#CF504E)*

看道题就想到树链剖分，结合一下哈希，联系一下二分。好像也是我第一次写双模数哈希（因为Codeforces卡`unsigned`来着）。

于是得到了：

![](/image/CF504E.png)

~~就这？~~ 就这样我创建了这个页面。

### [CF547D Mike and Fish](https://codeforces.com/problemset/problem/547/D)

*AC on 2021.10.20 [CODE](/post/code/#CF547D)*

昨天ZROI模拟赛刚做了一道给边染色的题，而这题不过是改成了给点染色，今天ZROI模拟赛刚做了一道巧妙转换成二分图染色的题。那么这题完完全全就像是那两道题综合一下的题，难度并没有很大，不过可惜的是还是没有自己独立思考出来。

对于每一个横/纵坐标上的点，每两个一组连边，之后跑二分图染色。同一组的两个点颜色不同，保证了同一行/列两种颜色之差不超过 $1$，每个点最多连 $2$ 条边，故要么是链要么是 $4$ 个点的环（不是奇环）。