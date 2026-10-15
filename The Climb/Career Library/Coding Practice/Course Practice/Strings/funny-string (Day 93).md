---
kind: "coding-problem"
title: "funny-string (Day 93)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 93 Solutions/funny-string-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 93 Solutions/FunnyString.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# funny-string (Day 93)

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

> [!example]- Reference 1 · FunnyString.txt
> ```java
> import java.util.*;
>
> public class Solution {
>
>     private static String isFunny(char[] s){
>         boolean funny = true;
>         for(int i = 1, j = s.length - 1; 
>             i < s.length; 
>             i++, j--){
>             if( Math.abs(s[i] - s[i-1]) != Math.abs(s[j] - s[j-1])){
>                 funny = false;
>                 break;
>             }
>         }
>         return (funny) ? "Funny" : "Not Funny";
>     }
>     
>     public static void main(String[] args) {
>         Scanner scan = new Scanner(System.in);
>         int testCases = scan.nextInt();
>         for(int i = 0; i < testCases; i++){
>             System.out.println(
>                 isFunny( scan.next().toCharArray() )
>             );
>         }
>         scan.close();
>     }
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/funny-string-English-f3fe472b.pdf|funny-string-English-f3fe472b.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/funny-string-English-f3fe472b.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2093%20Solutions/funny-string-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 93 Solutions/funny-string-English.pdf
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2093%20Solutions/FunnyString.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 93 Solutions/FunnyString.txt
