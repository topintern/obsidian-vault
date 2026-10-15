---
kind: "coding-problem"
title: "Problem discussion"
collection: "Coding Ninjas"
topic: "Greedy"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/3.greedy/problem q.txt","CODING RESOURCES/coding ninjas/3.greedy/problem s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Problem discussion

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Harshit gave Aahad an array of size N and asked to minimize the difference between the maximum value and minimum value by modifying the array under the condition that each array element either increase or decrease by k(only once).
It seems difficult for Aahad so he asked for your help

### Input Format

The First line contains two space-separated integers: N,K
Next lines contain N space-separated integers denoting elements of the array

### Output Format

The output contains a single integer denoting the minimum difference between maximum value and the minimum value in the array

### Constraints

1 =< N <= 10^5 
1 <= Ai,K <= 10^9
Sample Input1:
3 6
1 15 10
Sample Output1:
5
Explaination
We change from 1 to 6, 15 to  9 and 10 to 4. Maximum difference is 5 (between 4 and 9). We can't get a lower difference.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · problem s.txt
> ```text
> def getMinDiff(arr, n, k): 
>   
>     if (n == 1): 
>         return 0
>  
>     arr.sort()  
>   
>     ans = arr[n-1] - arr[0]  
>   
>     small = arr[0] + k  
>     big = arr[n-1] - k  
>       
>     if (small > big): 
>         small, big = big, small  
>   
>  
>     for i in range(1, n-1): 
>       
>         subtract = arr[i] - k  
>         add = arr[i] + k  
>   
>      
>         if (subtract >= small or add <= big): 
>             continue
>   
>         if (big - subtract <= add - small): 
>             small = subtract  
>         else: 
>             big = add  
>       
>   
>     return min(ans, big - small)  
> n,k=(int(j) for j in input().split())  
> arr=input().split()
> arr=[int(j) for j in arr] 
> print(getMinDiff(arr, n, k))
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/3.greedy/problem%20q.txt) · CODING RESOURCES/coding ninjas/3.greedy/problem q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/3.greedy/problem%20s.txt) · CODING RESOURCES/coding ninjas/3.greedy/problem s.txt
