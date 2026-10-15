---
kind: "coding-problem"
title: "Perimeter with conditions"
collection: "Coding Ninjas"
topic: "Greedy"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/3.greedy/perimeter q.txt","CODING RESOURCES/coding ninjas/3.greedy/perimeter s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Perimeter with conditions

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Aahad gives an array of integers and asks Harshit to find which three elements form a triangle (non-degenerate). The task seems easy to Harshit.
So, Aahad adds some conditions to this task -
1. Find the triangle with maximum perimeter
2. If there are two or more combinations with same value of maximum perimeter, then find the one with the longest side.
3.If there are more than one combinations which satisfy all the above conditions the find with maximum longest minimum side.

### Input Format

The First line contains no of elements of array: N
Each T lines contains N space-separated integers: A [i]

### Output Format

The output contains three space-separated elements that denote the length of the sides of triangle. If no such triangle is possible, then print -1.

### Constraints

1 =< N <= 10^5 
1 <= A[i] <= 10^9
Time Limit: 1 second
Sample Input1:
5
1 1 1 3 3
Sample Output1:
1 3 3 
Sample Input2:
3
2 2 4
Sample Output3:
-1 
Explaination
In the First Sample case, the elements that form a triangle with maximum perimeter is 1,3,3.
In the Second Sample case, the elements that can form a triangle are degenerate, so, we printed -1.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · perimeter s.txt
> ```text
> n=int(input())
> a=input().split()
> a=[int(j) for j in a]
> a.sort()
> a.reverse()
> c =0
> for i in range(n-2):
> 	if a[i + 2] + a[i + 1] <= a[i]:
> 		continue
> 	s = str(a[i+2]) + " " + str(a[i+1]) + " "  + str(a[i])  
> 	print(s)
> 	c= 1
> 	break
> if c==0:
> 	print("-1")
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/3.greedy/perimeter%20q.txt) · CODING RESOURCES/coding ninjas/3.greedy/perimeter q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/3.greedy/perimeter%20s.txt) · CODING RESOURCES/coding ninjas/3.greedy/perimeter s.txt
