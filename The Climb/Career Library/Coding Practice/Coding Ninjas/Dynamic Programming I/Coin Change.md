---
kind: "coding-problem"
title: "Coin Change"
collection: "Coding Ninjas"
topic: "Dynamic Programming I"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-1/coin change q.txt","CODING RESOURCES/coding ninjas/Dp-1/coin change s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Coin Change

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

You are given an infinite supply of coins of each of denominations D = {D0, D1, D2, D3, ...... Dn-1}. You need to figure out the total number of ways W, in which you can make change for Value V using coins of denominations D.
Note : Return 0, if change isn't possible.

### Input Format

Line 1 : Integer n i.e. total number of denominations
Line 2 : N integers i.e. n denomination values
Line 3 : Value V

### Output Format

Line 1 :  Number of ways i.e. W

### Constraints

1<=n<=10
1<=V<=1000

### Sample Input 1

```text
3
1 2 3
4
```

### Sample Output

```text
4
Sample Output Explanation :
Number of ways are - 4 total i.e. (1,1,1,1), (1,1, 2), (1, 3) and (2, 2).
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · coin change s.txt
> ```java
>
> public class Solution {
>
> 	
> 	public static int countWaysToMakeChange(int denominations[], int value){
> 		int n = denominations.length;
> 		int ways[][] = new int[n][value + 1];
> 		for(int i = 0; i < n; i++){
> 			ways[i][0] = 1;
> 		}
> 		for(int i = n-1; i >=0 ; i--){
> 			for(int j = 1; j <= value; j++){		
> 				int count1 = 0;
> 				if(i + 1 <= n - 1){
> 					count1 = ways[i + 1][j] ;
> 				}
> 				int count2 = 0;
> 				if(j - denominations[i] >= 0){
> 					count2 = ways[i][j - denominations[i]];
> 				}
> 				ways[i][j] = count1 + count2;
> 			}
> 		}
> 		return ways[0][value];
> 	}
> 	
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/coin%20change%20q.txt) · CODING RESOURCES/coding ninjas/Dp-1/coin change q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/coin%20change%20s.txt) · CODING RESOURCES/coding ninjas/Dp-1/coin change s.txt
