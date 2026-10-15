---
kind: "coding-problem"
title: "Longest Increasing Path (Day 28)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 28 Solutions/LongestIncreasingPath.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Longest Increasing Path (Day 28)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given an integer matrix, find the length of the longest increasing path.

From each cell, you can either move to four directions: left, right, up or down. 
You may NOT move diagonally or move outside of the boundary 

Example 1:
	Input: 3
		9 9 4
		6 6 8
		2 1 1
	Output: 4 
	Explanation: The longest increasing path is [1, 2, 6, 9].

Example 2:
	Input: nums = 3
			3 4 5
			3 2 6
			2 2 1
	Output: 4 
	Explanation: The longest increasing path is [3, 4, 5, 6]. 
	Moving diagonally is not allowed.

-----------TestCases-----------
case =1
input =5
2 6 3 8 2
1 3 1 4 3
4 2 6 4 7
8 3 5 7 1
3 5 2 6 1
output =4

case =2
input =5
1 1 1 1 1 
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
output =1

case =3
input =5
1 1 1 1 1 
1 2 3 1 1
9 1 4 5 1
1 1 7 6 1
11 1 8 1 10
output =8

case =4
input =3
1 2 3
6 5 4
7 8 9
output =9

case =5
input =4
1 2 3 1
4 5 6 4
9 8 7 10
2 3 4 2
output =7

case =6
input =4
1 3 5 7
2 3 4 5
5 3 4 7
4 2 1 5
output =6

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · LongestIncreasingPath.java
> ```java
> /*
> Given an integer matrix, find the length of the longest increasing path.
>
> From each cell, you can either move to four directions: left, right, up or down. 
> You may NOT move diagonally or move outside of the boundary 
>
> Example 1:
> 	Input: 3
> 		9 9 4
> 		6 6 8
> 		2 1 1
> 	Output: 4 
> 	Explanation: The longest increasing path is [1, 2, 6, 9].
>
> Example 2:
> 	Input: nums = 3
> 			3 4 5
> 			3 2 6
> 			2 2 1
> 	Output: 4 
> 	Explanation: The longest increasing path is [3, 4, 5, 6]. 
> 	Moving diagonally is not allowed.
>
> -----------TestCases-----------
> case =1
> input =5
> 2 6 3 8 2
> 1 3 1 4 3
> 4 2 6 4 7
> 8 3 5 7 1
> 3 5 2 6 1
> output =4
>
> case =2
> input =5
> 1 1 1 1 1 
> 1 1 1 1 1
> 1 1 1 1 1
> 1 1 1 1 1
> 1 1 1 1 1
> output =1
>
> case =3
> input =5
> 1 1 1 1 1 
> 1 2 3 1 1
> 9 1 4 5 1
> 1 1 7 6 1
> 11 1 8 1 10
> output =8
>
> case =4
> input =3
> 1 2 3
> 6 5 4
> 7 8 9
> output =9
>
> case =5
> input =4
> 1 2 3 1
> 4 5 6 4
> 9 8 7 10
> 2 3 4 2
> output =7
>
> case =6
> input =4
> 1 3 5 7
> 2 3 4 5
> 5 3 4 7
> 4 2 1 5
> output =6
> */
> import java.util.*;
> class LongestIncreasingPath
> {
>     private static final int[][] dir = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
>     private static int m, n;
>     public static int longestIncreasingPath(int[][] grid) {
>         int m = grid.length;
>         if (m == 0) return 0;
>         int n = grid[0].length;
>         // padding the matrix with zero as boundaries
>         // assuming all positive integer, otherwise use INT_MIN as boundaries
>         int[][] matrix = new int[m + 2][n + 2];
>         for (int i = 0; i < m; ++i)
>             System.arraycopy(grid[i], 0, matrix[i + 1], 1, n);
>
>         // calculate outdegrees
>         int[][] outdegree = new int[m + 2][n + 2];
>         for (int i = 1; i <= m; ++i)
>             for (int j = 1; j <= n; ++j)
>                 for (int[] d: dir)
>                     if (matrix[i][j] < matrix[i + d[0]][j + d[1]])
>                         outdegree[i][j]++;
>
>         // find leaves who have zero out degree as the initial level
>         n += 2;
>         m += 2;
>         List<int[]> leaves = new ArrayList<>();
>         for (int i = 1; i < m - 1; ++i)
>             for (int j = 1; j < n - 1; ++j)
>                 if (outdegree[i][j] == 0) leaves.add(new int[]{i, j});
>
>         // remove leaves level by level in topological order
>         int height = 0;
>         while (!leaves.isEmpty()) {
>             height++;
>             List<int[]> newLeaves = new ArrayList<>();
>             for (int[] node : leaves) {
>                 for (int[] d:dir) {
>                     int x = node[0] + d[0], y = node[1] + d[1];
>                     if (matrix[node[0]][node[1]] > matrix[x][y])
>                         if (--outdegree[x][y] == 0)
>                             newLeaves.add(new int[]{x, y});
>                 }
>             }
>             leaves = newLeaves;
>         }
>         return height;
>     }
> 	public static void main(String args[])
> 	{
> 		Scanner scan=new Scanner(System.in);
> 		int n=scan.nextInt();
> 		int[][] grid=new int[n][n];
> 		for(int i=0;i<n;i++)
> 			for(int j=0;j<n;j++)
> 				grid[i][j]=scan.nextInt();
> 		System.out.println(longestIncreasingPath(grid));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2028%20Solutions/LongestIncreasingPath.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 28 Solutions/LongestIncreasingPath.java
