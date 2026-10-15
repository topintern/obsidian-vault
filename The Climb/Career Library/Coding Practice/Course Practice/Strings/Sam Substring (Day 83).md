---
kind: "coding-problem"
title: "Sam Substring (Day 83)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 83 Solutions/SamSubstring.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Sam Substring (Day 83)

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

> [!example]- Reference 1 · SamSubstring.java
> ```java
> import java.util.*;
>
> public class SamSubstring {
>     static final long P = 1000000007;
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>
>         String line = in.nextLine();
>         long t = 0;
>         long p = 0;
>
>         for(int i = 0; i < line.length(); i++) {
>             long ch = (long) (line.charAt(i) - '0');
>             p = (p * 10 + ch * (i+1)) % P;
>             t = (t + p) % P;
>         }
>         System.out.println(t);
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2083%20Solutions/SamSubstring.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 83 Solutions/SamSubstring.java
