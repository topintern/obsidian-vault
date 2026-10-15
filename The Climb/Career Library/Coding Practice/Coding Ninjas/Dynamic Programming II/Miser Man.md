---
kind: "coding-problem"
title: "Miser Man"
collection: "Coding Ninjas"
topic: "Dynamic Programming II"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-2/miser man q.txt","CODING RESOURCES/coding ninjas/Dp-2/miser man s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Miser Man

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Jack is a wise and miser man. Always tries to save his money.
One day, he wants to go from city A to city B. Between A and B, there are N number of cities(including B and excluding A) and in each city there are M buses numbered from 1 to M. And the fare of each bus is different. Means for all N*M busses, fare (K) may be different or same. Now Jack has to go from city A to city B following these conditions:
1. At every city, he has to change the bus.
2. And he can switch to only those buses which have number either equal or 1 less or 1 greater to the previous.
You are to help Jack to go from A to B by spending the minimum amount of money.
N, M, K <= 100.

### Input

Line 1:    N M

Line 2:    NxM Grid

Each row lists the fares the M busses to go form the current city to the next city.

### Output

Single Line containing the minimum amount of fare that Jack has to give.

### Sample Input

```text
5 5
1  3  1  2  6
10 2  5  4  15
10 9  6  7  1
2  7  1  5  3
8  2  6  1  9
```

### Sample Output

```text
10
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · miser man s.txt
> ```cpp
> #include <cstdio>
> #include <iostream>
> using namespace std;
> int A[100][100], B[100][100], w, h;
> int fun(int i, int j)
> {
> 	int ans, a=1000000, b=1000000, c=1000000;
> 	if(i==h)
> 	{
> 		return 0;
> 	}
> 	if(B[i][j]!=-1)
> 	{
> 		return B[i][j];
> 	}
> 	if(j<w-1&&i<h)
> 	a=A[i][j]+fun(i+1, j+1);
> 	if(j>0&&i<h)
> 	b=A[i][j]+fun(i+1,j-1);
> 	if(i<h)
> 	c=A[i][j]+fun(i+1,j);
> 	ans=a;
> 	if(b<ans)
> 	ans=b;
> 	if(c<ans)
> 	ans=c;
> 	B[i][j]=ans;
> 	return ans;
> }
> int main() {
> 	int ans, m, i, j;
>     for(i=0;i<100;i++)
>     for(j=0;j<100;j++)
>     {
>         B[i][j]=-1;
>     }
>     scanf("%d%d",&h, &w);
>     for(i=0;i<h;i++)
>     for(j=0;j<w;j++)
>     {
>         scanf("%d",&A[i][j]);
>     }
>     m=100000;
>     for(i=0;i<w;i++)
>     {
>         ans=fun(0,i);
>         if(ans<m)
>         m=ans;
>     }
>     printf("%d\n", m);
>     return 0;
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/miser%20man%20q.txt) · CODING RESOURCES/coding ninjas/Dp-2/miser man q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/miser%20man%20s.txt) · CODING RESOURCES/coding ninjas/Dp-2/miser man s.txt
