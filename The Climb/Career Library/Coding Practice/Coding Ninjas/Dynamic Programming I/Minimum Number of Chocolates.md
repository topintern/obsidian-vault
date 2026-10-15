---
kind: "coding-problem"
title: "Minimum Number of Chocolates"
collection: "Coding Ninjas"
topic: "Dynamic Programming I"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-1/min no of choc q.txt","CODING RESOURCES/coding ninjas/Dp-1/min no of choc s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Minimum Number of Chocolates

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Noor is a teacher. She wants to give some chocolates to the students in her class. All the students sit in a line and each of them has a score according to performance. Noor wants to give at least 1 chocolate to each student. She distributes chocolates to them such that If two students sit next to each other then the one with the higher score must get more chocolates. Noor wants to save money, so she wants to minimise the total number of chocolates.
Note that when two students have equal score they are allowed to have different number of chocolates.

### Input Format

First Line: Integer N, the number of students in Noor’s class. 
Second Line: Each of the student's score separated by spaces.

### Output Format

Output a single line containing the minimum number of chocolates Noor must give.
Input Constraints
 1 <= N <= 100000
 1 <= score <= 100000

### Sample Input

```text
4
1 4 4 6
```

### sample Output

```text
6
```

### Sample Input

```text
3
8 7 5
```

### sample Output

```text
6
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · min no of choc s.txt
> ```text
>  int getMin(int *arr, int n){
>     int *dp = new int[n+1];
>     dp[0] = 1;
>
>     int i = 0;
>     int sum = 0;
>     for(i = 1; i < n; i++){
>         if(arr[i] > arr[i-1])
>         {
>             dp[i] = dp[i-1]+1;
>         }
>         else
>             dp[i] = 1;
>     }
>     for(i = n-2; i >= 0; i--){
>         if(arr[i] > arr[i+1] && dp[i] <= dp[i+1]){
>             dp[i] = dp[i+1]+1;
>         }
>     }
>     for(i = 0; i < n; i++)
>         sum += dp[i];
>     delete []dp;
>     return sum;
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/min%20no%20of%20choc%20q.txt) · CODING RESOURCES/coding ninjas/Dp-1/min no of choc q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/min%20no%20of%20choc%20s.txt) · CODING RESOURCES/coding ninjas/Dp-1/min no of choc s.txt
