---
kind: "coding-problem"
title: "Longest Line of Consecutive One in Matrix (Day 102)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 102 Solutions/Longest Line of Consecutive One in Matrix.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 102 Solutions/LongestLine.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Longest Line of Consecutive One in Matrix (Day 102)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Problem

Read the original PDF below. Its mathematical notation was not reliably preserved by text extraction.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · LongestLine.java
> ```java
> import java.util.Scanner;
>
> class LongestLine {
>   public static int longestLine(int[][] M) {
>     if (M.length == 0) 
> 		return 0;
>     
> 	int ones = 0;
>     int[][] dp = new int[M[0].length][4];
>     for (int i = 0; i < M.length; i++) {
>       int old = 0;
>       for (int j = 0; j < M[0].length; j++) {
>         if (M[i][j] == 1) {
>           dp[j][0] = j > 0 ? dp[j - 1][0] + 1 : 1;
>           dp[j][1] = i > 0 ? dp[j][1] + 1 : 1;
>           int prev = dp[j][2];
>           dp[j][2] = (i > 0 && j > 0) ? old + 1 : 1;
>           old = prev;
>           dp[j][3] = (i > 0 && j < M[0].length - 1) ? dp[j + 1][3] + 1 : 1;
>           ones = Math.max(ones, Math.max(Math.max(dp[j][0], dp[j][1]), Math.max(dp[j][2], dp[j][3])));
>         } else {
>           old = dp[j][2];
>           dp[j][0] = dp[j][1] = dp[j][2] = dp[j][3] = 0;
>         }
>       }
>     }
>     return ones;
>   }
>   
>   public static void main(String args[])
>   {
> 		Scanner sc=new Scanner(System.in);
> 		int r=sc.nextInt();
> 		int c=sc.nextInt();
> 		int[][] arr=new int[r][c];
> 		for(int i=0;i<r;i++)
> 			for(int j=0;j<c;j++)
> 				arr[i][j]=sc.nextInt();
> 		System.out.println( longestLine(arr));
>   }
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/Longest Line of Consecutive One in Matrix-c69bed23.pdf|Longest Line of Consecutive One in Matrix-c69bed23.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/Longest Line of Consecutive One in Matrix-c69bed23.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20102%20Solutions/Longest%20Line%20of%20Consecutive%20One%20in%20Matrix.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 102 Solutions/Longest Line of Consecutive One in Matrix.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20102%20Solutions/LongestLine.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 102 Solutions/LongestLine.java
