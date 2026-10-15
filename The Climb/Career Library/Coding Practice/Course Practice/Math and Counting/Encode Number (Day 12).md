---
kind: "coding-problem"
title: "Encode Number (Day 12)"
collection: "Course Practice"
topic: "Math and Counting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 12 Solutions/EncodeNumber.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Encode Number (Day 12)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a non-negative integer num, Return its encoding string.

The encoding is done by converting the integer to a string using a secret function that you should deduce from the following table:
n f(n)
0 
1 0
2 1
3 00
4 01
5 10
6 11
7 000

Example 1:
	Input=	23
	Output=1000

Example 2:
	Input=	107
	Output=101100


----TestCase----
case =1
input =515
output =000000100

case =2
input =2876
output =01100111101

case =3
input =345
output =01011010

case =4
input =187
output =0111100

case =5
input =48
output =10001

case =6
input =35
output =00100

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · EncodeNumber.java
> ```java
> /*
>  
>  Given a non-negative integer num, Return its encoding string.
>
> The encoding is done by converting the integer to a string using a secret function that you should deduce from the following table:
> n f(n)
> 0 
> 1 0
> 2 1
> 3 00
> 4 01
> 5 10
> 6 11
> 7 000
>
> Example 1:
> 	Input=	23
> 	Output=1000
>
> Example 2:
> 	Input=	107
> 	Output=101100
>
>
> ----TestCase----
> case =1
> input =515
> output =000000100
>
> case =2
> input =2876
> output =01100111101
>
> case =3
> input =345
> output =01011010
>
> case =4
> input =187
> output =0111100
>
> case =5
> input =48
> output =10001
>
> case =6
> input =35
> output =00100
>  
> */
>
> import java.util.Scanner;
>
> public class EncodeNumber {
> 	
> 	 public static String encode(int n) {
> 	        return n > 0 ? encode((n - 1) / 2) + "10".charAt(n % 2) : "";
> 	    }
> 	 
> 	 public static void main(String args[] ) {
> 		 Scanner sc = new Scanner(System.in);
> 			int n=sc.nextInt();
>
> 		    System.out.println(encode(n));
> 	}
>
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2012%20Solutions/EncodeNumber.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 12 Solutions/EncodeNumber.java
