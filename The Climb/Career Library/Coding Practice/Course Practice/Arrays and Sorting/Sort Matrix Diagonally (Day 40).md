---
kind: "coding-problem"
title: "Sort Matrix Diagonally (Day 40)"
collection: "Course Practice"
topic: "Arrays and Sorting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 40 Solutions/SortMatrixDiagonally.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Sort Matrix Diagonally (Day 40)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a m * n matrix mat of integers, sort it diagonally in ascending order from the top-left to the bottom-right then return the sorted array.

 

Example 1:


Input:3 4
3 3 1 1
2 2 1 2
1 1 1 2
Output: 
1 1 1 1
1 2 2 2
1 2 3 3

==========================================================

Explanation
A[i][j] on the same diagonal have same value of i - j
For each diagonal,
put its elements together, sort, and set them back.


Complexity
Time O(MNlogD), where D is the length of diagonal with D = min(M,N).
Space O(MN)



----------------------------------------------------


case=1
input=3 4
3 3 1 1
2 2 1 2
1 1 1 2
output=1 1 1 1
1 2 2 2
1 2 3 3


case=2
input=5 4
3 3 1 1
2 2 1 2
1 1 1 2
3 3 1 1
2 2 1 2
output=1 1 1 1 
1 1 2 2 
1 1 2 3 
2 1 2 3 
2 3 3 2

case=3
input=5 5
5 4 3 2 1
4 5 6 7 8
9 8 7 4 5
1 5 9 3 6
8 5 2 3 7
output=3 4 3 2 1 
3 5 4 5 8 
2 4 5 6 7 
1 5 8 7 6 
8 5 9 9 7

case=4
input=6 6
5 4 3 2 1 9
4 5 6 7 8 7
9 8 7 4 5 6
1 5 9 3 6 7
8 5 2 3 7 4
9 8 7 4 5 6
output=3 4 3 2 1 9 
3 5 4 5 6 7 
2 4 5 4 7 8 
1 4 5 6 6 7 
8 5 5 8 7 6 
9 8 7 9 9 7


case=5
input=6 4
3 3 1 1
2 2 1 2
1 1 1 2
3 3 1 1
2 2 1 2
1 1 1 2
output=1 1 1 1 
1 1 2 2 
1 1 2 3 
1 1 2 3 
1 2 2 2 
1 2 3 3


case=6
input=3 6
9 8 7 4 5 6
1 5 9 3 6 7
8 5 2 3 7 4
output=2 3 3 4 5 6 
1 5 8 7 4 7 
8 5 9 9 7 6

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SortMatrixDiagonally.java
> ```java
> /*
>  * 
>  Given a m * n matrix mat of integers, sort it diagonally in ascending order from the top-left to the bottom-right then return the sorted array.
>
>  
>
> Example 1:
>
>
> Input:3 4
> 3 3 1 1
> 2 2 1 2
> 1 1 1 2
> Output: 
> 1 1 1 1
> 1 2 2 2
> 1 2 3 3
>
> ==========================================================
>
> Explanation
> A[i][j] on the same diagonal have same value of i - j
> For each diagonal,
> put its elements together, sort, and set them back.
>
>
> Complexity
> Time O(MNlogD), where D is the length of diagonal with D = min(M,N).
> Space O(MN)
>
>
>
> ----------------------------------------------------
>
>
> case=1
> input=3 4
> 3 3 1 1
> 2 2 1 2
> 1 1 1 2
> output=1 1 1 1
> 1 2 2 2
> 1 2 3 3
>
>
> case=2
> input=5 4
> 3 3 1 1
> 2 2 1 2
> 1 1 1 2
> 3 3 1 1
> 2 2 1 2
> output=1 1 1 1 
> 1 1 2 2 
> 1 1 2 3 
> 2 1 2 3 
> 2 3 3 2
>
> case=3
> input=5 5
> 5 4 3 2 1
> 4 5 6 7 8
> 9 8 7 4 5
> 1 5 9 3 6
> 8 5 2 3 7
> output=3 4 3 2 1 
> 3 5 4 5 8 
> 2 4 5 6 7 
> 1 5 8 7 6 
> 8 5 9 9 7
>
> case=4
> input=6 6
> 5 4 3 2 1 9
> 4 5 6 7 8 7
> 9 8 7 4 5 6
> 1 5 9 3 6 7
> 8 5 2 3 7 4
> 9 8 7 4 5 6
> output=3 4 3 2 1 9 
> 3 5 4 5 6 7 
> 2 4 5 4 7 8 
> 1 4 5 6 6 7 
> 8 5 5 8 7 6 
> 9 8 7 9 9 7
>
>
> case=5
> input=6 4
> 3 3 1 1
> 2 2 1 2
> 1 1 1 2
> 3 3 1 1
> 2 2 1 2
> 1 1 1 2
> output=1 1 1 1 
> 1 1 2 2 
> 1 1 2 3 
> 1 1 2 3 
> 1 2 2 2 
> 1 2 3 3
>
>
> case=6
> input=3 6
> 9 8 7 4 5 6
> 1 5 9 3 6 7
> 8 5 2 3 7 4
> output=2 3 3 4 5 6 
> 1 5 8 7 4 7 
> 8 5 9 9 7 6
>
>  */
>
>
>
> import java.util.*;
>
> public class SortMatrixDiagonally {
>
> 	public static int[][] diagonalSort(int[][] A) {
>         int m = A.length, n = A[0].length;
>         HashMap<Integer, PriorityQueue<Integer>> d = new HashMap<>();
>         for (int i = 0; i < m; ++i) {
>             for (int j = 0; j < n; ++j) {
>                 d.putIfAbsent(i - j, new PriorityQueue<>());
>                 d.get(i - j).add(A[i][j]);
>             }
>         }
>         for (int i = 0; i < m; ++i)
>             for (int j = 0; j < n; ++j)
>                 A[i][j] = d.get(i - j).poll();
>         return A;
>     }
> 	
> 	public static void main(String args[] ) {
> 		 Scanner scan = new Scanner(System.in);
> 			int R=scan.nextInt();
> 			int C=scan.nextInt();      
>
> 			int[][] A=new int[R][C];
> 		       for(int i=0; i<R; i++)
> 		       {
> 		           for(int j=0; j<C; j++)
> 		           {
> 		        	   A[i][j] = scan.nextInt();
> 		           }
> 		       }
> 		       int[][] res=diagonalSort(A);
> 		       
> 		       
> 		       for(int i=0; i<R; i++)
> 		       {
> 		           for(int j=0; j<C; j++)
> 		           {
> 		        	   System.out.print(res[i][j]+" ");
> 		           }
> 		           System.out.println();
> 		       }
> 	}
>
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2040%20Solutions/SortMatrixDiagonally.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 40 Solutions/SortMatrixDiagonally.java
