---
layout:     post
title:      "luogu提高篇-深入浅出刷题笔记"
subtitle:   "luogu刷题"
date:       2024-07-22 23:00:00
author:     "Sage"
header-img: ""
header-style: text
hidden: false
catalog: true
published: true
tags:
    - luogu
---

# 参考

- [**Erik_Tse**](https://space.bilibili.com/231911980/channel/collectiondetail?sid=1403629)

# 第11章 递推与递归

# 第12章 贪心

# 第14章 搜索

# 第17章 集合

## 1、并查集

- 原理
  - [参考视频](https://www.bilibili.com/video/BV1Bh4y1k7fZ/?spm_id_from=333.999.0.0&vd_source=ce61818c8667e3f2de36a179a3c6e3af)
- 合并方法

  - 合并总在根上：任何非根节点的相连都必须转换成它们各自的根节点相连

  - 根相同不用合并（其实就是根只向根，多余的操作但是不矛盾）
- 优化方法

  - 路径压缩[O(1)]

    - 特点：破坏树结构
- 理解路径压缩：每次查找的时候把爷孙改成父子关系，减少查找的路径；
  - 按秩合并[O(logn)]
  
  - 树要又矮又胖
  
  - rnk小的指向大的
  
  - 只有rnk相等才需要更新秩
  - 启发式合并（按大小合并）[O(logn)]
  - sz需要提前初始化为1

### P1551 亲戚-1

- 20240722
- 特点
  - 标准并查集
  - 路径压缩[O(1)]


[亲戚](https://www.luogu.com.cn/problem/P1551)

```c++
#include <bits/stdc++.h>
using namespace std;

#define MAXN 5010
int n,m,p,x,y;
int fa[MAXN],rnk[MAXN],sz[MAXN];

//一、路径压缩
//2.查询:找祖宗，并压缩路径
// int find(int x){
//     return x == fa[x]? x:fa[x]= find(fa[x]);//理解赋值号的作用
// }

// //1.合并
// void join(int c1,int c2){//连接两个集合
//     int f1=find(c1),f2 = find(c2);
//     if(f1!=f2)fa[f1]= f2;
// }


//二、按秩合并
// int find(int x){
//     while (x^fa[x])x=fa[x];
//     return x ;
// }

// //1.合并
// void join(int c1,int c2){//连接两个集合
//     int f1=find(c1),f2 = find(c2);
//     if(f1!=f2){
//         if(rnk[f1]>rnk[f2])swap(f1,f2);
//         fa[f1]=f2;
//         if(rnk[f1]==rnk[f2])rnk[f2]++;
//     }
// }

//三、按大小合并
int find(int x){
    while (x^fa[x])x=fa[x];
    return x ;
}

//1.合并
void join(int c1,int c2){//连接两个集合
    int f1=find(c1),f2 = find(c2);
    if(f1!=f2){
        if(sz[f1]>sz[f2])swap(f1,f2);
        fa[f1]=f2;
        sz[f2]+=sz[f1];
    }
}

int main(){
    // freopen("in.txt","r",stdin);
    cin>>n>>m>>p;
    for(int i=1;i<= n; ++i)fa[i]= i,sz[i]=1;
    for(int i=0;i<m; ++i){
        cin >> x >> y;
        join(x,y);
    }
    for(int i=0;i<p; ++i){
        cin >>x >> y;
        if (find(x)== find(y))
            cout <<"Yes"<< endl;
        else
            cout<<"No"<< endl;
    }
    return 0;
}
```

### P1955⭐️⭐️⭐️ [NOI2015] 程序自动分析-1

- 20240722

- 特点

  - 离散化处理，节约空间

    - map中判定元素存在的方式

    ```c++
    if(m[k]== 0)
    if(m.find(k)== m.end())
    if(m.count(k))
    ```


[P1955 [NOI2015] 程序自动分析](https://www.luogu.com.cn/problem/)

```c++
#include <bits/stdc++.h>
using namespace std;

#define MAXN 200005
int fa[MAXN],rnk[MAXN],sz[MAXN];

struct node{
    int l,r,e;
}ns[100005];

int find(int x){
    return x==fa[x]? x:fa[x]=find(fa[x]) ;
}

//1.合并
void join(int c1,int c2){//连接两个集合
    // int f1=find(c1),f2 = find(c2);
    // if(f1!=f2)fa[f1]= f2;

    fa[find(c1)]= find(c2);
}

bool cmp(node n1,node n2){
    return n1.e >n2.e;
}
 
void judge(){
    int n,mark=1;
    cin >> n;
    map<int,int> m;
    for(int i = 0; i < n; i++){
        scanf("%d%d%d",&ns[i].l,&ns[i].r,&ns[i].e);
        //离散化
        if (!m[ns[i].l])
        {
            m[ns[i].l]=mark;
            mark++;
        }

        if (!m[ns[i].r])
        {
            m[ns[i].r]=mark;
            mark++;
        }
    }

    sort(ns,ns+n,cmp);

    for(int i=0; i <n; i++){
        int l=m[ns[i].l],r=m[ns[i].r];

        if(ns[i].e){
            fa[find(l)]=find(r);
        }else{
            int x=find(l),y=find(r);
            if (x==y)
            {
                cout <<"NO"<< endl;
                return;
            }
        }
    }
    cout <<"YES"<< endl;
}

int main(){
    freopen("in.txt","r",stdin);
    int t;
    cin >> t;
    for(int i =0; i<t; i++){
        for(int j=0;j< MAXN; j++)fa[j]= j;
        judge();
    }
    return 0;

}
```
# 第18章 图的基本应用
