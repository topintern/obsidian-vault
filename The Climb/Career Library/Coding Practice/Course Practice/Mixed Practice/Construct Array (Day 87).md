---
kind: "coding-problem"
title: "Construct Array (Day 87)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 87 Solutions/ConstructArray.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Construct Array (Day 87)

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

> [!example]- Reference 1 · ConstructArray.java
> ```java
> import java.util.*;
> import java.math.*;
>
> public class ConstructArray {
>     static long countArray(int n, int k, int x) {
>         long mod = 1000000007;
>         long val1 = 1;
>         for (long i=2;i<=n;i++) {
>             if (i % 2 == 0) {
>                 val1 = ((val1 - 1)%mod) * ((k-1)%mod);
>             } else {
>                 val1 = ((val1 + 1)%mod) * ((k-1)%mod);
>             }
>             val1 = val1 % mod;
>         }
>         long valRest = n % 2 == 0 ? val1+1 : val1-1;
>         if (x==1) {
>             return val1;
>         }
>         return valRest;
>     }
>
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         int n = in.nextInt();
>         int k = in.nextInt();
>         int x = in.nextInt();
>         long answer = countArray(n, k, x);
>         System.out.println(answer);
>         in.close();
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2087%20Solutions/ConstructArray.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 87 Solutions/ConstructArray.java
