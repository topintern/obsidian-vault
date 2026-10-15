---
kind: "coding-problem"
title: "Palindromic Substrings (Day 35)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 35 Solutions/PalindromicSubstrings.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Palindromic Substrings (Day 35)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You have given a task,
to count number of substrings which are pallindromes from a given String.

Example 1:
    Input= abc
    Output= 3
    Explanation= Three substrings are pallindrome: "a", "b", "c".
 

Example 2:
    Input= aaa
    Output= 6
    Explanation= Six substrings are pallindrome: "a", "a", "a", "aa", "aa", "aaa".

=====TestCases========
case =1
input =redivider
output =13

case =2
input =tattarattat
output =22

case =3
input =aaaaaa
output =21

case =4
input =ababbbbaba
output =23

case =5
input =abcdefghijklmnopqrstuvwxyz
output =26

case =6
input =ababababaxyzyxxxyx
output =41

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · PalindromicSubstrings.java
> ```java
> /*
>
> You have given a task,
> to count number of substrings which are pallindromes from a given String.
>
> Example 1:
>     Input= abc
>     Output= 3
>     Explanation= Three substrings are pallindrome: "a", "b", "c".
>  
>
> Example 2:
>     Input= aaa
>     Output= 6
>     Explanation= Six substrings are pallindrome: "a", "a", "a", "aa", "aa", "aaa".
>
> =====TestCases========
> case =1
> input =redivider
> output =13
>
> case =2
> input =tattarattat
> output =22
>
> case =3
> input =aaaaaa
> output =21
>
> case =4
> input =ababbbbaba
> output =23
>
> case =5
> input =abcdefghijklmnopqrstuvwxyz
> output =26
>
> case =6
> input =ababababaxyzyxxxyx
> output =41
>
> */
>
> import java.util.Scanner;
>
> public class PalindromicSubstrings {
>
>     static int count = 0;
>     
>     public static int countSubstrings(String s) {
>         if (s == null || s.length() == 0) return 0;
>         
>         for (int i = 0; i < s.length(); i++) { // i is the mid point
>             extendPalindrome(s, i, i); // odd length;
>             extendPalindrome(s, i, i + 1); // even length
>         }
>         
>         return count;
>     }
>     
>     private static void extendPalindrome(String s, int left, int right) {
>         while (left >=0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
>             count++; left--; right++;
>         }
>     }
>     
>     public static void main(String args[] ) {
> 		 Scanner sc = new Scanner(System.in);
> 			String str=sc.next();
>
> 		    System.out.println(countSubstrings(str));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2035%20Solutions/PalindromicSubstrings.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 35 Solutions/PalindromicSubstrings.java
