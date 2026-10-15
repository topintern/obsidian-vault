---
kind: "coding-problem"
title: "Twins (Day 65)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 65 Solutions/Twins.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Twins (Day 65)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Lia is fascinated by anything she considers to be a twin. 
She calls a pairs of positive integers, i and j, twins if:
-They are both prime. A prime number is an integer greater than 1 that has no positive divisors 
other than 1 and itself.
-Their absolute difference is exactly equal to  2(i.e.|j-i|=2).

Given an inclusive interval of integers from n to m, 
can you help Lia find the number of pairs of twins there are in the interval 
Note that pairs (i,j) and (j,i) are considered to be the same pair.

Input Format:
Two space-separated integers describing the respective values of  n and m.

Output Format:
Print a single integer denoting the number of pairs of twins.

Sample Input1:
3 13
Sample Output1:
3
Explanation1:
There are three pairs of twins: (3,5),(5,7) and (7,9).


========= Testcases Program-1 =========
case =1
input =3 13
output =3

case =2
input =4 5
output =0

case =3
input =1 1000
output =35

case =4
input =13 956
output =32

case =5
input =281 586
output =8

case =6
input =45 639
output =22

case =7
input =869782 1082556
output =1516

case =8
input =3449962 3573724
output =718

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Twins.java
> ```java
> /*
> Lia is fascinated by anything she considers to be a twin. 
> She calls a pairs of positive integers, i and j, twins if:
> -They are both prime. A prime number is an integer greater than 1 that has no positive divisors 
> other than 1 and itself.
> -Their absolute difference is exactly equal to  2(i.e.|j-i|=2).
>
> Given an inclusive interval of integers from n to m, 
> can you help Lia find the number of pairs of twins there are in the interval 
> Note that pairs (i,j) and (j,i) are considered to be the same pair.
>
> Input Format:
> Two space-separated integers describing the respective values of  n and m.
>
> Output Format:
> Print a single integer denoting the number of pairs of twins.
>
> Sample Input1:
> 3 13
> Sample Output1:
> 3
> Explanation1:
> There are three pairs of twins: (3,5),(5,7) and (7,9).
>
>
> ========= Testcases Program-1 =========
> case =1
> input =3 13
> output =3
>
> case =2
> input =4 5
> output =0
>
> case =3
> input =1 1000
> output =35
>
> case =4
> input =13 956
> output =32
>
> case =5
> input =281 586
> output =8
>
> case =6
> input =45 639
> output =22
>
> case =7
> input =869782 1082556
> output =1516
>
> case =8
> input =3449962 3573724
> output =718
>
> */
>
> import java.util.*;
>
> public class Twins {
>     private static boolean isPrime(int num) {
>         if (num < 2) return false;
>         if (num == 2) return true;
>         if (num % 2 == 0) return false;
>         for (int i = 3; i * i <= num; i += 2)
>             if (num % i == 0) return false;
>         return true;
> 	}
>
>     public static void main(String[] args) {
>        Scanner sc= new Scanner(System.in);
>         int m=sc.nextInt();
>         int n=sc.nextInt();
>         int count=0;
>         for(int i=m;i<=n;i++)
>         {
>             boolean a=isPrime(i);
>             boolean b=false;
>             if(a==true  && (i+2)<=n)
>                 {
>                 b=isPrime(i+2);
>                 if(b==true)
>                     count++;
>             }
>         }
>         System.out.println(count);
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2065%20Solutions/Twins.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 65 Solutions/Twins.java
