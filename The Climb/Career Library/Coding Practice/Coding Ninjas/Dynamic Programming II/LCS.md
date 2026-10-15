---
kind: "coding-problem"
title: "LCS"
collection: "Coding Ninjas"
topic: "Dynamic Programming II"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-2/lcs q.txt","CODING RESOURCES/coding ninjas/Dp-2/lcs s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# LCS

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Given 2 strings of S1 and S2 with lengths m and n respectively, find the length of longest common subsequence.
A subsequence of a string S whose length is n, is a string containing characters in same relative order as they are present in S, but not necessarily contiguous. Subsequences contain all the strings of length varying from 0 to n. E.g. subsequences of string "abc" are - "",a,b,c,ab,bc,ac,abc.

### Input Format

Line 1 : String S1
Line 2 : String s2

### Output Format

Line 1 : Length of lcs

### Sample Input

```text
adebc
dcadb
```

### Sample Output

```text
3
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · lcs s.txt
> ```cpp
> #include<iostream>
> #include<cstring>
> using namespace std;
>
> int lcs(string s, string t){
>
>   int m = s.size();
> 	int n = t.size();
> 	int **ans = new int*[m+1];
> 	for(int i = 0; i <= m; i++) {
> 		ans[i] = new int[n+1];
> 	}
>
> 	// First row
> 	for(int j = 0; j <= n; j++) {
> 		ans[0][j] = 0;
> 	}
>
> 	// First col
> 	for(int i = 0; i <= m; i++) {
> 		ans[i][0] = 0;
> 	}
>
> 	for(int i = 1; i <= m; i++) {
> 		for(int j = 1; j <= n; j++) {
> 			if(s[m-i] == t[n-j]) {
> 				ans[i][j] = 1 + ans[i-1][j-1];
>
> 			}
> 			else {
> 				ans[i][j] = max(ans[i-1][j], ans[i][j-1]);
> 			}
> 		}
> 	}
> 	return ans[m][n];
>
>
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/lcs%20q.txt) · CODING RESOURCES/coding ninjas/Dp-2/lcs q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/lcs%20s.txt) · CODING RESOURCES/coding ninjas/Dp-2/lcs s.txt
