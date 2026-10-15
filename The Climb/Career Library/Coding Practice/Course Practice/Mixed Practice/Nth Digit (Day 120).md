---
kind: "coding-problem"
title: "Nth Digit (Day 120)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 120 Solutions/NthDigit.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Nth Digit (Day 120)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given positive natural numbers are 1,2,3,4,5,6,7,8,9,10,11,12,13.....
You are given an integer P.
Your task is to find the digit at position-P in the natural number series.

Note:  P < 2^31.

Input Format:
-------------
An integer P.

Output Format:
--------------
Print a digit, at Position P.


Sample Input-1:
---------------
4

Sample Output-1:
----------------
4

Sample Input-1:
---------------
15

Sample Output-1:
----------------
2


### Explanation

------------
The digit at position 15 from the natural number series:
1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11,12,13,.....
After number 9, digit at position-10 is 1, digit at position-11 is 0, 
digit at position-12 is 1, digit at position-13 is 1,  
digit at position-14 is 1, digit at position-15 is 2.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · NthDigit.java
> ```java
> /*
> Given positive natural numbers are 1,2,3,4,5,6,7,8,9,10,11,12,13.....
> You are given an integer P.
> Your task is to find the digit at position-P in the natural number series.
>
> Note:  P < 2^31.
>
> Input Format:
> -------------
> An integer P.
>
> Output Format:
> --------------
> Print a digit, at Position P.
>
>
> Sample Input-1:
> ---------------
> 4
>
> Sample Output-1:
> ----------------
> 4
>
> Sample Input-1:
> ---------------
> 15
>
> Sample Output-1:
> ----------------
> 2
>
> Explanation:
> ------------
> The digit at position 15 from the natural number series:
> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11,12,13,.....
> After number 9, digit at position-10 is 1, digit at position-11 is 0, 
> digit at position-12 is 1, digit at position-13 is 1,  
> digit at position-14 is 1, digit at position-15 is 2.
>  
> */
>
> import java.util.*;
> class NthDigit {
> public int findNthDigit(int n) {
> 		int len = 1;
> 		long count = 9;
> 		int start = 1;
>
> 		while (n > len * count) {
> 			n -= len * count;
> 			len += 1;
> 			count *= 10;
> 			start *= 10;
> 		}
>
> 		start += (n - 1) / len;
> 		String s = Integer.toString(start);
> 		return Character.getNumericValue(s.charAt((n - 1) % len));
> 	}
> 	
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		int n=sc.nextInt();
> 		System.out.println(new NthDigit().findNthDigit(n));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20120%20Solutions/NthDigit.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 120 Solutions/NthDigit.java
