---
kind: "coding-problem"
title: "Numof Ways (Day 114)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 114 Solutions/NumofWays.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Numof Ways (Day 114)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You are decorating a side wall with balloons.
You have an unlimited set of ballons of three different colors.

The decoration should have N rows of 3 balloons each. 
You have to make sure that no two adjacent balloons have the same colour.
both vertically and horizontally.

Return the number of ways you can decorate the wall,  
the answer must be computed modulo 10^9 + 7

Input Format:
-------------
An integer N

Output Format:
--------------
Print an integer as outpur, number of ways to decorate.


Sample Input-1:
---------------
1

Sample Output-1:
----------------
12


### Explanation

------------
Suppose the colors are, B, G, R. Given N is 1
RBR	BRB	GRB
RBG	BRG	GRG
RGR	BGR	GBR
RGB	BGB	GBG


Sample Input-2:
---------------
2

Sample Output-2:
----------------
54

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · NumofWays.java
> ```java
> /*
> You are decorating a side wall with balloons.
> You have an unlimited set of ballons of three different colors.
>
> The decoration should have N rows of 3 balloons each. 
> You have to make sure that no two adjacent balloons have the same colour.
> both vertically and horizontally.
>
> Return the number of ways you can decorate the wall,  
> the answer must be computed modulo 10^9 + 7
>
> Input Format:
> -------------
> An integer N
>
> Output Format:
> --------------
> Print an integer as outpur, number of ways to decorate.
>
>
> Sample Input-1:
> ---------------
> 1
>
> Sample Output-1:
> ----------------
> 12
>
> Explanation:
> ------------
> Suppose the colors are, B, G, R. Given N is 1
> RBR	BRB	GRB
> RBG	BRG	GRG
> RGR	BGR	GBR
> RGB	BGB	GBG
>
>
> Sample Input-2:
> ---------------
> 2
>
> Sample Output-2:
> ----------------
> 54
>
>
> */
>
> import java.util.*;
>
> public class NumofWays {	
> 	
> 	public static int numOfWays(int n) {
>         long a121 = 6, a123 = 6, b121, b123, mod = (long)1e9 + 7;
>         for (int i = 1; i < n; ++i) {
>             b121 = a121 * 3 + a123 * 2;
>             b123 = a121 * 2 + a123 * 2;
>             a121 = b121 % mod;
>             a123 = b123 % mod;
>         }
>         return (int)((a121 + a123) % mod);
>     }
> 	
> 		public static void main(String args[] ) {
> 		Scanner scan = new Scanner(System.in);
> 		int n=scan.nextInt();     
> 		System.out.println(numOfWays(n));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20114%20Solutions/NumofWays.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 114 Solutions/NumofWays.java
