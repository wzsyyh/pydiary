---
title: CODE
date: 2021-10-19 18:37:16
tag: 
category: 
---

### CF504E

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef pair<int,int> pi;
typedef long long ll;
inline int gin() {
    int s=0,f=1;
    char c=getchar();
    while(c<'0' || c>'9') {
        if(c=='-') f=-1;
        c=getchar();
    }
    while(c>='0'&&c<='9') {
        s=(s<<3)+(s<<1)+(c^48);
        c=getchar();
    }
    return s*f;
}

const int N=3e5+5,mod=1e9+7;
int n,m,dep[N],sz[N],son[N],fa[N],dfn[N],zmz[N],top[N],dfc;
char str[N];
const pi B={131,13331};
pi bin[N],h1[N],h2[N];
vector<int> e[N];

inline pi operator + (pi a,pi b) {return {(a.first+b.first)%mod,(a.second+b.second)%mod};}
inline pi operator - (pi a,pi b) {return {(a.first-b.first+mod)%mod,(a.second-b.second+mod)%mod};}
inline pi operator * (pi a,pi b) {return {1ll*a.first*b.first%mod,1ll*a.second*b.second%mod};}
inline pi Hash(bool op,int x,int k) {
    if(op) return h2[x-k+1]-h2[x+1]*bin[k];
    return h1[x+k-1]-h1[x-1]*bin[k];
}

void dfs1(int u,int f) {
    sz[u]=1,dep[u]=dep[fa[u]=f]+1;
    for(int v:e[u]) if(v!=f) {
        dfs1(v,u);
        sz[u]+=sz[v];
        if(sz[v]>sz[son[u]]) son[u]=v;
    }
}

void dfs2(int u,int topf) {
    top[u]=topf,dfn[u]=++dfc,zmz[dfc]=u;
    if(son[u]) dfs2(son[u],topf);
    for(int v:e[u]) if(!top[v]) dfs2(v,v);
}

int lca(int x,int y) {
    while(top[x]!=top[y]) {
        if(dep[top[x]]<dep[top[y]]) swap(x,y);
        x=fa[top[x]];
    }
    return dep[x]<dep[y]?x:y;
}

vector<pi> get(int x,int y) {
    int z=lca(x,y);
    // puts("Yes?");
    vector<pi> q1,q2;
    while(dep[top[x]]>dep[z]) q1.push_back({x,top[x]}),x=fa[top[x]];
    // puts("Why?");
    q1.push_back({x,z});
    while(dep[top[y]]>dep[z]) q2.push_back({top[y],y}),y=fa[top[y]];
    // puts("Sure?");
    if(y!=z) q2.push_back({son[z],y});
    while(q2.size()) q1.push_back(q2.back()),q2.pop_back();
    return q1;
}

signed main() {
    #ifndef ONLINE_JUDGE
    freopen("test.in","r",stdin);
    freopen("test.out","w",stdout);
    #endif
    n=gin();
    scanf("%s",str+1);
    bin[0]={1,1},bin[1]=B;
    for(int i=1;i<n;i++) {
        int u=gin(),v=gin();
        e[u].push_back(v),e[v].push_back(u);
        bin[i+1]=bin[i]*B;
    }
    dfs1(1,0);
    dfs2(1,1);
    for(int i=1;i<=n;i++) {
        h1[i]=h1[i-1]*B+(pi){str[zmz[i]],str[zmz[i]]};
        h2[n-i+1]=h2[n-i+2]*B+(pi){str[zmz[n-i+1]],str[zmz[n-i+1]]};
    }
    m=gin();
    while(m--) {
        int a=gin(),b=gin(),c=gin(),d=gin(),ans=0,s=0,t=0;
        vector<pi> f=get(a,b),g=get(c,d);
        // puts("#");
        while(s<f.size() && t<g.size()) {
            // puts("@");
            int fl=dfn[f[s].first],fr=dfn[f[s].second];
            int gl=dfn[g[t].first],gr=dfn[g[t].second];
            bool tf=fl>fr,tg=gl>gr;
            int lenf=(tf?fl-fr:fr-fl)+1;
            int leng=(tg?gl-gr:gr-gl)+1;
            int len=min(lenf,leng);
            pi hf=Hash(tf,fl,len);
            pi hg=Hash(tg,gl,len);
            if(hf==hg) {
                if(len==lenf) s++;
                else f[s].first=zmz[fl+(tf?-1:1)*len];
                if(len==leng) t++;
                else g[t].first=zmz[gl+(tg?-1:1)*len];
                ans+=len;
            }
            else {
                int l=1,r=len;
                while(l<r) {
                    int mid=l+r>>1;
                    hf=Hash(tf,fl,mid);
                    hg=Hash(tg,gl,mid);
                    if(hf==hg) l=mid+1;
                    else r=mid;
                }
                ans+=l-1;
                break;
            }
        }
        printf("%d\n",ans);
    }
    return 0;
}
```

### CF547D

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef pair<int,int> pi;
typedef long long ll;
inline int gin() {
    int s=0,f=1;
    char c=getchar();
    while(c<'0' || c>'9') {
        if(c=='-') f=-1;
        c=getchar();
    }
    while(c>='0'&&c<='9') {
        s=(s<<3)+(s<<1)+(c^48);
        c=getchar();
    }
    return s*f;
}

const int N=2e5+5;
int n,prex[N],prey[N],col[N];
vector<int> g[N];

void dfs(int u) {
    for(int v:g[u]) if(col[v]==-1) col[v]=!col[u],dfs(v);
}

signed main() {
    #ifndef ONLINE_JUDGE
    freopen("test.in","r",stdin);
    freopen("test.out","w",stdout);
    #endif
    n=gin();
    for(int i=1;i<=n;i++) {
        int x=gin(),y=gin();
        col[i]=-1;
        if(!prex[x]) prex[x]=i;
        else g[prex[x]].push_back(i),g[i].push_back(prex[x]),prex[x]=0;
        if(!prey[y]) prey[y]=i;
        else g[prey[y]].push_back(i),g[i].push_back(prey[y]),prey[y]=0;
    }
    for(int i=1;i<=n;i++) if(col[i]==-1) col[i]=0,dfs(i);
    for(int i=1;i<=n;i++) putchar(col[i]?'b':'r');
    return 0;
}
```