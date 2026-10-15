---
kind: "coding-problem"
title: "new-year-chaos (Day 83)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 83 Solutions/new-year-chaos-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 83 Solutions/NewYearChaos.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# new-year-chaos (Day 83)

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

> [!example]- Reference 1 · NewYearChaos.java
> ```java
> import java.io.*;
> import java.util.*;
> import java.text.*;
> import java.math.*;
> import java.util.regex.*;
>
> public class NewYearChaos {
>
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
> 		int n = in.nextInt();
> 		int q[] = new int[n+1];
> 		for(int q_i=1; q_i <= n; q_i++){
> 			q[q_i] = in.nextInt();
> 		}
> 		// your code goes here
> 		int result = 0;
> 		boolean chaotic = false;
> 		boolean done = false;
> 		int[] bribe = new int[n+1];
> 		
> 		while(!done) {
> 			done = true;
> 			for(int i = 1; i < n; i++) {
> 				if(q[i] > q[i+1]) {
> 					bribe[q[i]]++;
> 					if(bribe[q[i]] > 2) {
> 						System.out.println("Too chaotic");
> 						chaotic = true;
> 						done = true;
> 						break;
> 					} else {
> 						result++;
> 						int temp = q[i];
> 						q[i] = q[i+1];
> 						q[i+1] = temp;
> 						done = false;
> 					}
> 				}
> 			}
> 		}
> 		
> 		if(!chaotic)
> 			System.out.println(result);
> 		in.close();
>     }
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/new-year-chaos-English-3a7e7e3c.pdf|new-year-chaos-English-3a7e7e3c.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/new-year-chaos-English-3a7e7e3c.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2083%20Solutions/new-year-chaos-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 83 Solutions/new-year-chaos-English.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2083%20Solutions/NewYearChaos.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 83 Solutions/NewYearChaos.java
