---
kind: "coding-problem"
title: "Largest Piece"
collection: "Coding Ninjas"
topic: "Graph Basics"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/4.Graphs-1/largest pice q.txt","CODING RESOURCES/coding ninjas/4.Graphs-1/largest pice s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Largest Piece

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Its Gary's birthday today and he has ordered his favourite square cake consisting of '0's and '1's . But Gary wants the biggest piece of '1's and no '0's . A piece of cake is defined as a part which consist of only '1's, and all '1's share an edge with eachother on the cake. Given the size of cake N and the cake , can you find the size of the biggest piece of '1's for Gary ?

### Constraints

1<=N<=50

### Input Format

Line 1 : An integer N denoting the size of cake 
Next N lines : N characters denoting the cake

### Output Format

Size of the biggest piece of '1's and no '0's

### Sample Input

```text
2
11
01
```

### Sample Output

```text
3
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · largest pice s.txt
> ```java
> import java.util.Scanner;
>
> public class solution {
> 	public static int NMAX=55;
> 	public static int [][]visited=new int[NMAX][NMAX];
> 	public static String []A=new String[NMAX];
> 	int cx[]={0,0,-1,1};//change in x while taking four moves
> 	int cy[]={1,-1,0,0};//change in y while taking four moves
> 	//Consider a cake to be connected graph with every vertex connected to its nearby 4 vertices 
> 	public int max(int a,int b)
> 	{
> 		if(a<b)
> 			return b;
> 		return a;
> 	}
> 	public int dfs(int x,int y,int n)
> 	{
> 		if(visited[x][y]==1)
> 			return 0;
> 		visited[x][y]=1;
> 		int coun=1;
> 		for(int i=0;i<4;i++)
> 		{
> 			int dx=x+cx[i];
> 			int dy=y+cy[i];
> 			if(dx>=0&&dx<n&&dy>=0&&dy<n&&A[dx].charAt(dy)=='1')
> 			{
> 				coun+=dfs(dx,dy,n);
> 			}
> 		}
> 		return coun;
> 	}
> 	public int solve(int n,String cake[])
> 	{
> 		for(int i=0;i<n;i++)
> 			for(int j=0;j<n;j++)
> 				{
> 					A[i]=cake[i];
> 				}
> 		int maxsize=0;
> 		for(int i=0;i<n;i++)
> 			for(int j=0;j<n;j++)
> 			{
> 				if(A[i].charAt(j)=='1'&&visited[i][j]==0)
> 				{
> 					maxsize=max(maxsize,dfs(i,j,n));
> 				}
> 			}	
> 		return 	maxsize;
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/4.Graphs-1/largest%20pice%20q.txt) · CODING RESOURCES/coding ninjas/4.Graphs-1/largest pice q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/4.Graphs-1/largest%20pice%20s.txt) · CODING RESOURCES/coding ninjas/4.Graphs-1/largest pice s.txt
