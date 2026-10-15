---
kind: "coding-problem"
title: "Magical String (Day 98)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 98 Solutions/Magical String - LeetCode.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 98 Solutions/MagicalString.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Magical String (Day 98)

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

> [!example]- Reference 1 · MagicalString.java
> ```java
> import java.util.Scanner;
>
> class MagicalString {
>     public static int magicalString(int n) {
>         if (n <= 0) return 0;
>         if (n <= 3) return 1;
>         
>         int[] a = new int[n + 1];
>         a[0] = 1; a[1] = 2; a[2] = 2;
>         int head = 2, tail = 3, num = 1, result = 1;
>         
>         while (tail < n) {
>             for (int i = 0; i < a[head]; i++) {
>                 a[tail] = num;
>                 if (num == 1 && tail < n) result++;
>                 tail++;
>             }
>             num = num ^ 3;
>             head++;
>         }
>         
>         return result;
>     }
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		int N=sc.nextInt();
> 		System.out.println(magicalString(N));
> 	}
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/Magical String - Leet Code-f1f3f219.pdf|Magical String - Leet Code-f1f3f219.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/Magical String - Leet Code-f1f3f219.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2098%20Solutions/Magical%20String%20-%20LeetCode.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 98 Solutions/Magical String - LeetCode.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2098%20Solutions/MagicalString.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 98 Solutions/MagicalString.java
