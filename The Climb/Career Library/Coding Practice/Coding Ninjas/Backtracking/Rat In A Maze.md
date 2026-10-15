---
kind: "coding-problem"
title: "Rat In A Maze"
collection: "Coding Ninjas"
topic: "Backtracking"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/2.backtrack/rat in maze q.txt","CODING RESOURCES/coding ninjas/2.backtrack/rat in maze s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Rat In A Maze

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

You are given a N*N maze with a rat placed at maze[0][0]. Find and print all paths that rat can follow to reach its destination i.e. maze[N-1][N-1]. Rat can move in any direc­tion ( left, right, up and down).
Value of every cell in the maze can either be 0 or 1. Cells with value 0 are blocked means rat can­not enter into those cells and those with value 1 are open.

### Input Format

Line 1 : Integer N
Next N Lines : Each line will contain ith row elements (separated by space)

### Output Format

One Line for every possible solution. 
Every line will have N*N maze elements printed row wise and are separated by space. Only cells that are part of solution path should be 1, rest all cells should be 0.

### Sample Input 1

```text
3
1 0 1
1 0 1
1 1 1
```

### Sample Output 1

```text
1 0 0 1 0 0 1 1 1 
Sample Output 1 Explanation :
Only 1 path is possible
```

### Sample Input 2

```text
3
1 0 1
1 1 1
1 1 1
```

### Sample Output 2

```text
1 0 0 1 1 1 1 1 1 
1 0 0 1 0 0 1 1 1 
1 0 0 1 1 0 0 1 1 
1 0 0 1 1 1 0 0 1 
Sample Output 2 Explanation :
4 paths are possible
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · rat in maze s.txt
> ```text
> ## Read input as specified in the question.
> ## Print output as specified in the question.
> def ratInAMaze(maze , n):
>     solution = [[0 for j in range(n)] for i in range(n)]
>     solveMaze(maze, solution, 0, 0 , n)
>
> def solveMaze(maze, solution, x, y , n):
>     if(x == n - 1 and y == n - 1):
>         solution[x][y] = 1
>         printSolution(solution , n)
>         print("")
>         return
>     if (x > n-1 or x < 0 or y > n - 1 or y < 0):
>       	return
>     if(x > n-1 or x < 0 or y > n - 1 or y < 0 or  maze[x][y] == 0 or solution[x][y] == 1):
>         return
> 		
>     solution[x][y] = 1
>     solveMaze(maze, solution, x - 1, y , n)
>     solveMaze(maze, solution, x + 1, y , n)
>     solveMaze(maze, solution, x , y - 1 , n)
>     solveMaze(maze, solution, x, y + 1 , n)
>     solution[x][y] = 0
> 	
> def printSolution(solution , n):
>     for i in range(0 , n):
>         for j  in range(0 , n):
>             print(solution[i][j] , end = " ")
>
> n = int(input())
> maze = n*[0]
> for i in range(0 , n):
> 	maze[i]=input().split() 
> 	maze[i]=[int(j) for j in maze[i]]
> ratInAMaze(maze , n)
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/2.backtrack/rat%20in%20maze%20q.txt) · CODING RESOURCES/coding ninjas/2.backtrack/rat in maze q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/2.backtrack/rat%20in%20maze%20s.txt) · CODING RESOURCES/coding ninjas/2.backtrack/rat in maze s.txt
