---
layout:     post
title:      "jz-2024-junior-grade5th"
subtitle:   "OJ刷题"
date:       2024-05-24 17:00:00
author:     "Sage"
header-img: ""
header-style: text
hidden: false
catalog: true
published: true
tags:
    - OJ	
    - chris
---

# 第一题：挑战（challenge）

(Input: challenge.in, Output: challenge.out)

## 时间限制: 1 s 空间限制: 256 MB

 

## 题目描述

Introl 组织了一场大挑战赛，并准备了丰厚的奖品，他给了挑战者每人一个加密之后的密码，并给了你加密的规则，请你还原它获得正确的密码拿到奖品。

加密规则如下：

对于任意字符串 S，将其中的每一个数字元素 num 都变换成 num+i（其中 i 是该字符的位置，且规定字符串的第一个字符位置为 1 ）如果结果大于 9，只保留个位数字。之后将其中的大写字母变成小写字母，将小写字母变成大写字母。

### 输入

从文件 challenge.in 中读入数据。

第一行输入一个正整数 N ，表示字符串的长度。

第二行输入加密之后的字符串 S 。

### 输出

输出到文件 challenge.out 中。

输出解密之后的字符串 S′。

## 样例数据

### 输入 

10
Xyi2NT7810

### 输出 

xYI8nt0020

### 数据范围限制

对于30% 的数据，1≤N≤10。

对于100% 的数据，1≤N≤1000。

```c
#include<bits/stdc++.h>
using namespace std;
int main()
{
    int n;
    freopen("challenge.in","r",stdin);
    freopen("challenge.out","w",stdout);
    cin>>n;
    string s;
    cin>>s;
    for(int i=0;i<n;i++)
	{
        if(s[i]>='a'&&s[i]<='z')
        s[i]-=32;
        else
		{
            if(s[i]>='A'&&s[i]<='Z')
            s[i]+=32;
            if(s[i]>='0'&&s[i]<='9')
			{
                int sum=s[i]-'0';
                int si=(i+1)%10;
                sum-=si;
                if(sum<0)
                sum=10+sum;
                s[i]=sum+'0';
            }
        }
        cout<<s[i];
    }
}
```

# 第二题：游戏（game）

(Input: game.in, Output: game.out)
时间限制: 1 s 空间限制: 256 MB

## 题目描述

Introl在玩一种特殊的游戏————凑顺子。

他现在有 n 张牌，每张牌的点数为 ai，他希望凑出尽可能多的顺子。

在该游戏中，顺子的定义为：点数大小连续的 m 张牌（m>1)，不能中断，不能重复。

例如 [1,2,3,4,5,6,7,] 是一个顺子，而 [1,2,4,5,6,7,8,9] 和 [1,2,2,3,4,5,6,7,8,9] 不是一个顺子。

需要注意的是，顺子不可以拆分，例如 [1,2,3,4,5,6,7,8,9] 不可以拆分成 [1,2,3,4]、[5,6,7,8,9] 两个顺子。

换句话说，先凑最长的顺子，剩下的牌再凑最长的顺子，以此类推，直到不能凑顺子为止，顺子长度最短为 2。

### 输入

从文件 game.in 中读入数据。

第一行输入一个正整数 N ，表示牌的个数。

第二行输入 N 个数，表示每张牌的点数 ai。

### 输出

输出到文件 game.out 中。

输出顺子的个数。

## 样例数据

### 输入 

13
2 1 2 3 5 4 4 3 5 8 7 6 9

### 输出 

2

### 数据范围限制

对于30% 的数据，1≤N≤10。

对于100% 的数据，1≤N≤1000,1≤ai≤100。
```c
#include<bits/stdc++.h>
using namespace std;
int a[1000001],s[1000001];
int main()
{
    int n;
    freopen("game.in","r",stdin);
    freopen("game.out","w",stdout);
    cin>>n;
    for(int i=1;i<=n;i++)
	{
        cin>>a[i];
        s[a[i]]++;
    }
    int ans=0;
    bool q=1;
    while(1)
	{
        for(int i=1;i<=100;i++)
		{
            if(s[i]!=0)
			{
                for(int j=i+1;;j++)
				{
                    if(s[j]==0)
					{
                        if(j!=i+1)
						{
                            ans++;
                            s[i]--;
                        }
                        break;
                    }
                    else
                    s[j]--;
                }
            }
        }
        q=0;
        for(int i=1;i<=100;i++)
		{
            if(s[i]!=0&&s[i+1]!=0)
            q=1;
        }
        if(!q)
        break;
    }
    cout<<ans;
}
```

