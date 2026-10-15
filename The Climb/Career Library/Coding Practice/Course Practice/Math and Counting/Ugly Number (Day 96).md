---
kind: "coding-problem"
title: "Ugly Number (Day 96)"
collection: "Course Practice"
topic: "Math and Counting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 96 Solutions/UglyNumber.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Ugly Number (Day 96)

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

> [!example]- Reference 1 · UglyNumber.java
> ```java
> import java.util.Scanner;
>
> public class UglyNumber {
>     public static long nthUglyNumber(int n) {
>         long[] ugly = new long[n];
>         ugly[0] = 1;
>         int index2 = 0, index3 = 0, index5 = 0;
>         long factor2 = 2, factor3 = 3, factor5 = 5;
>         for(int i=1;i<n;i++){
>             long min = Math.min(Math.min(factor2,factor3),factor5);
>             ugly[i] = min;
>             if(factor2 == min)
>                 factor2 = 2*ugly[++index2];
>             if(factor3 == min)
>                 factor3 = 3*ugly[++index3];
>             if(factor5 == min)
>                 factor5 = 5*ugly[++index5];
>         }
>         return ugly[n-1];
>     }
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
>         int n=sc.nextInt();
> 		System.out.println(nthUglyNumber(n));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2096%20Solutions/UglyNumber.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 96 Solutions/UglyNumber.java
