---
kind: "coding-problem"
title: "Fibonacci String (Day 116)"
collection: "Course Practice"
topic: "Dynamic Programming"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 116 Solutions/FibonacciString.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Fibonacci String (Day 116)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Pramod is working on Strings consist of digits only. 
He wants to findout, whether the given string can form Fibonacci sequence or not.

A String can form a Fibonacci Sequence, if it contains at least three numbers,
and numbers are in the following order:
first, second, third  = first + second, fourth = third + second, .. so on.

Return true, if the given string can form fibonacci sequence,
otherwise, return false.

Note: Numbers in the fibonacci sequence contains no leading 0's.
for example, 2, 03,5 or 2,3,05 or 02,3,5 are not valid.

Input Format:
-------------
A String consist of digits only

Output Format:
--------------
Print a boolean value as result.


Sample Input-1:
---------------
23581321

Sample Output-1:
----------------
true


### Explanation: 

------------
Fibonacci Sequence is : 2, 3, 5, 8, 13, 21
2, 3, 2+3=5, 3+5=8, 5+8=13, 8+13=21.

Sample Input-2:
---------------
199100199

Sample Output-2:
----------------
true


### Explanation: 

------------
Fibonacci Sequence is : 1 99 100 199
1, 99, 1+99=100, 99+100=199.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · FibonacciString.java
> ```java
> /*
> Pramod is working on Strings consist of digits only. 
> He wants to findout, whether the given string can form Fibonacci sequence or not.
>
> A String can form a Fibonacci Sequence, if it contains at least three numbers,
> and numbers are in the following order:
> first, second, third  = first + second, fourth = third + second, .. so on.
>
> Return true, if the given string can form fibonacci sequence,
> otherwise, return false.
>
> Note: Numbers in the fibonacci sequence contains no leading 0's.
> for example, 2, 03,5 or 2,3,05 or 02,3,5 are not valid.
>
> Input Format:
> -------------
> A String consist of digits only
>
> Output Format:
> --------------
> Print a boolean value as result.
>
>
> Sample Input-1:
> ---------------
> 23581321
>
> Sample Output-1:
> ----------------
> true
>
> Explanation: 
> ------------
> Fibonacci Sequence is : 2, 3, 5, 8, 13, 21
> 2, 3, 2+3=5, 3+5=8, 5+8=13, 8+13=21.
>
> Sample Input-2:
> ---------------
> 199100199
>
> Sample Output-2:
> ----------------
> true
>
> Explanation: 
> ------------
> Fibonacci Sequence is : 1 99 100 199
> 1, 99, 1+99=100, 99+100=199.
>
> */
>
> import java.util.*;
>
> public class FibonacciString {
>     public boolean isFibonacciString(String num) {
>         int n = num.length();
>         for (int i = 1; i <= n / 2; ++i)
>             for (int j = 1; Math.max(j, i) <= n - i - j; ++j)
>                 if (isValid(i, j, num)) return true;
>         return false;
>     }
>     private boolean isValid(int i, int j, String num) {
>         if (num.charAt(0) == '0' && i > 1) return false;
>         if (num.charAt(i) == '0' && j > 1) return false;
>         String sum;
>         Long x1 = Long.parseLong(num.substring(0, i));
>         Long x2 = Long.parseLong(num.substring(i, i + j));
>         for (int start = i + j; start != num.length(); start += sum.length()) {
>             x2 = x2 + x1;
>             x1 = x2 - x1;
>             sum = x2.toString();
>             if (!num.startsWith(sum, start)) return false;
>         }
>         return true;
>     }
> 	
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		String s=sc.next();
> 		System.out.println(new FibonacciString().isFibonacciString(s));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20116%20Solutions/FibonacciString.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 116 Solutions/FibonacciString.java
