---
kind: "coding-problem"
title: "Largest Bitonic Subarray"
collection: "Coding Ninjas"
topic: "Dynamic Programming I"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-1/largest bitionic sub q.txt","CODING RESOURCES/coding ninjas/Dp-1/largest bitionic sub s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Largest Bitonic Subarray

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

You are given an array of positive integers as input. Write a code to return the length of the largest such sub-array in which the values are arranged first in strictly ascending order and then in strictly descending order.
Such a sub-array is known as bitonic sub-array. A purely increasing or purely decreasing subsequence will also be considered as a bitonic sequence with the other part empty.
Note that the elements in bitonic sub-array need not be consecutive in the given array but the order should remain same.

### Input Format

Line 1 : A positive Integer N, i.e., the size of array
Line 2 : N space-separated integers as elements of the array 

### Output Format

Length of Largest Bitonic Sub-Array
Input Constraints:
1<= N <= 10^5

### Sample Input 1

```text
6
15 20 20 6 4 2
```

### Sample Output 1

```text
5
Sample Output 1 Explanation:
Here, longest Bitonic sub-array is {15, 20, 6, 4, 2} which has length = 5.
```

### Sample Input 2

```text
2
1 5
```

### Sample Output 2

```text
2
```

### Sample Input 3

```text
2
5 1
```

### Sample Output 3

```text
2
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · largest bitionic sub s.txt
> ```text
> //This function returns the length of the longest bitonic sub-array
> int longestBitonicSubarray(int *input, int n)
> {
>    int i, j;
>
> // incr[] stores the Longest Increasing Sub-array ending with input[i]
>    int incr[n];
>    for(i = 0; i < n; i++) {
>       incr[i] = 1;
>    }
>
> // Setting incr[] values
>    for(i = 1; i < n; i++) {
>       for(j = 0; j < i; j++) {
>          if((input[i] > input[j]) && (incr[i] < incr[j] + 1)) {
>             incr[i] = incr[j] + 1;
>          }
>       }
>    }
>
> // decr[] stores the Longest Decreasing Sub-array starting with input[i]
>    int decr[n];
>    for(i = 0; i < n; i++) {
>       decr[i] = 1;
>    }
>
> // Setting decr[] values
>    for(i = n-2; i >= 0; i--) {
>       for(j = n-1; j > i; j--) {
>          if((input[i] > input[j]) && (decr[i] < decr[j] + 1)) {
>             decr[i] = decr[j] + 1;
>          }
>       }
>    }
>
> // Required length of longest bitonic sub-array is the maximum value of (incr[i] + decr[i] - 1)
>    int maxim = incr[0] + decr[0] - 1;
>    for(i = 1; i < n; i++) {
>      if(incr[i] + decr[i] - 1 > maxim) {
>          maxim = incr[i] + decr[i] - 1;
>      }
>    }
>    return maxim;
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/largest%20bitionic%20sub%20q.txt) · CODING RESOURCES/coding ninjas/Dp-1/largest bitionic sub q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/largest%20bitionic%20sub%20s.txt) · CODING RESOURCES/coding ninjas/Dp-1/largest bitionic sub s.txt
