---
kind: "coding-problem"
title: "Confusing Number (Day 1)"
collection: "Course Practice"
topic: "Math and Counting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 1/ConfusingNumber.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Confusing Number (Day 1)

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

> [!example]- Reference 1 · ConfusingNumber.java
> ```java
> package Day1;
>
> /*
>  * 
>  * 
> Input: 20
> Output: 6
> Explanation: 
> The confusing numbers are [6,9,10,16,18,19].
> 6 converts to 9.
> 9 converts to 6.
> 10 converts to 01 which is just 1.
> 16 converts to 91.
> 18 converts to 81.
> 19 converts to 61.
>  * 
>  */
>
> import java.util.Scanner;
>
>
> public class ConfusingNumber {
>
> 	
> 	public static int[] valid = {0, 1, 6, 8, 9};
> 	public static int[] reverse = {0, 1, 2, 3, 4, 5, 9, 7, 8, 6};
> 	static int res = 0;
> 	public static int getConfusingNumberCount(int N) {
> 		dfs(0, N);
> 		return res;
> 	}
> 	public static void dfs(int num, int N) {
> 		if (isValid(num)) res++;
> 		for (int i = 0; i < valid.length; i++) {
> 			if (i == 0 && num == 0) continue;
> 			// check overflow
> 			int digit = valid[i];
> 			if ((Integer.MAX_VALUE - digit) / 10 < num || num * 10 + digit > N) continue;
> 			dfs(num * 10 + digit, N);
> 		}
> 	}
> 	public static boolean isValid(int num) {
> 		long rev = 0;
> 		int copy = num;
> 		while (num != 0) {
> 			int digit = num % 10;
> 			rev = rev * 10 + reverse[digit];
> 			num /= 10;
> 		}
> 		return rev != copy;
> 	}
> 	
> 	public static void main(String args[] ) {
> 		 Scanner scan = new Scanner(System.in);
> 			int n=scan.nextInt();
> 		    System.out.println(getConfusingNumberCount(n));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%201/ConfusingNumber.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 1/ConfusingNumber.java
