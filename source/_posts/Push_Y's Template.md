---
title: Push_Y's Template
date: 2021-07-25 09:26:28
tag: 学习笔记
category: 学习笔记
---

## 平衡树

### 权值线段树

```cpp
namespace SegmentTree{

    int sz[N<<2];

    inline void pushup(int x){sz[x]=sz[ls]+sz[rs];}

    void upd(int pos,int d,int x=1,int l=1,int r=m){
        if(l==r){
            sz[x]+=d;
            return ;
        }
        int mid=l+r>>1;
        if(pos<=mid) upd(pos,d,ls,l,mid);
        else upd(pos,d,rs,mid+1,r);
        pushup(x);
    }

    int rk(int pos,int x=1,int l=1,int r=m){
        if(l==r) return 1;
        int mid=l+r>>1;
        if(pos<=mid) return rk(pos,ls,l,mid);
        else return sz[ls]+rk(pos,rs,mid+1,r);
    }

    int kth(int k,int x=1,int l=1,int r=m){
        if(l==r) return l;
        int mid=l+r>>1,t=sz[ls];
        if(k<=t) return kth(k,ls,l,mid);
        else return kth(k-t,rs,mid+1,r);
    }

}

```

### Splay

```cpp
namespace Splay{

    int ch[N][2],fa[N],val[N],sz[N],cnt[N],rt,idx;

    inline void push(int x){sz[x]=sz[ch[x][0]]+sz[ch[x][1]]+cnt[x];}

    inline bool wrt(int x){return x==ch[fa[x]][1];}
    inline void rotate(int x){
        int p=fa[x],g=fa[p],k=wrt(x),b=ch[x][k^1];
        ch[p][k]=b, fa[b]=p;
        ch[g][wrt(p)]=x, fa[x]=g;
        ch[x][k^1]=p, fa[p]=x;
        push(p),push(x);
    }

    inline void splay(int x,int tar=0){
        while(fa[x]!=tar){
            if(fa[fa[x]]!=tar)
                wrt(x)==wrt(fa[x])?rotate(fa[x]):rotate(x);
            rotate(x);
        }
        if(!tar) rt=x;
    }

    inline void find(int v){
        int x=rt;
        while(ch[x][v>val[x]] && v!=val[x]){
            x=ch[x][v>val[x]];
        }
        splay(x);
    }

    inline void ins(int v){
        int x=rt,p=0;
        while(x && val[x]!=v){
            p=x;
            x=ch[x][v>val[x]];
        }
        if(x) cnt[x]++;
        else {
            x=++idx;
            if(p) ch[p][v>val[p]]=x;
            fa[x]=p, val[x]=v;
            ch[x][0]=ch[x][1]=0;
            cnt[x]=sz[x]=1;
        }
        splay(x);
    }

    inline int rk(int v){
        find(v);
        return sz[ch[rt][0]];
    }

    inline int kth(int k){
        int x=rt;
        while(1){
            if(ch[x][0] && k<=sz[ch[x][0]]) x=ch[x][0];
            else if(k>sz[ch[x][0]]+cnt[x]) k-=sz[ch[x][0]]+cnt[x],x=ch[x][1];
            else {
                splay(x);
                return x;
            }
        }
    }

    inline int pre(int v){
        find(v);
        if(v>val[rt]) return rt;
        int x=ch[rt][0];
        while(ch[x][1]) x=ch[x][1];
        splay(x);
        return x;
    }

    inline int nxt(int v){
        find(v);
        if(v<val[rt]) return rt;
        int x=ch[rt][1];
        while(ch[x][0]) x=ch[x][0];
        splay(x);
        return x;
    }

    inline void del(int w){
        int u=pre(w),v=nxt(w);
        splay(u),splay(v,u);
        int x=ch[v][0];
        if(cnt[x]>1){
            cnt[x]--;
            splay(x);
        }
        else ch[v][0]=0;
        push(v),push(u);
    }

}
```

### Treap

