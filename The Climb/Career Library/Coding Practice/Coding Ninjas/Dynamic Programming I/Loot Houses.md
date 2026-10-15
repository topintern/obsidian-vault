---
kind: "coding-problem"
title: "Loot Houses"
collection: "Coding Ninjas"
topic: "Dynamic Programming I"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-1/loot houses q.txt","CODING RESOURCES/coding ninjas/Dp-1/loot houses s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Loot Houses

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

A thief wants to loot houses. He knows the amount of money in each house. He cannot loot two consecutive houses. Find the maximum amount of money he can loot.

### Input Format

Line 1 : An integer N 
Line 2 : N spaced integers denoting money in each house

### Output Format

 Line 1 : Maximum amount of money looted
Input Constraints
1 <= n <= 10^4
1 <= A[i] < 10^4

### Sample Input

```text
6
5 5 10 100 10 5
```

### Sample Output 1

```text
110
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · loot houses s.txt
> ```cpp
> using namespace std;
>
> int getMaxMoney(int arr[], int n){
>     int *dp = new int[n];
>     dp[0] = arr[0];
>     if(n > 1){
>         dp[1] = max(arr[1], dp[0]);
>     }
>     for(int i=2; i<n; i++){
>         //dp[i-2] + arr[i] : Incase we are considering element
>         //dp[i-1] :,Incase we are skipping element
>         dp[i] = max(dp[i-2] + arr[i],dp[i-1]);
>     }
>
>     return dp[n-1];
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/loot%20houses%20q.txt) · CODING RESOURCES/coding ninjas/Dp-1/loot houses q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/loot%20houses%20s.txt) · CODING RESOURCES/coding ninjas/Dp-1/loot houses s.txt
