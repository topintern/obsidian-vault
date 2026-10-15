---
kind: "coding-problem"
title: "Full Counting Sort (Day 94)"
collection: "Course Practice"
topic: "Arrays and Sorting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 94 Solutions/FullCountingSort.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Full Counting Sort (Day 94)

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

> [!example]- Reference 1 · FullCountingSort.java
> ```java
> import java.io.*;
> import java.util.*;
> import java.text.*;
> import java.math.*;
> import java.util.regex.*;
>
> public class FullCountingSort {
>     public static void main(String[] args) throws Exception {
>         BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
>         int n = Integer.parseInt(in.readLine());
>         StringBuffer[] map = new StringBuffer[100];
>         for(int i = 0; i < 100; i++) {
>             map[i] = new StringBuffer();
>         }
>         for(int i = 0; i < n; i++) {
>             StringTokenizer tok = new StringTokenizer(in.readLine());
>             int v = Integer.parseInt(tok.nextToken());
>             String s = tok.nextToken();
>             map[v].append(i < n / 2 ? "-" : s).append(" ");
>         }
>         for(int i = 0; i < 100; i++) {
>             System.out.print(map[i]);
>         }
>         System.out.println();
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2094%20Solutions/FullCountingSort.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 94 Solutions/FullCountingSort.java
