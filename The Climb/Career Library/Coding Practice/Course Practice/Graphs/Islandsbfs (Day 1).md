---
kind: "coding-problem"
title: "Islandsbfs (Day 1)"
collection: "Course Practice"
topic: "Graphs"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 1/islandsbfs.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Islandsbfs (Day 1)

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

> [!example]- Reference 1 · islandsbfs.java
> ```java
> import java.util.*;
> import java.io.*;
>
> class islandsbfs{
> 	static class node{
> 		int row;
> 		int col;
> 		node(int r,int c)
> 		{
> 			row=r;
> 			col=c;
> 		}
> 	}
> 	
> 	
> 	static void bfs(int a[][],int v[][],int i,int j,int r,int c)
> 	{
> 		Queue<node> q=new LinkedList<node>();
> 		q.add(new node(i,j));
> 		int check[][]={{0,1},{1,0},{0,-1},{-1,0}};
> 		
> 		while(!q.isEmpty())
> 		{
> 			
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
> 					if(x<0 || x>=r || y<0 || y>=c || v[x][y]==1 ||a[x][y]==0)
> 					{
> 						continue;
> 					}
> 					v[x][y]=1;
> 				}
> 			}
>
>
> 		}
>
> 	}
> 	public static void main(String[] args) {
> 	       int r,c,p;
> 	       Scanner sc=new Scanner(System.in);
> 	       r=sc.nextInt();
> 	       c=sc.nextInt();
> 	       p=sc.nextInt();
> 	       int a[][]=new int[r][c];
> 	       int count=0;
> 	       for(int k=0;k<p;k++)
> 	       {
> 	       	a[sc.nextInt()][sc.nextInt()]=1;
> 	       	int v[][]=new int[r][c];
> 	       	count=0;
> 	       for(int i=0;i<r;i++)
> 	       {
> 	       	for(int j=0;j<c;j++)
> 	       	{
>                  if(a[i][j]==1 && v[i][j]!=1)
>                  {
>                  	bfs(a,v,i,j,r,c);
>                  	count++;
>                  }
> 	       	}
> 	       }
> 	       System.out.println(count);
> 	      }
> 	       	
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%201/islandsbfs.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 1/islandsbfs.java
