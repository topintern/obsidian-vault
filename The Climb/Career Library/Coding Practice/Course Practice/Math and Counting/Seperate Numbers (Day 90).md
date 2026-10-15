---
kind: "coding-problem"
title: "Seperate Numbers (Day 90)"
collection: "Course Practice"
topic: "Math and Counting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 90 Solutions/SeperateNumbers.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Seperate Numbers (Day 90)

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

> [!example]- Reference 1 · SeperateNumbers.txt
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
>         Scanner in = new Scanner(System.in);
>         int q = in.nextInt();
>         for(int a0 = 0; a0 < q; a0++){
>             int f=0;
>             String s = in.next();
>             int l=s.length();
>             if(l==1)
>                 {
>                 System.out.println("NO");
>                 continue;
>                 
>             }
>             for(int i=1;i<=l/2;i++)
>                 {
>                 String s1=s.substring(0,i);
>                 long y=Long.parseLong(s1);
>                 long x=y;
>                 while(s1.length()<l)
>                     {
>                      x++;
>                     s1=s1+String.valueOf(x);
>                        
>                 }
>                 if(s1.equals(s))
>                     {
>                     f=1;
>                     System.out.println("YES "+y);
>                     break;       
>                 }    
>             }
>             if(f==0)
>                 System.out.println("NO");                         
>         }    
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2090%20Solutions/SeperateNumbers.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 90 Solutions/SeperateNumbers.txt
