---
kind: "coding-problem"
title: "Lego Blocks (Day 76)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 76 Solutions/LegoBlocks.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Lego Blocks (Day 76)

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

> [!example]- Reference 1 · LegoBlocks.java
> ```java
> /* Enter your code here. Read input from STDIN. Print output to STDOUT */
>
> import java.util.Scanner;
>
> public class LegoBlocks {
> 	
> 	public static long MOD = 1000000007;
> 	
> 	public long power(long x, int y) {
> 	    long t;
> 	    if (y == 0)
> 	        return 1;
> 	    
> 	    t = power(x, y/2);
> 	    
> 	    if (y % 2 == 0)
> 	        return (t * t) % MOD;
> 	    else
> 	        return (((x * t) % MOD) * t) % MOD;
> 	}
> 	
> 	public void calculate() {
> 		Scanner sc = new Scanner(System.in);
> 		int N = sc.nextInt();
> 		int M = sc.nextInt();
> 		
> 		int i, j;
>
> 		long[] a = new long[M + 1];
> 		long[] b = new long[M + 1];
> 		long[] c = new long[M + 1];
>
> 		c[0] = 1;
> 		for (i = 1; i <= M; ++i) {
> 			c[i] = 0;
> 			if (i >= 1)
> 				c[i] = (c[i] + c[i - 1]) % MOD;
> 			if (i >= 2)
> 				c[i] = (c[i] + c[i - 2]) % MOD;
> 			if (i >= 3)
> 				c[i] = (c[i] + c[i - 3]) % MOD;
> 			if (i >= 4)
> 				c[i] = (c[i] + c[i - 4]) % MOD;
> 			
> 		}
> 		
> 		for (i = 0; i <= M; ++i) {
> 			b[i] = power(c[i], N);
> 		}
>
> 		long s;
> 		for (i = 1; i <= M; ++i) {
> 			s = 0;
> 			for (j = 1; j <= i - 1; ++j)
> 				s = (s + (a[j] * b[i - j]) % MOD) % MOD;
> 			
> 			if (b[i] < s)
> 				a[i] = b[i] + MOD - s;
> 			else
> 				a[i] = b[i] - s;
> 		}
> 		
> 		System.out.println(a[M]);
> 	}
> 	
> 	public static void main(String[] args) {
> 		LegoBlocks lb = new LegoBlocks();
> 		lb.calculate();
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2076%20Solutions/LegoBlocks.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 76 Solutions/LegoBlocks.java
