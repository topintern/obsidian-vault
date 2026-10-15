---
kind: "coding-problem"
title: "bear-and-steady-gene (Day 95)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 95 Solutions/bear-and-steady-gene-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 95 Solutions/BearAndSteadyGene.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# bear-and-steady-gene (Day 95)

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

> [!example]- Reference 1 · BearAndSteadyGene.java
> ```java
> import java.io.*;
> import java.util.*;
> import java.text.*;
> import java.math.*;
> import java.util.regex.*;
>
> public class BearAndSteadyGene {
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         int n = in.nextInt();
>         String s = in.next();
>         in.close();  
>         int needed = n / 4;
> 		int[] count = new int[256];
> 		for(int i=0; i < s.length(); i++) 
> 			count[s.charAt(i)]++;
>         if(count['A'] == needed && count['C'] == needed && count['B'] == needed && count['D'] == needed) {
> 			 System.out.println(0);
>              return;
>         }
> 		int right = 0;
>
> 		int result = n;
> 		for (int left = 0; left < n; left++) {
> 			while (count['A'] > needed || count['C'] > needed || count['B'] > needed || count['D'] > needed) {				
>                 if (right == n)	{
> 					System.out.println(result);
>                     return;
>                 }                
> 				--count[s.charAt(right)];
> 				++right;
> 			}
> 			result = Math.min(result, right - left);
> 			++count[s.charAt(left)];
> 		}
>         System.out.println(result); 
>     }
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/bear-and-steady-gene-English-be5932fa.pdf|bear-and-steady-gene-English-be5932fa.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/bear-and-steady-gene-English-be5932fa.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2095%20Solutions/bear-and-steady-gene-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 95 Solutions/bear-and-steady-gene-English.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2095%20Solutions/BearAndSteadyGene.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 95 Solutions/BearAndSteadyGene.java
