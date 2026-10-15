---
kind: "coding-problem"
title: "pairs (Day 91)"
collection: "Course Practice"
topic: "Arrays and Sorting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 91 Solutions/pairs-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 91 Solutions/Pairs.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# pairs (Day 91)

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

> [!example]- Reference 1 · Pairs.java
> ```java
> import java.io.*;
> import java.util.*;
> import java.text.*;
> import java.math.*;
> import java.util.regex.*;
>
> public class Pairs {
>     static int pairs(int[] a,int k) {
>         Arrays.sort(a);
>         int N = a.length;
> 		int count = 0;
> 		for (int i = 0; i < N - 1; i++)
> 		{
> 			int j = i + 1;
> 			while((j < N) && (a[j++] - a[i]) < k);
> 			j--;
> 			while((j < N) && (a[j++] - a[i]) == k)
> 				count++;			
> 		}
>
>         return count;
>     }
>
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         int res;
>         
>         String n = in.nextLine();
>         String[] n_split = n.split(" ");
>         
>         int _a_size = Integer.parseInt(n_split[0]);
>         int _k = Integer.parseInt(n_split[1]);
>         
>         int[] _a = new int[_a_size];
>         int _a_item;
>         String next = in.nextLine();
>         String[] next_split = next.split(" ");
>         
>         for(int _a_i = 0; _a_i < _a_size; _a_i++) {
>             _a_item = Integer.parseInt(next_split[_a_i]);
>             _a[_a_i] = _a_item;
>         }
>         
>         res = pairs(_a,_k);
>         System.out.println(res);
>     }
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/pairs-English-841067d1.pdf|pairs-English-841067d1.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/pairs-English-841067d1.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2091%20Solutions/pairs-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 91 Solutions/pairs-English.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2091%20Solutions/Pairs.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 91 Solutions/Pairs.java