# 第三题：涂色（paint）

(Input: paint.in, Output: paint.out)
时间限制: 2 s 空间限制: 256 MB

## 题目描述

Introl获得了一个N行的杨辉三角，他将每行中值为奇数的位置涂为了黑色。

Chihiro将提出M次询问，在第L行第R个位置是否被涂成黑色，请你回答 Yes 或 No。

### 输入

从文件 paint.in 中读入数据。

第一行两个整数N和M。

接下来M行，每行给出L,R表示一组询问。

### 输出

输出到文件 paint.out 中。

共M行，每行输出 Yes 或 No。

## 样例数据

### 输入 

3 2
2 2
3 2

### 输出 

Yes
No

### 数据范围限制

对于30% 的数据，1≤N,M≤50。

对于100% 的数据，1≤N≤4000，1≤M≤106。

### 提示

构成的杨辉三角为：

1

1 1

1 2 1

除第三行第二个位置外，其余位置均被涂为黑色。

```c
#include<bits/stdc++.h>
using namespace std;
int a[5000][5000];
int m,n,r,l;
int main()
{
	freopen("paint.in","r",stdin);
	freopen("paint.out","w",stdout);
	scanf("%d%d",&n,&m);
	a[1][1]=1;
	for(int i=2;i<=n;i++)
	{
		for(int j=1;j<=i;j++)
		a[i][j]=a[i-1][j-1]+a[i-1][j];
	}
	for(int i=1;i<=m;i++)
	{
		scanf("%d%d",&l,&r);
		if(a[l][r]%2!=0)
		printf("Yes\n");
		else 
		printf("No\n");
	}
}
```

# 第四题：区间（interval）

(Input: interval.in, Output: interval.out)
时间限制: 2 s 空间限制: 256 MB 

## 题目描述

Introl有一个长度为N且仅包含阿拉伯数字的字符串S=S1S2...Sn。

他会向你询问M次，在区间[L,R]中有多少个二元组 (i,j)(i<j)满足mex(Si,Sj)=K。

mex()函数表示未出现在序列中的最小非负整数。

### 输入

从文件 interval.in 中读入数据。

第一行两个整数N和M，分别表示字符串S的长度和询问次数。

第二行仅一个字符串S。

接下来M行，每行给出L,R,K表示一组询问。

### 输出

输出到文件 interval.out 中。

输出共有M行，每行一个整数，表示对应的询问的答案。

## 样例数据

### 输入 

5 2
10312
1 3 2
3 5 0

### 输出 

1
3

### 数据范围限制

对于30% 的数据，1≤M≤103。

对于另外20% 的数据，K=0。

对于100% 的数据，1≤L≤R≤N,K≤3×103，1≤M≤106。

### 提示

区间[1,3]中：

二元组 (1,2)满足mex(1,0)=2。

区间[3,5]中：

二元组 (3,4)满足mex(3,1)=0。

二元组 (3,5)满足mex(3,2)=0。

二元组 (4,5)满足mex(1,2)=0。

```c
#include<bits/stdc++.h>
using namespace std;
int n,m,f[3100][3100][3];
string s;
void d()
{
	scanf("%d%d",&n,&m);
	cin>>s;
    s="s"+s;
	return;
}
void g()
{
    int i=1;
    while(i<n)
    {
        int j=i,s0=0,s1=0,sj=0;
        while(j<=n)
        {
            if(s[j]=='0') 
            {
                f[i][j][1]+=(s0+sj);
                f[i][j][2]+=s1;
                s0++;
            }
            else
            {
                if(s[j]=='1') 
                {
                    f[i][j][0]+=(sj+s1);
                    f[i][j][2]+=s0;
                    s1++;
                }
                else 
                {
                    f[i][j][0]+=(sj+s1);
                    f[i][j][1]+=s0;
                    sj++;
                }
            }
            f[i][j][0]+=f[i][j-1][0];
            f[i][j][1]+=f[i][j-1][1];
            f[i][j][2]+=f[i][j-1][2];
            j++;
        }
        i++;
    }
    i=1;
    return;
}
void o()
{
	d();
    g();
    while(m--)
    {
        int l,r,k;
        cin>>l>>r>>k;
        if(k>2||l==r) 
		printf("0\n");
        else 
		printf("%d\n",f[l][r][k]);
    }
	return;
}
int main()
{
    freopen("interval.in","r",stdin);
    freopen("interval.out","w",stdout);
	o();
}
```

