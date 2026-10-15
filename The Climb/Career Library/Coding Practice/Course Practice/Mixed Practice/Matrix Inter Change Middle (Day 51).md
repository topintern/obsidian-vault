---
kind: "coding-problem"
title: "Matrix Inter Change Middle (Day 51)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 51 Solutions/MatrixInterChangeMiddle.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Matrix Inter Change Middle (Day 51)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Write a program to interchange the middle row and middle column  elements of a matrix .
Accept the number of rows and columns of the matrix from the user
if the matrix is not a square matrix print -1.
assume it is odd dimensions matrix. 


### Sample input

5 5
1 2 3 4 5
6 7 8 9 10
11 12 13 14 15
16 17 18 19 20
21 22 23 24 25


### Sample Output

1 2 11 4 5 
6 7 12 9 10 
3 8 13 18 23 
16 17 14 19 20 
21 22 15 24 25

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MatrixInterChangeMiddle.java
> ```java
> /*
>  * 
> Write a program to interchange the middle row and middle column  elements of a matrix .
> Accept the number of rows and columns of the matrix from the user
> if the matrix is not a square matrix print -1.
> *assume it is odd dimensions matrix. 
>
> Sample input:
> 5 5
> 1 2 3 4 5
> 6 7 8 9 10
> 11 12 13 14 15
> 16 17 18 19 20
> 21 22 23 24 25
>
> Sample Output:
> 1 2 11 4 5 
> 6 7 12 9 10 
> 3 8 13 18 23 
> 16 17 14 19 20 
> 21 22 15 24 25 
>
>  * 
>  * 
>  */
> import java.util.Scanner;
>
> public class MatrixInterChangeMiddle {
>
> 	static void matrixInterChangeMiddle(int mat[][], int n) {
>
> 		// interchange the col and row
> 		for (int i = 0; i < n; i++) {
> 			int temp = mat[n / 2][i];
> 			mat[n / 2][i] = mat[i][n / 2];
> 			mat[i][n / 2] = temp;
> 		}
>
> 		// display matrix
> 		for (int i = 0; i < n; i++) {
> 			for (int j = 0; j < n; j++) {
> 				System.out.print(mat[i][j] + " ");
> 			}
> 			System.out.println("");
> 		}
>
> 	}
>
> 	// main function
> 	public static void main(String[] args) {
>
> 		Scanner sc = new Scanner(System.in);
>
> 		// number of odd rows and odd columns
> 		int nrows = sc.nextInt();
> 		int ncols = sc.nextInt();
> 		
> 		int[][] matrix = new int[nrows][ncols];
> 		for (int i = 0; i < nrows; i++) {
> 			for (int j = 0; j < ncols; j++)
> 				matrix[i][j] = sc.nextInt();
> 		}
> 		if(nrows==ncols)
> 			matrixInterChangeMiddle(matrix, nrows);
> 		else
> 			System.out.println("-1");
>
> 	}
> }
>
> /*
> ===== testcases program-2 ======
> case=1
> input=3 3
> 3 4 5
> 8 9 10
> 13 14 15
> output=3 8 5 
> 4 9 14 
> 13 10 15
>
>
> case=2
> input=7 7
> 6 7 1 2 3 4 5
> 11 12 6 7 8 9 10
> 16 17 11 12 13 14 15
> 21 22 16 17 18 19 20
> 26 27 21 22 23 24 25
> 28 29 30 31 32 33 34
> 35 36 37 38 39 40 41
> output=6 7 1 21 3 4 5 
> 11 12 6 22 8 9 10 
> 16 17 11 16 13 14 15 
> 2 7 12 17 22 31 38 
> 26 27 21 18 23 24 25 
> 28 29 30 19 32 33 34 
> 35 36 37 20 39 40 41 
>
> case=3
> input=3 2
> 3 4
> 8 9
> 13 14
> output=-1
>
> case=4
> input=5 5
> 42 71 94 29 94
> 43 16 76 34 61
> 26 63 45 56 67
> 55 19 42 49 17
> 99 65 78 34 53
> output=42 71 26 29 94
> 43 16 63 34 61
> 94 76 45 42 78
> 55 19 56 49 17
> 99 65 67 34 53
>
> case=5
> input=3 3
> 13 67 80
> 80 73 18
> 43 46 43
> output=13 80 80
> 67 73 46
> 43 18 43
>
> case=6
> input=1 1
> 54
> output=54
>
> case=7
> input=7 7
> 29 60 17 95 51 77 19
> 90 30 28 24 88 13 72
> 87 38 57 19 42 44 73
> 57 73 46 69 38 46 31
> 17 58 37 74 30 42 58
> 19 58 22 80 37 91 87
> 78 20 96 88 66 50 37
> output=29 60 17 57 51 77 19
> 90 30 28 73 88 13 72
> 87 38 57 46 42 44 73
> 95 24 19 69 74 80 88
> 17 58 37 38 30 42 58
> 19 58 22 46 37 91 87
> 78 20 96 31 66 50 37
>
> case=8
> input=5 5
> 94 49 12 59 42
> 18 51 90 73 74
> 85 71 22 46 74
> 32 76 41 29 66
> 43 10 60 18 77
> output=94 49 85 59 42
> 18 51 71 73 74
> 12 90 22 41 60
> 32 76 46 29 66
> 43 10 74 18 77
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2051%20Solutions/MatrixInterChangeMiddle.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 51 Solutions/MatrixInterChangeMiddle.java
