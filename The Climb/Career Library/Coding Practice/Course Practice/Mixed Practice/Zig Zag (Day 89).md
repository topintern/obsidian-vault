---
kind: "coding-problem"
title: "Zig Zag (Day 89)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 89 Solutions/ZigZag.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Zig Zag (Day 89)

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

> [!example]- Reference 1 · ZigZag.java
> ```java
> import java.util.*;
> import java.lang.*;
> import java.io.*;
> import java.math.*;
> public class ZigZag {
>     
>     public static void main (String[] args) throws java.lang.Exception {
>         Scanner kb = new Scanner(System.in);
>         int test_cases = kb.nextInt();
>         for(int cs = 1; cs <= test_cases; cs++){
>             int n = kb.nextInt();
>              int a[] = new int[n];
>             for(int i = 0; i < n; i++){
>                 a[i] = kb.nextInt();
>             }
>             findZigZagSequence(a, n);
>         }
>    }
>    
>     public static void findZigZagSequence(int [] a, int n){
>         Arrays.sort(a);
>         int mid = n/2;
>     
>         int temp = a[mid];
>         a[mid] = a[n - 1];
>         a[n - 1] = temp;
>         int st = mid + 1;
>         int ed = n - 2;
>         while(st <= ed){
>             temp = a[st];
>             a[st] = a[ed];
>             a[ed] = temp;
>             st = st + 1;
>             ed = ed - 1;
>         }
>         for(int i = 0; i < n; i++){
>             System.out.print(a[i]);
>             if(i<n-1)
>             System.out.print(" ");
>         }
>         System.out.println();
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2089%20Solutions/ZigZag.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 89 Solutions/ZigZag.java
