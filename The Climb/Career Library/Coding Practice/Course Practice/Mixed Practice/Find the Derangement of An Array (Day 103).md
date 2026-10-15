---
kind: "coding-problem"
title: "Find the Derangement of An Array (Day 103)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 103 Solutions/Find the Derangement of An Array - LeetCode.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 103 Solutions/FindDerangement.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Find the Derangement of An Array (Day 103)

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

> [!example]- Reference 1 · FindDerangement.java
> ```java
> import java.util.Scanner;
>
> class FindDerangement {
>     public static int findDerangement(int n) {
>         if (n <= 1) return 0;
>         long dp[] = new long[n + 1];
>         long mod = 1000000007;
>         dp[2] = 1;
>         for (int i = 3; i <= n; i++) {
>             dp[i] = (i - 1) * (dp[i - 1] + dp[i - 2]) % mod;
>         }
>         return (int)dp[n];        
>     }
> 	public static void main(String args[])
> 	{
> 		Scanner sc = new Scanner(System.in);
> 		int n=sc.nextInt();
> 		System.out.println(findDerangement(n));
> 	}
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/Find the Derangement of An Array - Leet Code-365e072a.pdf|Find the Derangement of An Array - Leet Code-365e072a.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/Find the Derangement of An Array - Leet Code-365e072a.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20103%20Solutions/Find%20the%20Derangement%20of%20An%20Array%20-%20LeetCode.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 103 Solutions/Find the Derangement of An Array - LeetCode.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20103%20Solutions/FindDerangement.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 103 Solutions/FindDerangement.java
