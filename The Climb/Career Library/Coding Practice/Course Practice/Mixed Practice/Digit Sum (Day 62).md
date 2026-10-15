---
kind: "coding-problem"
title: "Digit Sum (Day 62)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 62 Solutions/DigitSum.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Digit Sum (Day 62)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

We define super digit of an integer x using the following rules:
Given an integer, we need to find the super digit of the integer.

If x has only 1 digit, then its super digit is x.
Otherwise, the super digit of x is equal to the super digit of the sum of the digits of x.
For example, the super digit of 9875 will be calculated as:
	super_digit(9875)   	9+8+7+5 = 29 
	super_digit(29) 		2 + 9 = 11
	super_digit(11)		1 + 1 = 2
	super_digit(2)			= 2  
You are given two numbers n and k. 
The number p is created by concatenating the number n, k times. 
Continuing the above example where n=9875, assume your value k=4. 
Your initial p=9875 9875 9875 9875 (spaces added for clarity).
    superDigit(p) = superDigit(9875987598759875)
                  5+7+8+9+5+7+8+9+5+7+8+9+5+7+8+9 = 116
    superDigit(p) = superDigit(116)
                  1+1+6 = 8
    superDigit(p) = superDigit(8)
	
All of the digits of p sum to 116. The digits of  116 sum to 8. 8 is only one digit, so it's the super digit.

Input Format:
The first line contains two space separated integers,  n and k.
Output Format:
Return the super digit of p, where p is created as described above.

Sample Input1:
148 3
Sample Output1:
3
Explanation1:
Here n=148 and k=3, so P=148148148.

super_digit(P) = super_digit(148148148) 
               = super_digit(1+4+8+1+4+8+1+4+8)
               = super_digit(39)
               = super_digit(3+9)
               = super_digit(12)
               = super_digit(1+2)
               = super_digit(3)
               = 3.

Sample Input2:
9875 4
Sample Output2:
8


========= Testcases Program-3 =========
case =1
input =12345 7
output =6

case =2
input =525 5
output =6

case =3
input =148 3
output =3

case =4
input =9875 4
output =8

case =5
input =123 3
output =3

case =6
input =999 99
output =9

case =7
input =98963 100
output =8

case =8
input =593 10
output =8

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · DigitSum.java
> ```java
> /*
> We define super digit of an integer x using the following rules:
> Given an integer, we need to find the super digit of the integer.
>
> If x has only 1 digit, then its super digit is x.
> Otherwise, the super digit of x is equal to the super digit of the sum of the digits of x.
> For example, the super digit of 9875 will be calculated as:
> 	super_digit(9875)   	9+8+7+5 = 29 
> 	super_digit(29) 		2 + 9 = 11
> 	super_digit(11)		1 + 1 = 2
> 	super_digit(2)			= 2  
> You are given two numbers n and k. 
> The number p is created by concatenating the number n, k times. 
> Continuing the above example where n=9875, assume your value k=4. 
> Your initial p=9875 9875 9875 9875 (spaces added for clarity).
>     superDigit(p) = superDigit(9875987598759875)
>                   5+7+8+9+5+7+8+9+5+7+8+9+5+7+8+9 = 116
>     superDigit(p) = superDigit(116)
>                   1+1+6 = 8
>     superDigit(p) = superDigit(8)
> 	
> All of the digits of p sum to 116. The digits of  116 sum to 8. 8 is only one digit, so it's the super digit.
>
> Input Format:
> The first line contains two space separated integers,  n and k.
> Output Format:
> Return the super digit of p, where p is created as described above.
>
> Sample Input1:
> 148 3
> Sample Output1:
> 3
> Explanation1:
> Here n=148 and k=3, so P=148148148.
>
> super_digit(P) = super_digit(148148148) 
>                = super_digit(1+4+8+1+4+8+1+4+8)
>                = super_digit(39)
>                = super_digit(3+9)
>                = super_digit(12)
>                = super_digit(1+2)
>                = super_digit(3)
>                = 3.
>
> Sample Input2:
> 9875 4
> Sample Output2:
> 8
>
>
> ========= Testcases Program-3 =========
> case =1
> input =12345 7
> output =6
>
> case =2
> input =525 5
> output =6
>
> case =3
> input =148 3
> output =3
>
> case =4
> input =9875 4
> output =8
>
> case =5
> input =123 3
> output =3
>
> case =6
> input =999 99
> output =9
>
> case =7
> input =98963 100
> output =8
>
> case =8
> input =593 10
> output =8
>
> 		   
> */
>
> import java.util.*;
> import java.math.*;
>
> public class DigitSum {
>
> 	static String solve(String x) {
> 		if(x.length()==1)
> 			return x;
> 		long s=0;
> 		for(int i=0;i<x.length();i++)
> 			s+=x.charAt(i)-48;
> 		return solve(String.valueOf(s));
>
> 	}
>  
> 	public static void main(String [] args) {
> 		Scanner scn = new Scanner(System.in);
> 		String t = scn.next();
> 		long k = scn.nextLong();
> 		long s=0;
> 		for(int i=0;i<t.length();i++)
> 			s+=t.charAt(i)-48;
> 		s*=k;
> 		System.out.println(DigitSum.solve(String.valueOf(s)));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2062%20Solutions/DigitSum.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 62 Solutions/DigitSum.java
