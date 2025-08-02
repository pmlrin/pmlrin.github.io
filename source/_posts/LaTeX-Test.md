---
title: LaTeX-Test
date: 2024-07-29 22:15:45
tags:
  - LaTeX
categories:
  - LaTeX
password: "123456"
author:
 - Pomelorin
---

$$
\Huge\sum_{i=1}^{+\infty}=\dfrac{+\infty}{2}
$$

$$
\Huge\text{主}=6
$$

<!-- more -->

```c++
#include<bits/stdc++.h>
using namespace std;

namespace _yz
{
	typedef long long ll;
	const ll N=200000+10;
	struct point{ll x,y,n,t;}p[N];
	ll n,ans=0;
	multiset<point>s;
	bool operator<(point a,point b)
	{
		if(a.x==b.x) return a.y<b.y;
		return a.x<b.x;
	}
	bool cmp(point a,point b)
	{
		if(a.y==b.y) return a.x>b.x;
		return a.y>b.y;
	}
	void main()
	{
		ll opt,a,b,c;
		scanf("%lld",&n);
		for(ll i=1;i<=n;i++)
		{
			scanf("%lld%lld%lld%lld",&opt,&b,&a,&c);
			p[i]=(point){a+b,b-a,c,opt};
		}
		sort(p+1,p+n+1,cmp);
		for(ll i=1;i<=n;i++)
		{
			if(p[i].t==2) s.insert(p[i]);
			else
			{
				while(p[i].n)
				{
					auto it=s.lower_bound(p[i]);
					if(it==s.end()) break;
					point now=(*it);
					ll add=min(now.n,p[i].n);
					p[i].n-=add; now.n-=add; ans+=add;
					s.erase(it);
					if(now.n>=1) s.insert(now);
				}
			}
		}
		printf("%lld\n",ans);
		return;
	}
}
int main()
{
	_yz::main();
	return 0;
}
```

![](https://cdn.jsdelivr.net/gh/Yurchiu/PicGo/20240325_202902.jpg)