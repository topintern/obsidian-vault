---
kind: "coding-problem"
title: "Min. Absolute Difference In Array"
collection: "Coding Ninjas"
topic: "Greedy"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/3.greedy/min difference q.txt","CODING RESOURCES/coding ninjas/3.greedy/min difference s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Min. Absolute Difference In Array

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Given an integer array A of size N, find and return the minimum absolute difference between any two elements in the array.
We define the absolute difference between two elements ai, and aj (where i != j ) is |ai - aj|.

### Input format

Line 1 : Integer N, Array Size
Line 2 : Array elements (separated by space)

### Output Format

Minimum difference

### Constraints

1 <= N <= 10^6

### Sample Input

```text
5
2 9 0 4 5
```

### Sample Input

```text
1
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · min difference s.txt
> ```cpp
> #include<iostream>
> #include<algorithm>
> using namespace std;
>
> int minAbsoluteDiff(int input[],int size)
> {
>   sort(input,input+size);
>   int ans=input[1]-input[0];
>   for(int i=0;i<size-1;i++)
>   {
>     ans=min(ans,input[i+1]-input[i]);
>   }
>   return ans;
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/3.greedy/min%20difference%20q.txt) · CODING RESOURCES/coding ninjas/3.greedy/min difference q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/3.greedy/min%20difference%20s.txt) · CODING RESOURCES/coding ninjas/3.greedy/min difference s.txt