```cpp
namespace Treap{

    int sz[N],rd[N],ch[N][2],val[N],cnt[N],idx,rt;

    inline void push(int x){sz[x]=sz[ch[x][0]]+sz[ch[x][1]]+cnt[x];}

    inline void rotate(int& p,int k){
        int x=ch[p][k^1];
        ch[p][k^1]=ch[x][k];
        ch[x][k]=p;
        push(p),push(x);
        p=x;
    }

    void ins(int& x,int v){
        if(!x){
            x=++idx;
            sz[x]=cnt[x]=1;
            ch[x][0]=ch[x][1]=0;
            val[x]=v;
            rd[x]=rand();
            return ;
        }
        if(v==val[x]){
            cnt[x]++,sz[x]++;
            return ;
        }
        int k=v>val[x];
        ins(ch[x][k],v);
        if(rd[x]<rd[ch[x][k]]) rotate(x,k^1);
        push(x);
    }

    void del(int& x,int v){
        if(!x) return ;
        if(v<val[x]) del(ch[x][0],v);
        else if(v>val[x]) del(ch[x][1],v);
        else {
            if(!ch[x][0] && !ch[x][1]){
                cnt[x]--,sz[x]--;
                if(cnt[x]==0) x=0;
            }
            else if(ch[x][0] && !ch[x][1]){
                rotate(x,1);
                del(ch[x][1],v);
            }
            else if(!ch[x][0] && ch[x][1]){
                rotate(x,0);
                del(ch[x][0],v);
            }
            else {
                int k=rd[ch[x][0]]>rd[ch[x][1]];
                rotate(x,k);
                del(ch[x][k],v);
            }
        }
        push(x);
    }

    int rk(int x,int v){
        if(!x) return 0;
        if(v==val[x]) return sz[ch[x][0]]+1;
        if(v<val[x]) return rk(ch[x][0],v);
        else return sz[ch[x][0]]+cnt[x]+rk(ch[x][1],v);
    }

    int kth(int x,int k){
        if(!x) return 0;
        if(k<=sz[ch[x][0]]) return kth(ch[x][0],k);
        else if(k>sz[ch[x][0]]+cnt[x]) return kth(ch[x][1],k-sz[ch[x][0]]-cnt[x]);
        else return val[x];
    }

    int pre(int x,int v){
        if(!x) return -inf;
        if(v<=val[x]) return pre(ch[x][0],v);
        else return max(val[x],pre(ch[x][1],v));
    }

    int nxt(int x,int v){
        if(!x) return inf;
        if(v>=val[x]) return nxt(ch[x][1],v);
        else return min(val[x],nxt(ch[x][0],v));
    }

}
```

### fhq-Treap


## 字符串

### 扩展kmp

```cpp
struct exkmp{

    int nxt[N],extend[N];

    void GetNext(){
        int a=0;
        nxt[0]=m;
        while(a<m-1 && t[a]==t[a+1]) a++;
        nxt[1]=a,a=1;
        for(int k=2;k<m;k++){
            int p=a+nxt[a]-1,L=nxt[k-a];
            if(k+L-1>=p){
                int j=(p-k+1)>0?p-k+1:0;
                while(k+j<m && t[k+j]==t[j]) j++;
                nxt[k]=j;
                a=k;
            }
            else nxt[k]=L;
        }
    }

    void GetExtend(){
        int a=0;
        while(a<m && s[a]==t[a]) a++;
        extend[0]=a,a=0;
        for(int k=1;k<n;k++){
            int p=a+extend[a]-1,L=nxt[k-a];
            if(k+L-1>=p){
                int j=(p-k+1)>0?(p-k+1):0;
                while(k+j<n && j<m && s[k+j]==t[j]) j++;
                extend[k]=j;
                a=k;
            }
            else extend[k]=L;
        }
    }

}K;
```

### Manacher

```cpp
struct Manacher{
    int f[N];
    void solve(char* a,int n){
        int r=0,p=0;
        for(int i=0;i<n;i++){
            if(i<r) f[i]=min(f[2*p-i],r-i);
            else f[i]=1;
            while(0<=i-f[i] && i+f[i]<n && a[i-f[i]]==a[i+f[i]]) f[i]++;
            if(i+f[i]-1>r) r=i+f[i]-1,p=i;
        }
        for(int i=0;i<n;i++) f[i]--;
    }
}man;
```