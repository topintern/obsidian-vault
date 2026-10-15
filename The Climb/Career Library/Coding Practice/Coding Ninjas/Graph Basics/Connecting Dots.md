---
kind: "coding-problem"
title: "Connecting Dots"
collection: "Coding Ninjas"
topic: "Graph Basics"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/4.Graphs-1/connect dots q.txt","CODING RESOURCES/coding ninjas/4.Graphs-1/connect dots s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Connecting Dots

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Gary has a board of size NxM. Each cell in the board is a coloured dot. There exist only 26 colours denoted by uppercase Latin characters (i.e. A,B,...,Z). Now Gary is getting bore and wants to play a game. The key of this game is to find a cycle that contain dots of same colour. Formally, we call a sequence of dots d1,?d2,?...,?dk a cycle if and only if it meets the following condition:
1. These k dots are different: if i???j then di is different from dj.
2. k is at least 4.
3. All dots belong to the same colour.
4. For all 1?=?i?=?k?-?1: di and di?+?1 are adjacent. Also, dk and d1 should also be adjacent. Cells x and y are called adjacent if they share an edge.
Since Gary is colour blind, he wants your help. Your task is to determine if there exists a cycle on the board.
Assume input to be 0-indexed based.

### Input Format

Line 1 : Two integers N and M, the number of rows and columns of the board
Next N lines : a string consisting of M characters, expressing colors of dots in each line. Each character is an uppercase Latin letter.

### Output Format

Return 1 if there is a cycle else return 0

### Constraints

2?=?N,?M?=?50

### Sample Input

```text
3 4
AAAA
ABCA
AAAA
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

> [!example]- Reference 1 · connect dots s.txt
> ```java
> import java.util.*;
>
> public class solution {
> 	
> 	int[] dx = {1, -1, 0, 0};
> 	int[] dy = {0, 0, 1, -1};
> 	int[][] visited;
> 	int findCycle = 0;
> 	
> 	void dfs(String[] board, int x, int y, int fromX, int fromY, char needColor, int n, int m)
> 	{
> 		if(x < 0 || x >= n || y < 0 || y >= m) return;
> 		if(board[x].charAt(y) != needColor) return;
> 		if(visited[x][y] == 1)
> 		{
> 			findCycle = 1;
> 			return;
> 		}
> 		visited[x][y] = 1;
> 		for(int f = 0; f < 4; f++)
> 		{
> 			int nextX = x + dx[f];
> 			int nextY = y + dy[f];
> 			if(nextX == fromX && nextY == fromY) continue;
> 			dfs(board, nextX, nextY, x, y, needColor, n, m);
> 		}
> 	}
>
> 	int solve(String[] board , int n, int m)
> 	{
> 		
> 		visited = new int[n][m];
>
> 		for(int i = 0; i < n ; i++)
> 			Arrays.fill(visited[i],0);
> 		
> 		for(int i = 0; i < n; i++)
> 			for(int j = 0; j < m; j++)
> 				if(visited[i][j] == 0)
> 					dfs(board,i, j, -1, -1, board[i].charAt(j), n, m);
> 		
> 		return findCycle;
> 	}
> 	
> 	
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/4.Graphs-1/connect%20dots%20q.txt) · CODING RESOURCES/coding ninjas/4.Graphs-1/connect dots q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/4.Graphs-1/connect%20dots%20s.txt) · CODING RESOURCES/coding ninjas/4.Graphs-1/connect dots s.txt
