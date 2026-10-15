---
kind: "coding-problem"
title: "Vanya and GCD"
collection: "Coding Ninjas"
topic: "Dynamic Programming I"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-1/vanya gcd q.txt","CODING RESOURCES/coding ninjas/Dp-1/vanya gcd s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Vanya and GCD

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Vanya has been studying all day long about sequences and other Complex Mathematical Terms. She thinks she has now become really good at it. So, her friend Vasya decides to test her knowledge and keeps the following challenge it front of her:
Vanya has been given an integer array A of size N. Now, she needs to find the number of increasing sub-sequences of this array with length =1 and GCD=1. A sub-sequence of an array is obtained by deleting some (or none) elements and maintaining the relative order of the rest of the elements. As the answer may be large, print it Modulo 109+7
She finds this task really easy, and thinks that you can do it too. Can you?

### Input Format

The first line contains a single integer N denoting size of array A. The next line contains N space separated integers denoting the elements of array A

### Output Format

Print the required answer Modulo 10^9+7 on a single line.

### Constraints

1=N=500

1=A[i]=100

### Sample Input

```text
3
1 2 3
```

### Sample Output

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

> [!example]- Reference 1 · vanya gcd s.txt
> ```cpp
> #include <iostream>
> #include <algorithm>
> #define ss(n) scanf("%d", &n)
> #define mod 1000000007
> using namespace std;
> int dp[501][101], A[501];
> int main()
> {
> 	int i, j, n, k, x, m=0;
> 	ss(n);
> 	for(i=0;i<n;i++)
> 	{
> 		ss(A[i]);
> 		m=max(A[i],m);
> 		dp[i][A[i]]=1;
> 	}
> 	for(i=1;i<n;i++)
> 	for(j=0;j<i;j++)
> 	{
> 		if(A[i]>A[j])
> 		{
> 			for(k=1;k<=m;k++)
> 			{
> 				x=__gcd(k, A[i]);
> 				dp[i][x]+=dp[j][k];
> 				if(dp[i][x]>=mod)
> 				dp[i][x]-=mod;
> 			}
> 		}
> 	}
> 	int ans=0;
> 	for(i=0;i<n;i++)
> 	{
> 		ans+=dp[i][1];
> 		if(ans>=mod)
> 		ans-=mod;
> 	}
> 	printf("%d\n", ans);
>     return 0;
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/vanya%20gcd%20q.txt) · CODING RESOURCES/coding ninjas/Dp-1/vanya gcd q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/vanya%20gcd%20s.txt) · CODING RESOURCES/coding ninjas/Dp-1/vanya gcd s.txt
