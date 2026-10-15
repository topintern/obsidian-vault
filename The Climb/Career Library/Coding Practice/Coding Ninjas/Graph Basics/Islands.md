---
kind: "coding-problem"
title: "Islands"
collection: "Coding Ninjas"
topic: "Graph Basics"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/4.Graphs-1/islands q.txt","CODING RESOURCES/coding ninjas/4.Graphs-1/islands s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Islands

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

An island is a small piece of land surrounded by water . A group of islands is said to be connected if we can reach from any given island to any other island in the same group . Given N islands (numbered from 1 to N) and two lists of size M (u and v) denoting island u[i] is connected to island v[i] and vice versa . Can you count the number of connected groups of islands.

### Constraints

1<=N<=100
1<=M<=(N*(N-1))/2
1<=u[i],v[i]<=N

### Input Format

Line 1 : Two integers N and M
Line 2 : List u of size of M
Line 3 : List v of size of M
Output Return Format :
The count the number of connected groups of islands

### Sample Input

```text
2 1
1
2
```

### Sample Output

```text
1 
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · islands s.txt
> ```java
>
> public class solution {
> 	public static int[][] adj=new int[1005][1005];
> 	public static int [] visited=new int[1005];
> 	public void dfs(int u,int p,int n)
> 	{
> 		if(visited[u]!=0)
> 			return ;
> 		visited[u]=1;
> 		for(int i=1;i<=n;i++)
> 		if(adj[u][i]==1&&i!=p)
> 		{
> 			dfs(i,u,n);
> 		}
> 	}
> 	public int solve(int n,int m,int u[],int v[])
> 	{
> 		for(int i=0;i<m;i++)
> 		{
> 			adj[u[i]][v[i]]=1;
> 			adj[v[i]][u[i]]=1;
> 		}
> 		int connected_groups=0;
> 		for(int i=1;i<=n;i++)
> 		if(visited[i]==0)
> 		{
> 			dfs(i,i,n);
> 			connected_groups++;
> 		}
> 		return connected_groups;
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/4.Graphs-1/islands%20q.txt) · CODING RESOURCES/coding ninjas/4.Graphs-1/islands q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/4.Graphs-1/islands%20s.txt) · CODING RESOURCES/coding ninjas/4.Graphs-1/islands s.txt
