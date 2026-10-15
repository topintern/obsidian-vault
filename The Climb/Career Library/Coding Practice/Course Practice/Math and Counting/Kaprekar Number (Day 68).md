---
kind: "coding-problem"
title: "Kaprekar Number (Day 68)"
collection: "Course Practice"
topic: "Math and Counting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 68 Solutions/KaprekarNumber.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Kaprekar Number (Day 68)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

A modified Kaprekar number is a positive whole number with a special property. 
If you square it, then split the number into two integers and sum those integers, 
you have the same value you started with.

Consider a positive whole number n with d digits. 
We square n to arrive at a number that is either 2*d digits long or 2*d-1 digits long.
Split the string representation of the square into two parts, l and r. 
The right hand part, r must be d digits long. The left is the remaining substring. 
Convert those two substrings back to integers, add them and see if you get n.

For example, if n=5, d=1 then square(n)=25. 
We split that into two strings and convert them back to integers 2 and 2. 
We test 2+5=7 != 5, so this is not a modified Kaprekar number. 
If n=9, still d=1, and square(n)=81. This gives us 1+8=9, the original n.

Note: r may have leading zeros.

Given two positive integers p and q where p is lower than q, 
write a program to print the modified Kaprekar numbers in the range between p and q, inclusive.

Input Format:
The first line contains the lower integer limit .
The second line contains the upper integer limit .
Note: Your range should be inclusive of the limits.

Output Format:
Output each modified Kaprekar number in the given range, space-separated on a single line. 
If no modified Kaprekar numbers exist in the given range, print INVALID RANGE.

Sample Input
1
100
Sample Output
1 9 45 55 99

Explanation
1, 9, 45, 55, 99 are the Kaprekar Numbers in the given range.


========= Testcases Program-2 =========
case =1
input =1
100
output =1 9 45 55 99

case =2
input =56
98
output =INVALID RANGE

case =3
input =25
150
output =45 55 99

case =4
input =100
500
output =297

case =5
input =100
1000
output =297 703 999

case =6
input =1
1000
output =1 9 45 55 99 297 703 999

case =7
input =1
10000
output =1 9 45 55 99 297 703 999 2223 2728 4950 5050 7272 7777 9999

case =8
input =1000
100000
output =2223 2728 4950 5050 7272 7777 9999 17344 22222 77778 82656 95121 99999

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · KaprekarNumber.java
> ```java
> /*
> A modified Kaprekar number is a positive whole number with a special property. 
> If you square it, then split the number into two integers and sum those integers, 
> you have the same value you started with.
>
> Consider a positive whole number n with d digits. 
> We square n to arrive at a number that is either 2*d digits long or 2*d-1 digits long.
> Split the string representation of the square into two parts, l and r. 
> The right hand part, r must be d digits long. The left is the remaining substring. 
> Convert those two substrings back to integers, add them and see if you get n.
>
> For example, if n=5, d=1 then square(n)=25. 
> We split that into two strings and convert them back to integers 2 and 2. 
> We test 2+5=7 != 5, so this is not a modified Kaprekar number. 
> If n=9, still d=1, and square(n)=81. This gives us 1+8=9, the original n.
>
> Note: r may have leading zeros.
>
> Given two positive integers p and q where p is lower than q, 
> write a program to print the modified Kaprekar numbers in the range between p and q, inclusive.
>
> Input Format:
> The first line contains the lower integer limit .
> The second line contains the upper integer limit .
> Note: Your range should be inclusive of the limits.
>
> Output Format:
> Output each modified Kaprekar number in the given range, space-separated on a single line. 
> If no modified Kaprekar numbers exist in the given range, print INVALID RANGE.
>
> Sample Input
> 1
> 100
> Sample Output
> 1 9 45 55 99
>
> Explanation
> 1, 9, 45, 55, 99 are the Kaprekar Numbers in the given range.
>
>
> ========= Testcases Program-2 =========
> case =1
> input =1
> 100
> output =1 9 45 55 99
>
> case =2
> input =56
> 98
> output =INVALID RANGE
>
> case =3
> input =25
> 150
> output =45 55 99
>
> case =4
> input =100
> 500
> output =297
>
> case =5
> input =100
> 1000
> output =297 703 999
>
> case =6
> input =1
> 1000
> output =1 9 45 55 99 297 703 999
>
> case =7
> input =1
> 10000
> output =1 9 45 55 99 297 703 999 2223 2728 4950 5050 7272 7777 9999
>
> case =8
> input =1000
> 100000
> output =2223 2728 4950 5050 7272 7777 9999 17344 22222 77778 82656 95121 99999
>
> */
>
> import java.util.*;
>
> public class KaprekarNumber {
>
>     public static void main(String[] args) {
>         /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
>         Scanner sc = new Scanner(System.in);
>         long p = Long.valueOf(sc.nextLine());
>         long q = Long.valueOf(sc.nextLine());
>         boolean found = false;
>         for (long i = p; i <= q; i++) {
>             if (isKaprekar(i)) {
>                 found = true;
>                 System.out.print(i + " ");
>             }
>         }
>         if (!found)
>             System.out.println("INVALID RANGE");
>     }
>     
>     public static boolean isKaprekar(long num) {
>         int d = Long.toString(num).length();
>         String square = Long.toString(num * num);
>         int leftLen = square.length() - d;
>         String first = "0";
>         if (leftLen > 0)
>             first = square.substring(0, leftLen);
>         String second = square.substring(leftLen);
>         return num == (Long.valueOf(first) + Long.valueOf(second));
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2068%20Solutions/KaprekarNumber.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 68 Solutions/KaprekarNumber.java
