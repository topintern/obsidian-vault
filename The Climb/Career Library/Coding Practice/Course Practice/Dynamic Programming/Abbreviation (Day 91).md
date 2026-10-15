---
kind: "coding-problem"
title: "Abbreviation (Day 91)"
collection: "Course Practice"
topic: "Dynamic Programming"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 91 Solutions/Abbreviation.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Abbreviation (Day 91)

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

> [!example]- Reference 1 · Abbreviation.txt
> ```java
> import java.io.*;
> import java.util.*;
> import java.text.*;
> import java.math.*;
> import java.util.regex.*;
>
> public class Solution {
>
>     public static void main(String[] args) {
>         Scanner sc = new Scanner(System.in);
>         int q = sc.nextInt();
>         sc.nextLine();
>         for (int z = 0; z < q; z++) {
>             char[] a = sc.nextLine().toCharArray();
>             char[] b = sc.nextLine().toCharArray();
>             boolean[][] dp = new boolean[a.length+1][b.length+1];
>             for (int i = 0; i <= a.length; i++)
>             dp[i][0] = true;
>             for (int i = 1; i <= a.length; i++) {
>                 if (a[i-1]>='A'&&a[i-1]<='Z') {
>                     for (int j = 1; j <= b.length; j++) {
>                         if (b[j-1]==a[i-1])
>                             dp[i][j] = dp[i-1][j-1];
>                     }
>                 } else {
>                     char c = (char)(a[i-1]-32);
>                     for (int j = 1; j <= b.length; j++) {
>                         if (b[j-1]==c)
>                             dp[i][j] = dp[i-1][j-1];
>                         dp[i][j] |= dp[i-1][j];
>                     }
>                 }
>             }
>             System.out.println(dp[a.length][b.length]?"YES":"NO");
>         }
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2091%20Solutions/Abbreviation.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 91 Solutions/Abbreviation.txt
