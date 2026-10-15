---
kind: "coding-problem"
title: "Lowest Palindrome (Day 85)"
collection: "Course Practice"
topic: "Dynamic Programming"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 85 Solutions/LowestPalindrome.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Lowest Palindrome (Day 85)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

******Testcases*******
case =1
input =6 2
092282
output =082280

case =2
input =9 4
123456789
output =123454321

case =3
input =4 3
1234
output =0220

case =4
input =5 2
13456
output =13431

case =5
input =4 1
0110
output =-1

case =6
input =4 1
3943
output =3443

case =7
input =4 4
3943
output =0000

case =8
input =6 3
092282
output =002200

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · LowestPalindrome.java
> ```java
> /*
> *******Testcases*******
> case =1
> input =6 2
> 092282
> output =082280
>
> case =2
> input =9 4
> 123456789
> output =123454321
>
> case =3
> input =4 3
> 1234
> output =0220
>
> case =4
> input =5 2
> 13456
> output =13431
>
> case =5
> input =4 1
> 0110
> output =-1
>
> case =6
> input =4 1
> 3943
> output =3443
>
> case =7
> input =4 4
> 3943
> output =0000
>
> case =8
> input =6 3
> 092282
> output =002200
>
> */
>
> import java.util.Scanner;
>
> public class LowestPalindrome {
>     public static void main(String[] args) {
>         Scanner scanner = new Scanner(System.in);
>
>         int n = scanner.nextInt();
>         int k = scanner.nextInt();
>         char[] c = scanner.next().toCharArray();
>         boolean[] ch = new boolean[n];
>         for (int i = 0; i < n/2; ++i) {
>             if (c[i] != c[n - i - 1]) {
>                 c[i] = c[n - i - 1] = (char)Math.min(c[i], c[n - i - 1]);
>                 ch[i] = true;
>                 --k;
>             }
>         }
>         if (k < 0) {
>             System.out.println(-1);
>             return;
>         }
>         for (int i = 0; i < n/2; ++i) {
>             if (c[i] != '0') {
>                 if (ch[i] && k > 0) {
>                     c[i] = c[n - i - 1] = '0';
>                     --k;
>                 }
>                 if (!ch[i] && k > 1) {
>                     c[i] = c[n - i - 1] = '0';
>                     k -= 2;
>                 }
>             }
>         }
>         if (n % 2 == 1 && k > 0) {
>             c[n/2] = '0';
>         }
>         System.out.println(new String(c));
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2085%20Solutions/LowestPalindrome.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 85 Solutions/LowestPalindrome.java
