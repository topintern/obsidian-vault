---
kind: "coding-problem"
title: "Coding Ninjas"
collection: "Coding Ninjas"
topic: "Graph Basics"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/4.Graphs-1/cod ninjs q.txt","CODING RESOURCES/coding ninjas/4.Graphs-1/cod ninjs s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Coding Ninjas

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Given a NxM matrix containing Uppercase English Alphabets only. Your task is to tell if there is a path in the given matrix which makes the sentence “CODINGNINJA” .
There is a path from any cell to all its neighbouring cells. A neighbour may share an edge or a corner.

### Input Format

Line 1 : Two space separated integers N  and M, where N is number of rows and M is number of columns in the matrix.
Next N lines : N rows of the matrix. First line of these N line will contain 0th row of matrix, second line will contain 1st row and so on
Assume input to be 0-indexed based

### Output Format

Return 1 if there is a path which makes the sentence “CODINGNINJA” else return 0.

### Constraints

1 <= N <= 100
1 <= M <= 100

### Sample Input

```text
2 11
CXDXNXNXNXA
XOXIXGXIXJX
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

> [!example]- Reference 1 · cod ninjs s.txt
> ```java
>
> public class solution {
> 	
> 	int[][] a = {{-1,-1},{-1,0},{-1,1},{0,-1},{0,1},{1,-1},{1,0},{1,1}};
> 	String pattern = "CODINGNINJA";
> 	int[][] used;
> 	
> 	int validPoint(int x,int y,int N,int M){
> 		
> 		if(x >= 0 && x < N && y >= 0 && y < M)
> 			return 1;
> 		return 0;
> 	}
> 	
> 	int DFS(String[] G,int x, int y, int index, int N, int M){
> 		
> 		if(index == 11)
> 			return 1;
> 		
> 		used[x][y] = 1;
> 		int i, newx, newy;
> 		int found = 0;
> 		for(i = 0; i < 8; i++){
> 			
> 			newx = x + a[i][0];
> 			newy = y + a[i][1];
>
> 			if(validPoint(newx,newy,N,M) == 1 && G[newx].charAt(newy) == pattern.charAt(index) && used[newx][newy] == 0){
> 				found = found | DFS(G,newx,newy,index+1,N,M);
> 			}
> 		}
> 		
> 		used[x][y] = 0;
> 		
> 		return found;
> 	}
>
> 	int solve(String[] Graph , int N, int M)
> 	{
> 		int i,j,found = 0;
> 		
> 		used = new int[N][M];
> 		
> 		for(i = 0;i < N; i++){
> 			for( j = 0 , found = 0; j < M; j++ ){
> 				if(Graph[i].charAt(j)== 'C'){
> 					found = DFS(Graph,i,j,1,N,M);
> 					if(found == 1)
> 						break;
> 				}
> 			}
> 			if(found == 1)
> 				break;
> 		}
>
> 		return found;
>
> 	}
> 	
> 	
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/4.Graphs-1/cod%20ninjs%20q.txt) · CODING RESOURCES/coding ninjas/4.Graphs-1/cod ninjs q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/4.Graphs-1/cod%20ninjs%20s.txt) · CODING RESOURCES/coding ninjas/4.Graphs-1/cod ninjs s.txt
