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