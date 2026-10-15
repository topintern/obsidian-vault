---
kind: "coding-problem"
title: "Mandragora Forest (Day 94)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 94 Solutions/MandragoraForest.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Mandragora Forest (Day 94)

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

> [!example]- Reference 1 · MandragoraForest.java
> ```java
> import java.io.*;
> import java.util.*;
> import java.text.*;
> import java.math.*;
> import java.util.regex.*;
>
> public class MandragoraForest {
>
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>             int n = in.nextInt();
>             List<Long> healths = new ArrayList<>();
>             for (int i = 0; i < n; i++) {
>                 healths.add(in.nextLong());
>             }
>             Collections.sort(healths);
>             long maxExp = 0;
>             long totalHealth = 0;
>             long totalStrength = n + 1;
>             for (int i = n - 1; i >= 0; i--) {
>                 totalStrength--;
>                 totalHealth += healths.get(i);
>                 long exp = totalStrength * totalHealth;
>                 if (exp > maxExp) {
>                     maxExp = exp;
>                 }
>             }
>             System.out.println(maxExp);
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2094%20Solutions/MandragoraForest.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 94 Solutions/MandragoraForest.java
