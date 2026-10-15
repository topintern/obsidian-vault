---
kind: "coding-problem"
title: "FILLMTR"
collection: "Coding Ninjas"
topic: "Advanced Graphs"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/5.Adv graphs/fillmtr q.txt","CODING RESOURCES/coding ninjas/5.Adv graphs/fillmtr s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# FILLMTR

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Fill The Matrix
A matrix B (consisting of integers) of dimension N × N is said to be good if there exists an array A (consisting of integers) such that B[i][j] = |A[i] - A[j]|, where |x| denotes absolute value of integer x.

You are given a partially filled matrix B of dimension N × N. Q of the entries of this matrix are filled by either 0 or 1. You have to identify whether it is possible to fill the remaining entries of matrix B (the entries can be filled by any integer, not necessarily by 0 or 1) such that the resulting fully filled matrix B is good.

### Input

The first line of the input contains an integer T denoting the number of test cases.

The first line of each test case contains two space separated integers N, Q.

Each of the next Q lines contain three space separated integers i, j, val, which means that B[i][j] is filled with value val.

### Output

For each test case, output "yes" or "no" (without quotes) in a single line corresponding to the answer of the problem.

### Constraints

1 = T = 10^6
2 = N = 10^5
1 = Q = 10^6
1 = i, j = N
0 = val = 1
Sum of each of N, Q over all test cases doesn't exceed 106

### Input

4
2 2
1 1 0
1 2 1
2 3
1 1 0
1 2 1
2 1 0
3 2
2 2 0
2 3 1
3 3
1 2 1
2 3 1
1 3 1

### Output

yes
no
yes
no

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · fillmtr s.txt
> ```cpp
> #include<bits/stdc++.h>
> using namespace std;
> typedef long long ll;
> #define pb push_back
> vector<ll> gp[100010];
> pair<ll,pair<ll,ll> > query[1000010];
> ll n,q;
> ll color[100010];
> map<ll,map<ll,ll> >m;
> bool isBipartiteUtil(ll src)
> {
>     color[src] = 1;
>     queue <ll> q;
>     q.push(src);
>     while (!q.empty())
>     {
>         ll u = q.front();
>         q.pop();
>         for (int v = 0; v < gp[u].size(); ++v)
>         {
>         	int vv=gp[u][v];
>         	int c=m[u][vv];
>             if (color[vv] == -1)
>             {
>                 if(c==0)
>                 color[vv]=color[u];
>                 else
>                 color[vv]=1-color[u];
>                 q.push(gp[u][v]);
>             }
>             else if (abs(color[gp[u][v]]-color[u])!=c)
>                 return false;
>         }
>     }
>     return true;
> }
> bool isBipartite()
> {
>     
>     for (int i = 0; i <=n; ++i)
>         color[i] = -1;
>     for (int i = 1; i <=n; i++)
>       if (color[i] == -1&&gp[i].size()>=1)
>         if (isBipartiteUtil(i) == false)
>            return false;
>      return true;
> }
> int main()
> {
> 	//freopen("input2.txt","r",stdin);
> 	//freopen("output2.txt","w",stdout);
> 	ll t;
> 	cin>>t;
> 	while(t--)
> 	{
> 		ll i=0;
> 		m.clear();
> 		bool ans =true;
> 		cin>>n>>q;
> 		for(ll j=0;j<=n;j++)
> 		gp[j].clear();
> 		while(i<q)
> 		{
> 			ll a,b,c;
> 			cin>>a>>b>>c;
> 			query[i].first=a;query[i].second.first=b;query[i].second.second=c;
> 				gp[a].pb(b);gp[b].pb(a);
> 				if(m.find(a)!=m.end()&&m[a].find(b)!=m[a].end())
> 				{
> 					int tt=m[a][b];
> 					if(tt!=c)
> 					ans=false;
> 				}
> 				else if(m.find(b)!=m.end()&&m[b].find(a)!=m[b].end())
> 				{
> 					int tt=m[b][a];
> 					if(tt!=c)
> 					ans=false;
> 				}
> 				else
> 				{
> 					m[a][b]=m[b][a]=c;
> 				}
> 			i++;
> 		}
> 		if(ans==false)
> 		{
> 			cout<<"no\n";
> 			continue;
> 		}
> 	       ans=isBipartite();
> 			if(ans==false)
> 			cout<<"no\n";
> 		   else
> 		   cout<<"yes\n";
> 		}
> 		
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/5.Adv%20graphs/fillmtr%20q.txt) · CODING RESOURCES/coding ninjas/5.Adv graphs/fillmtr q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/5.Adv%20graphs/fillmtr%20s.txt) · CODING RESOURCES/coding ninjas/5.Adv graphs/fillmtr s.txt
