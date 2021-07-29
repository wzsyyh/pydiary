---
title: 「游记」2021ZROISC
date: 2021-07-16 16:01:28
tag: 游记
category: 游记
---

## Day 0

2021.07.16 中午到了金华。

中午川菜辣死了，下午麦当劳冰淇淋有亿点小。

## Day 1

刚AK IOI2021的dls在隔壁桌吃早餐。

现在我们楼下都是NOI赛前集训的神佬们，有dls、lk……

再想想自己生在浙江，不禁流下了眼泪。

南外的吕秋实吕老师！

讲的大部分东西都很熟，只有欧拉序+RMQ求LCA之前没有写过，写了以后发现虽然是 $O(1)$ 询问，但板子题比树剖还是要慢。

例题列表

T1 https://atcoder.jp/contests/abc070/tasks/abc070_d ✔️

T2 树上路径不带修最小值 ✔️

T3 https://codeforces.ml/contest/609/problem/E ✔️

T4 https://acm.hdu.edu.cn/showproblem.php?pid=3183 ✔️

T5 http://poj.org/problem?id=3419 ✔️

T6 https://codeforces.ml/contest/1301/problem/E ✔️

T7 https://codeforces.ml/problemset/problem/1527/D ✖️

T8 https://www.luogu.com.cn/problem/UVA1707 

## Day 2

讲线段树和树状数组的时候感觉还是很水，然后：“现在我们已经学会线段树了，快来看一下这道题吧。”于是暴毙了。
今天的题还是蛮难的吧。

T1 求给定序列冒泡排序需要交换多少次（求逆序对） ✔️

T2 https://www.luogu.com.cn/problem/P4868  ✔️

T3 http://poj.org/problem?id=2155 ✔️

T4 https://codeforces.ml/contest/1527/problem/E ✖️

T5 从区间拓展到树上http://poj.org/problem?id=3728 ✔️

T6 http://acm.hdu.edu.cn/showproblem.php?pid=6315 ✔️ [笔记](/post/hdu6315)

T7 http://acm.hdu.edu.cn/showproblem.php?pid=5634

T8 https://codeforces.com/contest/1149/problem/C

## Day 3

第一场模拟赛，太惨烈了不想记录

T1的`freopen`忘记去掉了，抱灵了

T2开始题意理解错了，写了个 Kruskal ，只得了10分。看数据范围应该想到状压。

T3可以转化为求每个点开头的最长上升子序列、最长下降子序列，还要求计数。

用树状数组计数较为方便：

```cpp
inline void add(int x,int d,int num){
    while(x<=n+1){
        if(c1[x]<d) c1[x]=d,c2[x]=num;
        else if(c1[x]==d) (c2[x]+=num)%=mod;
        x+=x&-x;
    }
}

pi sum(int x){
    pi res=make_pair(0,0);
    while(x>0){
        if(c1[x]>res.first){
            res.first=c1[x];
            res.second=c2[x];
        }
        else if(c1[x]==res.first) (res.second+=c2[x])%=mod;
        x-=x&-x;
    }
    return res;
}
```

## Day 4

https://vjudge.net/contest/447983:

T1 https://acm.hdu.edu.cn/showproblem.php?pid=6638 ✔️

T2 https://acm.hdu.edu.cn/showproblem.php?pid=6606 ✔️

T3 https://acm.hdu.edu.cn/showproblem.php?pid=6609

T4 https://www.luogu.com.cn/problem/CF600E dsu on tree✔️ 线段树合并✖️

T5 https://www.luogu.com.cn/problem/P3521 ✔️吃老本

T6 https://www.luogu.com.cn/problem/P4556 ✔️吃老本

T7 https://codeforces.com/problemset/problem/1181/D

T8 https://codeforces.com/problemset/problem/1354/D

## Day 5

https://vjudge.net/contest/448336

T1 https://www.luogu.com.cn/problem/CF955D ✔️

T2 https://www.luogu.com.cn/problem/CF985F ✔️

T3 https://darkbzoj.tk/problem/2462

T4 https://www.luogu.com.cn/problem/UVA1519

T5 https://www.luogu.com.cn/problem/P4052 ✔️

T6 https://vjudge.net/problem/HihoCoder-1877 hihocoder

T7 https://acm.hdu.edu.cn/showproblem.php?pid=3336 ✔️

T8 https://www.luogu.com.cn/problem/UVA10298 ✔️吃老本

T9 https://www.luogu.com.cn/problem/P3435 ✔️吃老本

