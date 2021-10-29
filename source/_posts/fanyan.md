---
title: 「学习笔记」 二项式反演
date: 2021-10-19 15:00:16
tag: 学习笔记
category: 学习笔记
---

由于大家还没停课所以我很幸运的获得了每一道题的首A。

![](/image/20211028.png)

## 基本形式

$g_k$ 表示恰好有 $k$ 个满足条件 $S$。

### 形式一：“至少形式”

$f_k$ 表示至少有 $k$ 个满足条件 $S$。

说是至少其实是因为很多人这么称呼（周神讲课的时候也这么说）。实际上不应当把 $f_k$ 理解为“至少 $k$ 个满足条件 $S$ ”，**而应该理解为“钦定 $k$ 个满足条件 $S$ ，剩下的放任自流”。**

$$f(k) = \sum_{i=k}^{n}{ \binom{i}{k} {g(i)} } \iff g(k) = \sum_{i=k}^{n} (-1)^{i-k} \binom{i}{k} {f(i)} $$

### 形式二：“至多形式”

$f_k$ 表示至多有 $k$ 个满足条件 $S$。

同样的这并不应当理解成“至多”。

$$f(k) = \sum_{i=m}^{k}{ \binom{k}{i} {g(i)} } \iff g(k) = \sum_{i=m}^{k} (-1)^{n-i} \binom{k}{i} {f(i)} $$

> “至少”形比“至多”形在算法竞赛中更为常用。

上面两个形式证明只需代入。

## 例题

> 类型1：套式子

### [[BZOJ2839]集合计数](https://hydro.ac/d/bzoj/p/2839)

*AC on 2021.10.28 [CODE](/post/code/#BZOJ2839])*

$$\binom{n}{k} (2^{2^{n-k}}-1) = f(k) = \sum_{i=k}^{n} \binom{i}{k}{g(i)}$$

然后反演就好了。适合作为新手第一题。

### [King's Colors](https://codeforces.com/gym/101933/problem/K)

*AC on 2021.10.28 [CODE](/post/code/#gym101933K)*

$n$ 个点的树填 $k$ 种不同的颜色，要求没有相邻两点颜色相同。

$$k \cdot (k-1)^{n-1} = f(k) = \sum_{i=1}^{k} \binom{k}{i} g(i)$$

### [BZOJ4710 分特产](https://hydro.ac/d/bzoj/p/4710)

*AC on 2021.10.28 [CODE](/post/code/#BZOJ4710)*

$$\binom{n}{k} \prod_{i=1}^{m} \binom{a[i]+n-k-1}{n-k-1} = f(k) = \sum_{i=k}{n} \binom{i}{k} g(i)$$

> 类型2：求补集

### [BZOJ4487 染色问题](https://hydro.ac/d/bzoj/p/4487)

*AC on 2021.10.28 [CODE](/post/code/#BZOJ4487)*

$n \times m$ 的矩形，填 $c$ 种不同的颜色，要求每行每列都有颜色。

$f(i,j,k)$ 表示钦定 $i$ 行 $j$ 列一个都没染且钦定 $k$ 种颜色未使用。（即**至少形式**）

$g(i,j,k)$ 表示恰好 $i$ 行 $j$ 列一个都没染且恰好 $k$ 种颜色未使用。

$$f(x,y,z) = \binom{n}{x} \binom{m}{y} \binom{c}{z} (c-z+1)^{(n-x)(m-y)}$$

$$f(x,y,z) = \sum_{i=x}^{n} \sum_{j=y}^{m} \sum_{k=z}^{c} \binom{i}{x} \binom{j}{y} \binom{k}{z} g(i,j,k)$$

一个优化复杂度的小技巧，$O(nm)$ 处理出 $(c-z+1)$ 的 $1$ 到 $nm$ 次方。

### [CF1228E Another Filling the Grid](https://codeforces.com/problemset/problem/1228/E)

*AC on 2021.10.28 [CODE](/post/code/#CF1228E)*

$n \times n$ 的方格纸，$k$ 种数字，要求每行、每列最小值均为 $1$。

$f(i,j)$ 表示钦定有 $i$ 行、$j$ 列不满足要求的方案数。（即**至少形式**）

$g(i,j)$ 表示恰好有 $i$ 行、$j$ 列不满足要求的方案数。

$$f(x,y) = \binom{n}{x} \binom{n}{y} (k-1)^{n^2 - (n-x)(n-y)} k^{(n-x)(n-y)}$$

$$f(x,y) = \sum_{i=x}^{n} \sum_{j=y}^{n} \binom{i}{x} \binom{j}{y} g(i,j)$$

### [CF997C Sky Full of Stars](https://codeforces.com/problemset/problem/997/C)

*AC on 2021.10.28 [CODE](/post/code/#CF997C)*