---
kind: "coding-problem"
title: "Print Snake Pattern (Day 39)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 39 Solutions/PrintSnakePattern.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Print Snake Pattern (Day 39)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a matrix of 2-Dimensional array of n rows and n columns. 
Print this matrix in snake fashion starting from column n-1 
as shown in the figure below.


### Sample Input

3
1 2 3 
4 5 6
7 8 9


### Sample Output: 

3 2 1 4 5 6 9 8 7


### Explanation:


1<-2<-3 
|
4->5->6
	  |
7<-8<-9

=====TestCases=======
case =1
input =2
1 2
3 4
output =2 1 3 4

case =2
input =3
10 20 30
15 25 35
20 30 40
output =30 20 10 15 25 35 40 30 20

case =3
input =4
1 4 6 9
2 3 5 8
16 15 14 13
12 10 11 7
output =9 6 4 1 2 3 5 8 13 14 15 16 12 10 11 7

case =4
input =5
5 4 3 2 1
6 7 8 9 10
15 14 13 12 11
16 17 18 19 20
25 24 23 22 21
output =1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25

case =5
input =4
1 2 3 4
2 1 2 3
3 2 1 2
4 3 2 1
output =4 3 2 1 2 1 2 3 2 1 2 3 4 3 2 1

case =6
input =1
5
output =5

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · PrintSnakePattern.txt
> ```java
> /*
>  * 
> Given a matrix of 2-Dimensional array of n rows and n columns. 
> Print this matrix in snake fashion starting from column n-1 
> as shown in the figure below.
>
> Sample Input:
> 3
> 1 2 3 
> 4 5 6
> 7 8 9
>
> Sample Output: 
> 3 2 1 4 5 6 9 8 7
>
> Explanation:
>
> 1<-2<-3 
> |
> 4->5->6
> 	  |
> 7<-8<-9
>
> =====TestCases=======
> case =1
> input =2
> 1 2
> 3 4
> output =2 1 3 4
>
> case =2
> input =3
> 10 20 30
> 15 25 35
> 20 30 40
> output =30 20 10 15 25 35 40 30 20
>
> case =3
> input =4
> 1 4 6 9
> 2 3 5 8
> 16 15 14 13
> 12 10 11 7
> output =9 6 4 1 2 3 5 8 13 14 15 16 12 10 11 7
>
> case =4
> input =5
> 5 4 3 2 1
> 6 7 8 9 10
> 15 14 13 12 11
> 16 17 18 19 20
> 25 24 23 22 21
> output =1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
>
> case =5
> input =4
> 1 2 3 4
> 2 1 2 3
> 3 2 1 2
> 4 3 2 1
> output =4 3 2 1 2 1 2 3 2 1 2 3 4 3 2 1
>
> case =6
> input =1
> 5
> output =5
>
>  * 
>  */
> package Elite2020;
> import java.util.Scanner;
> public class PrintSnakePattern {
>
> 	// Function used for traversing over the given matrix
> 	static void printSnakePattern(int[][] mat, int n) {
>
> 		for (int i = 0; i < n; i++) {
> 			if (i % 2 == 1) {
> 				for (int j = 0; j < n; j++) {
> 					System.out.print(Integer.toString(mat[i][j]) + " ");
> 				}
> 			} else {
> 				for (int j = n - 1; j >= 0; j--) {
> 					System.out.print(Integer.toString(mat[i][j]) + " ");
> 				}
> 			}
> 		}
> 	}
>
> 	// main function
> 	public static void main(String[] args) {
>
> 		Scanner sc = new Scanner(System.in);
> 		
> 		// number of rows and columns
> 		int n = sc.nextInt();
>         int[][] matrix = new int[n][n];
> 		for(int i=0;i<n;i++)
> 		{
> 			for(int j=0;j<n;j++)
> 				matrix[i][j]=sc.nextInt();
> 		}
>
> 		printSnakePattern(matrix, n);
>
> 	}
>
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2039%20Solutions/PrintSnakePattern.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 39 Solutions/PrintSnakePattern.txt
