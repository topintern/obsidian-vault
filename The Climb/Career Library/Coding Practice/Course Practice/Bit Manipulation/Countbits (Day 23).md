---
kind: "coding-problem"
title: "Countbits (Day 23)"
collection: "Course Practice"
topic: "Bit Manipulation"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/ELITE DAY 23 SOLUTIONS/countbits.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Countbits (Day 23)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Problem

The source has reference code without a separate problem statement. Establish its inputs, expected outputs, and constraints before practising.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · countbits.java
> ```java
> import java.util.*;
> class countbits {
>     public static int[] countBits(int start,int num) {
>         int[] ans = new int[num -start + 1];
>         for (int i = 0; start <= num; ++i,++start)
>             ans[i] = popcount(start);
>         return ans;
>     }
>     private static int popcount(int x) {
>         int count;
>         for (count = 0; x != 0; ++count)
>           x &= x - 1; //zeroing out the least significant nonzero bit
>         return count;
>     }
>     public static void main(String args[])
>     {
> 	Scanner sc=new Scanner(System.in);
> 	int start=sc.nextInt();
> 	int end=sc.nextInt();
> 	for(int n:countBits(start,end))
> 	System.out.print(n+" ");
>     }
>
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/ELITE%20DAY%2023%20SOLUTIONS/countbits.java) · CODING RESOURCES/ELITE FS COMPLETE/ELITE DAY 23 SOLUTIONS/countbits.java
