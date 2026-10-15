---
kind: "coding-problem"
title: "3 Cycle"
collection: "Coding Ninjas"
topic: "Graph Basics"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/4.Graphs-1/3 cycle q.txt","CODING RESOURCES/coding ninjas/4.Graphs-1/3 cycle s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# 3 Cycle

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Given a graph with N vertices (numbered from 1 to N) and Two Lists (U,V) of size M where (U[i],V[i]) and (V[i],U[i]) are connected by an edge , then count the distinct 3-cycles in the graph. A 3-cycle PQR is a cycle in which (P,Q), (Q,R) and (R,P) are connected an edge.

### Input Format

Line 1 : Two integers N and M
Line 2 : List u of size of M
Line 3 : List v of size of M
Return Format :
The count the number of 3-cycles in the given Graph

### Constraints

1<=N<=100
1<=M<=(N*(N-1))/2
1<=u[i],v[i]<=N

### Sample Input

```text
3 3
1 2 3
2 3 1
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

> [!example]- Reference 1 · 3 cycle s.txt
> ```java
> import java.util.Scanner;
>
> public class solution {
> 	public static int[][] adj=new int[1005][1005];
> 	public int solve(int n,int m,int U[],int V[])
> 	{
> 		for(int i=0;i<m;i++)
> 		{
> 			adj[U[i]][V[i]]=1;
> 			adj[V[i]][U[i]]=1;
> 		}
> 		int cycles=0;
> 		Scanner scan = new Scanner(System.in);
> 		for(int a=1;a<=n;a++)
> 		{
> 			for(int b=1;b<=n;b++)
> 			if(adj[a][b]==1)
> 			{
> 				int u=b;
> 				for(int j=1;j<=n;j++)
> 				if(adj[u][j]==1)
> 				{
> 					int v=j;
> 					if(v==a)
> 						continue;
> 					//System.out.println("hi\n");
> 					if(adj[v][a]==1) // if a,u,v form a cycle :)
> 					{
> 						cycles++;
> 					}
> 				}
> 			}
> 		}
> 		return cycles/6; // A cycle is counted 6 times , (anticlockwise + clockwise )*(from A + from U + from V)
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/4.Graphs-1/3%20cycle%20q.txt) · CODING RESOURCES/coding ninjas/4.Graphs-1/3 cycle q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/4.Graphs-1/3%20cycle%20s.txt) · CODING RESOURCES/coding ninjas/4.Graphs-1/3 cycle s.txt
