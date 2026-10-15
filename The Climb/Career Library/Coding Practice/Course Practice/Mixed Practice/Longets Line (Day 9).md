---
kind: "coding-problem"
title: "Longets Line (Day 9)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 9 Solutions/LongetsLine.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Longets Line (Day 9)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a 01 matrix M, find the longest line of consecutive one in the matrix. The line could be horizontal, vertical, diagonal or anti-diagonal.

Example:
Input:3 3
0 1 1 0
0 1 1 0
0 0 0 1
Output: 3

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · LongetsLine.java
> ```java
> /*
>  * 
>  * 
> Given a 01 matrix M, find the longest line of consecutive one in the matrix. The line could be horizontal, vertical, diagonal or anti-diagonal.
>
> Example:
> Input:3 3
> 0 1 1 0
> 0 1 1 0
> 0 0 0 1
> Output: 3
>
>
>
>  */
>
> package Leetcode;
>
> import java.util.Scanner;
>
> public class LongetsLine {
>
> 	public static int longestLine(int [][] M) {
> 		if(M==null || M.length==0)return 0;
> 		int rows=M.length,cols=M[0].length;
> 		int [][][] dp=new int[rows+1][cols+2][4];
> 		int res=0;
> 		for(int i=0;i<rows;i++) {
> 			for(int j=0;j<cols;j++) {
> 				if(M[i][j]==1) {
> 					//Horizantal
> 					dp[i+1][j+1][0]=dp[i+1][j][0]+1;
> 					res=Math.max(res,dp[i+1][j+1][0]);
> 					
> 					//vertical
> 					dp[i+1][j+1][1]=dp[i][j+1][1]+1;
> 					res=Math.max(res,dp[i+1][j+1][1]);
> 					
> 					//diagonal
> 					dp[i+1][j+1][2]=dp[i][j][2]+1;
> 					res=Math.max(res,dp[i+1][j+1][2]);
> 					
> 					//anti diagonal
> 					dp[i+1][j+1][3]=dp[i][j+2][3]+1;
> 					res=Math.max(res,dp[i+1][j+1][3]);
> 				}
> 			}
> 		}
> 		return res;
> 		
> 	}
> 	
> 	
> 	public static void main(String args[] ) {
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
> 		       System.out.println(longestLine(matrix));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%209%20Solutions/LongetsLine.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 9 Solutions/LongetsLine.java
