---
kind: "coding-problem"
title: "Build (Day 1)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 1/build.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Build (Day 1)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Problem

The source has reference code without a separate problem statement. Establish its inputs, expected outputs, and constraints before practising.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · build.java
> ```java
> import java.util.*;
> import java.io.*;
>
> class build{
> 	static class node{
> 		int row;
> 		int col;
> 		node(int r,int c)
> 		{
> 			row=r;
> 			col=c;
> 		}
> 	}
> 	static int locate(int a[][],int r,int c)
> 	{
> 		int dist[][]=new int[r][c];
> 		int walk=1,min=-1;
> 		for(int i=0;i<r;i++)
> 		{
> 			for(int j=0;j<c;j++)
> 			{
> 				if(a[i][j]==1)
> 				{
>                     min=bfs(a,dist,--walk,i,j);
> 				}
> 			}
> 		}
> 		return min;
> 	}
> 	static int bfs(int a[][],int dist[][],int walk,int i,int j)
> 	{
> 		Queue<node> q=new LinkedList<node>();
> 		
> 		int check[][]={{0,1},{1,0},{0,-1},{-1,0}};
> 		int depth=0,min=-1;
> 		q.add(new node(i,j));
> 		
> 		while(!q.isEmpty())
> 		{
> 			depth++;
> 			int length=q.size();
> 			for(int k=0;k<length;k++)
> 			{
> 				node n=q.poll();
> 				int row=n.row;
> 				int col=n.col;
> 				for(int l=0;l<4;l++)
> 				{
>
> 					int x=row+check[l][0];
> 					int y=col+check[l][1];
>
>
> 					if(x<0 || x>=a.length || y<0 || y>=a[x].length || a[x][y]!=walk)
> 					{
> 						continue;
> 					}
>
> 					a[x][y]=walk-1;
> 					dist[x][y]+=depth;
> 				
>                     
> 					q.add(new node(x,y));
>
> 					if(min<0 || min>dist[x][y])
> 					{
> 						min=dist[x][y];
> 					}
>
>
> 				}
> 			}
>
>
> 		}
> 		return min;
>
> 	}
> 	public static void main(String[] args) {
> 	       int r,c;
> 	       Scanner sc=new Scanner(System.in);
> 	       r=sc.nextInt();
> 	       c=sc.nextInt();
> 	       int a[][]=new int[r][c];
> 	       for(int i=0;i<r;i++)
> 	       {
> 	       	for(int j=0;j<c;j++)
> 	       	{
>                  a[i][j]=sc.nextInt();
> 	       	}
> 	       }
> 	       System.out.println(locate(a,r,c));	
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%201/build.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 1/build.java
