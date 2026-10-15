---
kind: "coding-problem"
title: "the-great-xor (Day 92)"
collection: "Course Practice"
topic: "Bit Manipulation"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 92 Solutions/GreatXOR.java","CODING RESOURCES/ELITE FS COMPLETE/Day 92 Solutions/the-great-xor-English.pdf"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# the-great-xor (Day 92)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Problem

Read the original PDF below. Its mathematical notation was not reliably preserved by text extraction.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · GreatXOR.java
> ```java
> import java.util.*;
>
> public class Solution {
>
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         int q = in.nextInt();
>         for(int a0 = 0; a0 < q; a0++){
>             long x = in.nextLong();
>             // your code goes here
>             long b = 1;
>             long total = 0;
>             while(b < x) {
>                 if((b & x) == 0) {
>                     total += b;
>                 }
>                 b = b * 2;
>             }
>             System.out.println(total);
>         }
>     }
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/the-great-xor-English-d40b9c1e.pdf|the-great-xor-English-d40b9c1e.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/the-great-xor-English-d40b9c1e.pdf#height=420]]

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2092%20Solutions/GreatXOR.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 92 Solutions/GreatXOR.java
- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2092%20Solutions/the-great-xor-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 92 Solutions/the-great-xor-English.pdf
