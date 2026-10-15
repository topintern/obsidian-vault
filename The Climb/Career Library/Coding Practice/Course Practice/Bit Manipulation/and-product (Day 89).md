---
kind: "coding-problem"
title: "and-product (Day 89)"
collection: "Course Practice"
topic: "Bit Manipulation"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 89 Solutions/and-product-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 89 Solutions/AndProduct.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# and-product (Day 89)

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

> [!example]- Reference 1 · AndProduct.java
> ```java
> import java.util.Scanner;
>
>  class AndProduct {
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         solve(in);
>         in.close();
>     }
>
>     public static void solve(Scanner in){
>         long a,b,count,ans,athbit,bthBit;
> 		a = in.nextLong();
> 		b = in.nextLong();
> 		ans = 0L;
> 		int bits = (int)(Math.log(b)/Math.log(2));
> 		for (int j = 0; j <= bits; j++) {
> 			count = 1L << j;
> 			athbit = a & count;
> 			bthBit = b & count;
> 			if(athbit != 0 && bthBit != 0 && (b-a) <=count){
> 				ans = ans | count;
> 			}
> 		}
> 		System.out.println(ans);
>     }
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/and-product-English-8dd5a868.pdf|and-product-English-8dd5a868.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/and-product-English-8dd5a868.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2089%20Solutions/and-product-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 89 Solutions/and-product-English.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2089%20Solutions/AndProduct.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 89 Solutions/AndProduct.java
