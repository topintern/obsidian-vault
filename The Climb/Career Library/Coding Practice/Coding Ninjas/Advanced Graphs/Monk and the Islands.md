---
kind: "coding-problem"
title: "Monk and the Islands"
collection: "Coding Ninjas"
topic: "Advanced Graphs"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/5.Adv graphs/monk islands q.txt","CODING RESOURCES/coding ninjas/5.Adv graphs/monk islands s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Monk and the Islands

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

MONK AND THE ISLAND
Monk visits the land of Islands. There are a total of N islands numbered from 1 to N. Some pairs of islands are connected to each other by Bidirectional bridges running over water.
Monk hates to cross these bridges as they require a lot of efforts. He is standing at Island #1 and wants to reach the Island #N. Find the minimum the number of bridges that he shall have to cross, if he takes the optimal route.

### Input

First line contains T. T testcases follow.
First line of each test case contains two space-separated integers N, M.
Each of the next M lines contains two space-separated integers X and Y , denoting that there is a bridge between Island X and Island Y.

### Output

Print the answer to each test case in a new line.

### Constraints

1 = T = 10
1 = N = 10000
1 = M = 100000
1 = X, Y = N

### SAMPLE INPUT

```text
2
3 2
1 2
2 3
4 4
1 2
2 3
3 4
4 2
```

### SAMPLE OUTPUT

```text
2
2
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · monk islands s.txt
> ```cpp
> #include <bits/stdc++.h>
>  
> using namespace std;
>  
> #define max 100005
>  
>  
>  
>  
>  
> int main()
> {
> 	int t,i0;
> 	cin>>t;
> 	for(i0=0;i0<t;i0++)
> 	{
> 		int n,m,i,j;
> 		cin>>n>>m;
> 		vector <int> brid[max];
> 		for(i=0;i<m;i++)
> 		{
> 			int x,y;
> 			cin>>x>>y;
>             brid[x].push_back(y);
>             brid[y].push_back(x);
> 		}
>  
> 		//cout<<bfs(1,n)<<endl;
>  
> 		queue <int> q;
> 	int level[max];
> 	bool visited[max];
> 	for(i=0;i<max;i++)
> 	{
> 		visited[i]=false;
> 	}
> 	q.push(1);
>     visited[1]=true;
>     level[1]=0;
>  
>     
>     while(!q.empty())
>     {   
>     	int p=q.front();
>     	q.pop();
>         for(i=0;i<brid[p].size();i++)
>         {   
>            if(visited[brid[p][i]]==false)
>            {
>                level[brid[p][i]]=level[p] + 1;
>                q.push(brid[p][i]);
>                visited[brid[p][i]]=true;
>            
>            }
>         }
>     }
>  
>     cout<<level[n]<<endl;
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/5.Adv%20graphs/monk%20islands%20q.txt) · CODING RESOURCES/coding ninjas/5.Adv graphs/monk islands q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/5.Adv%20graphs/monk%20islands%20s.txt) · CODING RESOURCES/coding ninjas/5.Adv graphs/monk islands s.txt
