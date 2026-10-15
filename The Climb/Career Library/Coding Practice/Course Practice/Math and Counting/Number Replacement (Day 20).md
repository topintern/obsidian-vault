---
kind: "coding-problem"
title: "Number Replacement (Day 20)"
collection: "Course Practice"
topic: "Math and Counting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 20 Solutions/NumberReplacement.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Number Replacement (Day 20)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a positive integer n and you can do operations as follow:

If n is even, replace n with n/2.
If n is odd, you can replace n with either n + 1 or n - 1.
What is the minimum number of replacements needed for n to become 1?

Example 1:
	Input:	8
	Output:	 3
	Explanation:
		8 -> 4 -> 2 -> 1

Example 2:
	Input:	7
	Output:	 4
	Explanation:
		7 -> 8 -> 4 -> 2 -> 1
		or
		7 -> 6 -> 3 -> 2 -> 1

-----------TestCases---------
case =1
input =76356789
output =37

case =2
input =87566
output =22

case =3
input =123456
output =20

case =4
input =2020
output =13

case =5
input =156
output =9

case =6
input =18
output =5

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · NumberReplacement.java
> ```java
> /*
> Given a positive integer n and you can do operations as follow:
>
> If n is even, replace n with n/2.
> If n is odd, you can replace n with either n + 1 or n - 1.
> What is the minimum number of replacements needed for n to become 1?
>
> Example 1:
> 	Input:	8
> 	Output:	 3
> 	Explanation:
> 		8 -> 4 -> 2 -> 1
>
> Example 2:
> 	Input:	7
> 	Output:	 4
> 	Explanation:
> 		7 -> 8 -> 4 -> 2 -> 1
> 		or
> 		7 -> 6 -> 3 -> 2 -> 1
>
> -----------TestCases---------
> case =1
> input =76356789
> output =37
>
> case =2
> input =87566
> output =22
>
> case =3
> input =123456
> output =20
>
> case =4
> input =2020
> output =13
>
> case =5
> input =156
> output =9
>
> case =6
> input =18
> output =5
>
> */
> import java.util.*;
> class NumberReplacement{
> 	public static int numberReplacement(int n) {
> 	    int c = 0;
> 	    while (n != 1) {
> 		if ((n & 1) == 0) {
> 		    n >>>= 1;
> 		} else if (n == 3 || Integer.bitCount(n + 1) > Integer.bitCount(n - 1)) {
> 		    --n;
> 		} else {
> 		    ++n;
> 		}
> 		++c;
> 	    }
> 	    return c;
> 	}
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		int n=sc.nextInt();
> 		System.out.println(numberReplacement(n));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2020%20Solutions/NumberReplacement.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 20 Solutions/NumberReplacement.java
