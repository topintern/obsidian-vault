---
kind: "coding-problem"
title: "Print Diagonal Pattern (Day 44)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 44 Solutions/PrintDiagonalPattern.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Print Diagonal Pattern (Day 44)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a matrix of m*n size, 
the task is to print its elements in diagonally pattern.


### Sample Input

3 3
1 2 3 
4 5 6
7 8 9


### Sample Output: 

1 2 4 7 5 3 6 8 9


### Explanation:


1-2 3 
 / /|
4 5 6
|/ /	  
7 8-9



=======TestCases==========
----------TestCases-----------
case =1
input =2 2
1 2
3 4
output =1 2 3 4

case =2
input =3 3
1 2 6
3 5 7
4 8 9
output =1 2 3 4 5 6 7 8 9

case =3
input =2 4
5 6 3 2
1 4 5 1
output =5 6 1 4 3 2 5 1

case =4
input =4 3
1 2 3
4 5 6
7 8 9
10 11 12
output =1 2 4 7 5 3 6 8 10 11 9 12

case =5
input =4 4
4 3 2 1
8 7 6 5
5 6 7 8
1 2 3 4
output =4 3 8 5 7 2 1 6 6 1 2 7 5 8 3 4

case =6
input =3 5
6 5 4 3 2
7 4 3 2 8
3 2 1 4 5
output =6 5 7 3 4 4 3 3 2 1 2 2 8 4 5

case =7
input =4 1
1 
2 
3 
4
output =1 2 3 4

case =8
input =5 3
6 7 3
5 4 2
4 3 1
3 2 4
2 8 5
output =6 7 5 4 4 3 2 3 3 2 2 1 4 8 5

case =9
input =4 2
5 1
6 4
3 5
2 1
output =5 1 6 3 4 5 2 1

case =10
input =5 5 
1 2 6 7 15
3 5 8 14 16
4 9 13 17 22
10 12 18 21 23
11 19 20 24 25
output =1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25

case =11
input =5 0
output=-1

case =12
input =5 -5
output=-1

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · PrintDiagonalPattern.java
> ```java
> /*
>  * 
> Given a matrix of m*n size, 
> the task is to print its elements in diagonally pattern.
>
> Sample Input:
> 3 3
> 1 2 3 
> 4 5 6
> 7 8 9
>
> Sample Output: 
> 1 2 4 7 5 3 6 8 9
>
> Explanation:
>
> 1-2 3 
>  / /|
> 4 5 6
> |/ /	  
> 7 8-9
>
>
>
> =======TestCases==========
> ----------TestCases-----------
> case =1
> input =2 2
> 1 2
> 3 4
> output =1 2 3 4
>
> case =2
> input =3 3
> 1 2 6
> 3 5 7
> 4 8 9
> output =1 2 3 4 5 6 7 8 9
>
> case =3
> input =2 4
> 5 6 3 2
> 1 4 5 1
> output =5 6 1 4 3 2 5 1
>
> case =4
> input =4 3
> 1 2 3
> 4 5 6
> 7 8 9
> 10 11 12
> output =1 2 4 7 5 3 6 8 10 11 9 12
>
> case =5
> input =4 4
> 4 3 2 1
> 8 7 6 5
> 5 6 7 8
> 1 2 3 4
> output =4 3 8 5 7 2 1 6 6 1 2 7 5 8 3 4
>
> case =6
> input =3 5
> 6 5 4 3 2
> 7 4 3 2 8
> 3 2 1 4 5
> output =6 5 7 3 4 4 3 3 2 1 2 2 8 4 5
>
> case =7
> input =4 1
> 1 
> 2 
> 3 
> 4
> output =1 2 3 4
>
> case =8
> input =5 3
> 6 7 3
> 5 4 2
> 4 3 1
> 3 2 4
> 2 8 5
> output =6 7 5 4 4 3 2 3 3 2 2 1 4 8 5
>
> case =9
> input =4 2
> 5 1
> 6 4
> 3 5
> 2 1
> output =5 1 6 3 4 5 2 1
>
> case =10
> input =5 5 
> 1 2 6 7 15
> 3 5 8 14 16
> 4 9 13 17 22
> 10 12 18 21 23
> 11 19 20 24 25
> output =1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
>
> case =11
> input =5 0
> output=-1
>
> case =12
> input =5 -5
> output=-1
>  
>  * 
>  */
>  
> import java.util.Arrays;
> import java.util.Scanner;
>
> public class PrintDiagonalPattern {
>
> 	 public static int[] findDiagonalOrder(int[][] matrix) {
> 	        if (matrix.length == 0) return new int[0];
> 	        int r = 0, c = 0, m = matrix.length, n = matrix[0].length, arr[] = new int[m * n];
> 	        for (int i = 0; i < arr.length; i++) {
> 	            arr[i] = matrix[r][c];
> 	            if ((r + c) % 2 == 0) { // moving up
> 	                if      (c == n - 1) { r++; }
> 	                else if (r == 0)     { c++; }
> 	                else            { r--; c++; }
> 	            } else {                // moving down
> 	                if      (r == m - 1) { c++; }
> 	                else if (c == 0)     { r++; }
> 	                else            { r++; c--; }
> 	            }   
> 	        }   
> 	        return arr;
> 	    }
>
> 	// main function
> 	public static void main(String[] args) {
>
> 		Scanner sc = new Scanner(System.in);
>
> 		// number of rows and columns
> 		int m = sc.nextInt();
> 		int n = sc.nextInt();
>
> 		int[][] matrix = new int[m][n];
> 		for (int i = 0; i < m; i++) {
> 			for (int j = 0; j < n; j++)
> 				matrix[i][j] = sc.nextInt();
> 		}
> 		System.out.println(Arrays.toString(findDiagonalOrder(matrix)));
>
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2044%20Solutions/PrintDiagonalPattern.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 44 Solutions/PrintDiagonalPattern.java
