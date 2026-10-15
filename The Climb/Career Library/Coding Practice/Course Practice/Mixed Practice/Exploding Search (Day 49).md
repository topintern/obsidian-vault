---
kind: "coding-problem"
title: "Exploding Search (Day 49)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 49 Solutions/ExplodingSearch.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Exploding Search (Day 49)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Magazines and newspapers often have letter matrices in which certain words need to be located. 

Umesh, a puzzle fanatic at IIT Roorkee, had an idea for a new kind of searching puzzle. 
In the letter matrix provided, words can be located along any set of diagonals, 
with repetition of past selected letters.

Given a matrix of size NxN, you need to find out the total number of locations of a particular string.

Input Format:
-------------
Line 1: N. 1 <= N <= 1000
Next N Lines: Elements of the NxN matrix in row major order (separated by a space)
Last Line: The string to search.

Output Format:
--------------
Line 1: The number of ways in which the string can be found in the matrix.



### Sample Input

5
B X A X X
X A X X X
X B B X X
X A X A X
X X B X X
ABA


### Sample Output

14
 

### Explanation

	For example, in the letter matrix:
		B X A X X
		X A X X X
		X B B X X
		X A X A X
		X X B X X


	The string ABA can be found in 14 different ways – corresponding to the following locations:

		  A	  B	  A
		(1,1)	(0,0)	(1,1)
		(1,1)	(2,2)	(3,1)
		(1,1)	(2,2)	(3,3)
		(1,1)	(2,2)	(1,1)
		(3,1)	(2,2)	(3,1)
		(3,1)	(2,2)	(3,3)
		(3,1)	(4,2)	(3,1)
		(3,1)	(4,2)	(3,3)
		(3,1)	(2,2)	(1,1)
		(3,3)	(2,2)	(3,3)
		(3,3)	(2,2)	(1,1)
		(3,3)	(2,2)	(3,1)
		(3,3)	(4,2)	(3,1)
		(3,3)	(4,2)	(3,3)

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ExplodingSearch.java
> ```java
> /*
>  * 
> Magazines and newspapers often have letter matrices in which certain words need to be located. 
>
> Umesh, a puzzle fanatic at IIT Roorkee, had an idea for a new kind of searching puzzle. 
> In the letter matrix provided, words can be located along any set of diagonals, 
> with repetition of past selected letters.
>
> Given a matrix of size NxN, you need to find out the total number of locations of a particular string.
>
> Input Format:
> -------------
> Line 1: N. 1 <= N <= 1000
> Next N Lines: Elements of the NxN matrix in row major order (separated by a space)
> Last Line: The string to search.
>
> Output Format:
> --------------
> Line 1: The number of ways in which the string can be found in the matrix.
>
>
> Sample Input:
> 5
> B X A X X
> X A X X X
> X B B X X
> X A X A X
> X X B X X
> ABA
>
> Sample Output:
> 14
>  
> Explanation:
> 	For example, in the letter matrix:
> 		B X A X X
> 		X A X X X
> 		X B B X X
> 		X A X A X
> 		X X B X X
>
>
> 	The string ABA can be found in 14 different ways – corresponding to the following locations:
>
> 		  A	  B	  A
> 		(1,1)	(0,0)	(1,1)
> 		(1,1)	(2,2)	(3,1)
> 		(1,1)	(2,2)	(3,3)
> 		(1,1)	(2,2)	(1,1)
> 		(3,1)	(2,2)	(3,1)
> 		(3,1)	(2,2)	(3,3)
> 		(3,1)	(4,2)	(3,1)
> 		(3,1)	(4,2)	(3,3)
> 		(3,1)	(2,2)	(1,1)
> 		(3,3)	(2,2)	(3,3)
> 		(3,3)	(2,2)	(1,1)
> 		(3,3)	(2,2)	(3,1)
> 		(3,3)	(4,2)	(3,1)
> 		(3,3)	(4,2)	(3,3)
>
>  */
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
>
> class ExplodingSearch {
> 	private static char[][] matrix;
> 	private static char[] searchString;
> 	private static int N;
> 	public static void main(String[] args) throws NumberFormatException, IOException {
> 		BufferedReader input = new BufferedReader(new InputStreamReader(System.in));
> 		N = Integer.parseInt(input.readLine());
> 		matrix = new char[N][];
> 		
> 		for (int row = 0; row < matrix.length; row++) matrix[row] = input.readLine().replace(" ", "").toCharArray();
> 		searchString = input.readLine().toCharArray();
> 		
> 		System.out.println(numWays());
>
> 	}
> 	
> 	public static  int numWays(){
> 		int total = 0;
> 		
> 		for (int row = 0; row < N; row++)
> 			for (int col = 0; col < N; col ++) {
> 				if (matrix[row][col]==searchString[0]) {
> 					int tottem=search(row,col,0);
> 					total+=tottem;
> 				}
> 			}
> 		
> 		return total;
> 	}
> 	
> public static int search(int row, int col, int index){
> 		
> 		
> 		//if entire string is found return 1
> 		if (index == searchString.length - 1) return 1;
> 		int total = 0;
> 		
> 		if (validCoordinate(row+1,col+1) && matrix[row+1][col+1]== searchString[index+1]) total+=search(row+1,col+1,index+1);
> 		if (validCoordinate(row+1,col-1) && matrix[row+1][col-1]== searchString[index+1]) total+=search(row+1,col-1,index+1);
> 		if (validCoordinate(row-1,col+1) && matrix[row-1][col+1]== searchString[index+1]) total+=search(row-1,col+1,index+1);
> 		if (validCoordinate(row-1,col-1) && matrix[row-1][col-1]== searchString[index+1]) total+=search(row-1,col-1,index+1);
> 		
> 		return total;
> 	}
> 	
> 	public static boolean validCoordinate(int r, int c){
> 		return r >= 0 && c >= 0 && r < N && c < N;
> 	}
> }
>
> /*
> ====== Testcases Program-3 ======
> case = 1
> input =5
> X X A X X
> X A X B X
> X B B X A
> X A X A X
> X X B X X
> ABA
> output =17
>
> case = 2
> input =5
> B X A X X
> X A X X X
> X B B X B
> X A X A X
> X X B X X
> ABA
> output =15
>
> case = 3
> input =5
> B X A X X
> X A X X X
> X B B X B
> X A X A X
> X X B X X
> ABAB
> output =36
>
> case =4
> input =5
> B X A X X
> X A X X X
> X B B X X
> X A X A X
> X X B X X
> ABA
> output =14
>
> case =5
> input =6
> B X A B X X
> X A X A X X
> X B B X X A
> X A X A B X
> X X B X X A
> X X B A B X
> ABAB
> output =53
>
> case =6
> input =6
> X A X A B X
> X X B X X A
> X X B A B X
> X A X A X X
> X B B X X A
> X A X A B X
> ABA
> output =35
>
> case =7
> input =6
> X X B X X A
> X A X A B X
> X X B A B X
> X B B X X A
> X A X A B X
> X X B X X A
> BAB
> output =31
>
> case =8
> input =7
> X A A X B X X
> X B X X A B X
> X X X X X X X
> X A X B A X B
> X B X A X B X
> X X X B A B X 
> X B X A A B A
> ABB
> output =2
>
> case =9
> input =7
> X A B X B A X
> X X A B A X X
> X X X A X X X
> X X A B A X X
> X A B X B A X
> X A B A B A X
> X A X B X A X
> ABA
> output =16
>
> case =10
> input =7
> X X X A X X X
> X A X B X A X
> X A B A B A X
> X X A B A X X
> X A B A B A X
> X X A B A X X
> X A X B X A X
> ABB
> output =4
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2049%20Solutions/ExplodingSearch.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 49 Solutions/ExplodingSearch.java
