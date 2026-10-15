---
kind: "coding-problem"
title: "Four Keys (Day 14)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 14 Solutions/FourKeys.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Four Keys (Day 14)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Imagine you have a special keyboard with the following keys:

Key 1: (A): Print one 'A' on screen.

Key 2: (Ctrl-A): Select the whole screen.

Key 3: (Ctrl-C): Copy selection to buffer.

Key 4: (Ctrl-V): Print buffer on screen appending it after what has already been printed.

Now, you can only press the keyboard for N times (with the above four keys), find out the maximum numbers of 'A' you can print on screen.

Example 1:
Input:3
Output: 3

### Explanation: 

We can at most get 3 A's on screen by pressing following key sequence:
A, A, A

Example 2:
Input: 7
Output: 9

### Explanation: 

We can at most get 9 A's on screen by pressing following key sequence:
A, A, A, Ctrl A, Ctrl C, Ctrl V, Ctrl V

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · FourKeys.java
> ```java
> /*
>  * 
>  * 
>  Imagine you have a special keyboard with the following keys:
>
> Key 1: (A): Print one 'A' on screen.
>
> Key 2: (Ctrl-A): Select the whole screen.
>
> Key 3: (Ctrl-C): Copy selection to buffer.
>
> Key 4: (Ctrl-V): Print buffer on screen appending it after what has already been printed.
>
> Now, you can only press the keyboard for N times (with the above four keys), find out the maximum numbers of 'A' you can print on screen.
>
> Example 1:
> Input:3
> Output: 3
> Explanation: 
> We can at most get 3 A's on screen by pressing following key sequence:
> A, A, A
>
> Example 2:
> Input: 7
> Output: 9
> Explanation: 
> We can at most get 9 A's on screen by pressing following key sequence:
> A, A, A, Ctrl A, Ctrl C, Ctrl V, Ctrl V
>
>
>
>
>
>  */
>
> package Elite2020;
>
> import java.util.Scanner;
>
> public class FourKeys {
> 	 public static int maxA(int n) {
> 	        int[] dp = new int[n + 1];
> 	        for (int i = 0; i <= n; i++) {
> 	            dp[i] = i;
> 	            for (int j = 1; j <= i - 3; j++)
> 	                dp[i] = Math.max(dp[i], dp[j] * (i - j - 1));
> 	        }
> 	        return dp[n];
> 	    }
> 	
> 	 public static void main(String args[] ) {
> 		 Scanner sc = new Scanner(System.in);
> 			int n=sc.nextInt();
> 		    System.out.println(maxA(n));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2014%20Solutions/FourKeys.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 14 Solutions/FourKeys.java
