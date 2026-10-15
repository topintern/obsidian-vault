---
kind: "coding-problem"
title: "Count BSTs"
collection: "Coding Ninjas"
topic: "Dynamic Programming I"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-1/count bsts q.txt","CODING RESOURCES/coding ninjas/Dp-1/count bsts s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Count BSTs

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Given an integer N, find and return the count of unique Binary search trees (BSTs) are possible with nodes valued from 1 to N.
Output count can be very large, so return the count modulo 10^9+7.

### Input Format

Integer n 

### Output Format

Count of BSTs
Contraints :
1<= N <=1000

### Sample Input 1

```text
8
```

### Sample Output 1

```text
1430
```

### Sample Input 2

```text
3
```

### Sample Output 2

```text
5
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · count bsts s.txt
> ```cpp
> #include <climits> 
> int countBST( int n) {
> 	int *catalan = new int[n+1];
>     int mod = 1000000000 + 7;
> 	catalan[0] = catalan[1] = 1;
> 	for (int i=2; i<=n; i++)
> 	{
> 		catalan[i] = 0;
>         for (int j=0; j<i; j++) {
>             int temp = (int)(catalan[j] * 1l * catalan[i-j-1]) % mod;
> 			catalan[i] = (catalan[i] + temp) % mod;
>         }
> 	}
> 	return catalan[n] % mod;
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/count%20bsts%20q.txt) · CODING RESOURCES/coding ninjas/Dp-1/count bsts q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/count%20bsts%20s.txt) · CODING RESOURCES/coding ninjas/Dp-1/count bsts s.txt
