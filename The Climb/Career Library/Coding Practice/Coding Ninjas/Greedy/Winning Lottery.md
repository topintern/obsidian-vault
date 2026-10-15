---
kind: "coding-problem"
title: "Winning Lottery"
collection: "Coding Ninjas"
topic: "Greedy"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/3.greedy/lottery q.txt","CODING RESOURCES/coding ninjas/3.greedy/lottery s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Winning Lottery

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Harshit knows by his resources that this time the winning lottery number is the smallest number whose sum of the digits is S and the number of digits is D. You have to help Harshit and print the winning lottery number.

### Input Format

The Input line contains two space-separated integers: S,D

### Output Format

The output contains a single integer denoting the winning lottery number

### Constraints

1 <= D <= 1000
1 <= S <= 9*D
Time Limit: 1 second
Sample Input1:
9 2
Sample Output1:
18

### Explanation

There are many other possible numbers like 45, 54, 90, etc with the sum of digits as 9 and number of digits as 2. The smallest of them is 18.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · lottery s.txt
> ```text
> def findSmallest(m,s): 
>   
>     res=[0 for i in range(m+1)] 
>    
>    
>     s -= 1
>   
>     for i in range(m-1,0,-1): 
>       
>         if (s > 9): 
>           
>             res[i] = 9
>             s -= 9
>       
>         else: 
>           
>             res[i] = s 
>             s = 0
>    
>     res[0] = s + 1 
>                      
>    
>    
>     for i in range(m): 
>         print(res[i],end="") 
>   
>   
> s,m=(int(j) for j in input().split())  
> findSmallest(m, s)
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/3.greedy/lottery%20q.txt) · CODING RESOURCES/coding ninjas/3.greedy/lottery q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/3.greedy/lottery%20s.txt) · CODING RESOURCES/coding ninjas/3.greedy/lottery s.txt
