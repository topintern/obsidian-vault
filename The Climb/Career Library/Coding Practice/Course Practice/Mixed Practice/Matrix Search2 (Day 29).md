---
kind: "coding-problem"
title: "Matrix Search2 (Day 29)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 29 Solutions/MatrixSearch2.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Matrix Search2 (Day 29)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted in ascending from left to right.
Integers in each column are sorted in ascending from top to bottom.
Example:

Consider the following matrix:
5 5
1 4 7 11 15
2 5 8 12 19
3 6 9 16 22
10 13 14 17 24
18 21 23 26 30
5
Given target = 5, return true.

Given target = 20, return false.
-------------------------------------------------------

Approach 4: Search Space Reduction
Intuition

Because the rows and columns of the matrix are sorted (from left-to-right and top-to-bottom, respectively), we can prune \mathcal{O}(m)O(m) or \mathcal{O}(n)O(n) elements when looking at any particular value.

Algorithm

First, we initialize a (row, col)(row,col) pointer to the bottom-left of the matrix.[1] Then, until we find target and return true (or the pointer points to a (row, col)(row,col) that lies outside of the dimensions of the matrix), we do the following: if the currently-pointed-to value is larger than target we can move one row "up". Otherwise, if the currently-pointed-to value is smaller than target, we can move one column "right". It is not too tricky to see why doing this will never prune the correct answer; because the rows are sorted from left-to-right, we know that every value to the right of the current value is larger. Therefore, if the current value is already larger than target, we know that every value to its right will also be too large. A very similar argument can be made for the columns, so this manner of search will always find target in the matrix (if it is present).

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MatrixSearch2.java
> ```java
> /*
>  * 
>  Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:
>
> Integers in each row are sorted in ascending from left to right.
> Integers in each column are sorted in ascending from top to bottom.
> Example:
>
> Consider the following matrix:
> 5 5
> 1 4 7 11 15
> 2 5 8 12 19
> 3 6 9 16 22
> 10 13 14 17 24
> 18 21 23 26 30
> 5
> Given target = 5, return true.
>
> Given target = 20, return false.
> -------------------------------------------------------
>
> Approach 4: Search Space Reduction
> Intuition
>
> Because the rows and columns of the matrix are sorted (from left-to-right and top-to-bottom, respectively), we can prune \mathcal{O}(m)O(m) or \mathcal{O}(n)O(n) elements when looking at any particular value.
>
> Algorithm
>
> First, we initialize a (row, col)(row,col) pointer to the bottom-left of the matrix.[1] Then, until we find target and return true (or the pointer points to a (row, col)(row,col) that lies outside of the dimensions of the matrix), we do the following: if the currently-pointed-to value is larger than target we can move one row "up". Otherwise, if the currently-pointed-to value is smaller than target, we can move one column "right". It is not too tricky to see why doing this will never prune the correct answer; because the rows are sorted from left-to-right, we know that every value to the right of the current value is larger. Therefore, if the current value is already larger than target, we know that every value to its right will also be too large. A very similar argument can be made for the columns, so this manner of search will always find target in the matrix (if it is present).
>
>  */
>
>
> import java.util.Scanner;
>
> public class MatrixSearch2 {
> 	
> 	 public static boolean searchMatrix(int[][] matrix, int target) {
> 	        // start our "pointer" in the bottom-left
> 	        int row = matrix.length-1;
> 	        int col = 0;
>
> 	        while (row >= 0 && col < matrix[0].length) {
> 	            if (matrix[row][col] > target) {
> 	                row--;
> 	            } else if (matrix[row][col] < target) {
> 	                col++;
> 	            } else { // found it
> 	                return true;
> 	            }
> 	        }
>
> 	        return false;
> 	    }
>
> 	 public static void main(String args[] ) {
> 		 Scanner scan = new Scanner(System.in);
> 			int R=scan.nextInt();
> 			int C=scan.nextInt();      
>
> 			int[][] matrix=new int[R][C];
> 		       for(int i=0; i<R; i++)
> 		       {
> 		           for(int j=0; j<C; j++)
> 		           {
> 		        	   matrix[i][j] = scan.nextInt();
> 		           }
> 		       }
> 				int target=scan.nextInt();      
>
> 		       System.out.println(searchMatrix(matrix,target));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2029%20Solutions/MatrixSearch2.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 29 Solutions/MatrixSearch2.java
