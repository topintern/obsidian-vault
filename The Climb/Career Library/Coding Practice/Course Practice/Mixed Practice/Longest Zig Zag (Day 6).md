---
kind: "coding-problem"
title: "Longest Zig Zag (Day 6)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day-6-Solutions/LongestZigZag.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Longest Zig Zag (Day 6)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

The longest Zig-Zag subsequence problem is to find length of 
the longest subsequence of given sequence such that all elements of 
this are alternating. 

If a sequence {x1, x2, .. xn} is alternating sequence then its element satisfy 
one of the following relation :
  x1 < x2 > x3 < x4 > x5 < …. xn or 
  x1 > x2 < x3 > x4 < x5 > …. xn 
  

### Sample Input

8
10 22 9 33 49 50 31 60


### Sample Output: 

6


### Explanation

The subsequences {10, 22, 9, 33, 31, 60} or
{10, 22, 9, 49, 31, 60} or {10, 22, 9, 50, 31, 60}
are longest Zig-Zag of length 6.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · LongestZigZag.java
> ```java
> /*
>  * The longest Zig-Zag subsequence problem is to find length of 
>  * the longest subsequence of given sequence such that all elements of 
>  * this are alternating. 
>  * 
>  * If a sequence {x1, x2, .. xn} is alternating sequence then its element satisfy 
>  * one of the following relation :
>   x1 < x2 > x3 < x4 > x5 < …. xn or 
>   x1 > x2 < x3 > x4 < x5 > …. xn 
>   
> Sample Input:
> 8
> 10 22 9 33 49 50 31 60
>
> Sample Output: 
> 6
>
> Explanation:
> The subsequences {10, 22, 9, 33, 31, 60} or
> {10, 22, 9, 49, 31, 60} or {10, 22, 9, 50, 31, 60}
> are longest Zig-Zag of length 6.
>
>
>  */
>
> import java.io.*;
> import java.util.Scanner; 
>
> class LongestZigZag { 
>
> //Function to return longest 
> //Zig-Zag subsequence length 
> static int longestZigZagSubseqLen(int arr[], int n) 
> { 
> 	/*Z[i][0] = Length of the longest 
> 		Zig-Zag subsequence ending at 
> 		index i and last element is 
> 		greater than its previous element 
> 	Z[i][1] = Length of the longest 
> 		Zig-Zag subsequence ending at 
> 		index i and last element is 
> 		smaller than its previous 
> 		element */
> 	int Z[][] = new int[n][2]; 
>
> 	/* Initialize all values from 1 */
> 	for (int i = 0; i < n; i++) 
> 		Z[i][0] = Z[i][1] = 1; 
>
> 	int res = 1; // Initialize result 
>
> 	/* Compute values in bottom up manner */
> 	for (int i = 1; i < n; i++) 
> 	{ 
> 		// Consider all elements as 
> 		// previous of arr[i] 
> 		for (int j = 0; j < i; j++) 
> 		{ 
> 			// If arr[i] is greater, then 
> 			// check with Z[j][1] 
> 			if (arr[j] < arr[i] && 
> 				Z[i][0] < Z[j][1] + 1) 
> 				Z[i][0] = Z[j][1] + 1; 
>
> 			// If arr[i] is smaller, then 
> 			// check with Z[j][0] 
> 			if( arr[j] > arr[i] && 
> 			Z[i][1] < Z[j][0] + 1) 
> 				Z[i][1] = Z[j][0] + 1; 
> 		} 
>
> 		/* Pick maximum of both values at 
> 		index i */
> 		if (res < Math.max(Z[i][0], Z[i][1])) 
> 			res = Math.max(Z[i][0], Z[i][1]); 
> 	}
> 	for(int i=0;i<Z.length;i++)
> 	{
> 	System.out.print(Z[i][0]+" "); 
> 	System.out.println(Z[i][1]);  
> 	
> }
>
> 	return res; 
> } 
>
> /* Main program */
> public static void main(String[] args) 
> { 
> 	Scanner sc = new Scanner(System.in);
> 	int noOfElements = sc.nextInt();
> 	int[] arr  = new int[noOfElements];
> 	for(int i=0;i<noOfElements;i++)
> 		arr[i]=sc.nextInt();
> 	
> 	System.out.println(longestZigZagSubseqLen(arr, noOfElements)); 
> } 
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day-6-Solutions/LongestZigZag.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day-6-Solutions/LongestZigZag.java