T10 http://poj.org/problem?id=2752 ✔️

T11 https://www.luogu.com.cn/problem/P2375 ✔️吃老本

T12 https://www.luogu.com.cn/problem/P4600

## Day 6

依然是字符串 https://vjudge.net/contest/448336

扩展kmp

T1 https://acm.hdu.edu.cn/showproblem.php?pid=2594

T2 https://acm.hdu.edu.cn/showproblem.php?pid=6629

马拉车拉马

T3 https://codeforces.com/gym/101981/attachments

T4 https://www.luogu.com.cn/problem/P3454

## Day 7

21 暑期集训C班 day2

T1 贪心sbt。

T2 自己脑残加了些特判来优化，爆了。还有就是0+没有特判。

T3 写了二分+二分，O(qlognlogm)，还算得了个80分吧。

艹，已经很接近正解了。。。

我的二分+二分相当于两次二分出 $i$ 和 $j$ ，看是否满足 $i+j=\frac{n}{2}$ 。

其实只用一次二分 $i$ ，看 $\frac{n}{2}-i$ 是否在另一个序列中。

T4 正解显然是 AC自动机+数位dp ，然而数位dp写炸了，最后想交个暴力结果暴力也挂了，抱灵了。

$f[statu][i][0/1][0/1][bin]$

有关中位数的题1 https://www.luogu.com.cn/problem/AT2165

二分答案mid，最下面一行大于 $mid$ 设为 $1$ ，小于 $mid$ 设为 $0$ 。

有关中位数的题2 https://acm.ecnu.edu.cn/problem/3681/

二分一个 $mid$ ，大于 $mid$ 的设为 $1$ ，小于 $mid$ 的设为 $-1$ ，按拓扑序dp求最长路看是否大于 $0$ 。

## Day 8

https://www.luogu.com.cn/problem/P3350

https://www.luogu.com.cn/problem/SP2371

https://acm.hdu.edu.cn/showproblem.php?pid=6800

https://www.luogu.com.cn/problem/P5163

https://www.luogu.com.cn/problem/CF1365G

## Day 9

各品种平衡树

https://www.luogu.com.cn/problem/P1486

https://www.luogu.com.cn/problem/P2161

https://www.luogu.com.cn/problem/P2521

https://www.luogu.com.cn/problem/P3224


## Day 10

可持久化数据结构

### 例题

https://codeforces.com/contest/323/problem/C

https://loj.ac/p/2718

https://loj.ac/p/3048

https://loj.ac/p/2555

https://loj.ac/p/3346

https://www.luogu.com.cn/problem/P2839

http://acm.hdu.edu.cn/showproblem.php?pid=5756

http://acm.hdu.edu.cn/showproblem.php?pid=5118

https://codeforces.com/contest/1340/problem/F

### 课后练习

https://loj.ac/p/2551

https://uoj.ac/problem/29

https://loj.ac/p/2310

https://codeforces.ml/contest/702/problem/F

## Day 11

### 例题

https://www.luogu.com.cn/problem/P2408

https://codeforces.ml/contest/1073/problem/G

https://codeforces.ml/contest/232/problem/D

https://codeforces.ml/contest/666/problem/E

https://onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=1770

https://loj.ac/p/2083

https://codeforces.ml/contest/1063/problem/F

课后练习

http://poj.org/problem?id=3581

https://loj.ac/p/2133

https://loj.ac/p/2073

https://loj.ac/p/3326

## Day 12

### 例题

https://www.luogu.com.cn/problem/P1896

https://codeforces.ml/problemset/problem/1238/E

https://www.luogu.com.cn/problem/P4127

https://loj.ac/p/6770

https://www.luogu.com.cn/problem/P1850

https://codeforces.com/gym/101623/problem/E

https://codeforces.ml/problemset/problem/1237/F

https://atcoder.jp/contests/arc112/tasks/arc112_e

http://poj.org/problem?id=1769

https://acm.hdu.edu.cn/showproblem.php?pid=6856

https://codeforces.ml/contest/1322/problem/D

https://www.luogu.com.cn/problem/P3628

https://loj.ac/p/2249

https://acm.hdu.edu.cn/showproblem.php?pid=6065

https://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=2591

### 课后练习

https://codeforces.ml/contest/1106/problem/E

https://loj.ac/p/2540

https://atcoder.jp/contests/dp/tasks/dp_y

https://atcoder.jp/contests/dp/tasks/dp_w

https://www.luogu.com.cn/problem/P2612

https://www.luogu.com.cn/problem/P4027

## Day 13