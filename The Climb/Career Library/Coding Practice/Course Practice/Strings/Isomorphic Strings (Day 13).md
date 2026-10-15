---
kind: "coding-problem"
title: "Isomorphic Strings (Day 13)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day13 Solutions/IsomorphicStrings.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Isomorphic Strings (Day 13)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given two strings s and t, determine if they are isomorphic.

Two strings are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

Example 1:

Input: s = "egg", t = "add"
Output: true
Example 2:

Input: s = "foo", t = "bar"
Output: false
Example 3:

Input: s = "paper", t = "title"
Output: true
Note:
You may assume both s and t have the same length.


The idea is that we need to map a char to another one, for example, "egg" and "add", we need to constract the mapping 'e' -> 'a' and 'g' -> 'd'. Instead of directly mapping 'e' to 'a', another way is to mark them with same value, for example, 'e' -> 1, 'a'-> 1, and 'g' -> 2, 'd' -> 2, this works same.

So we use two arrays here m1 and m2, initialized space is 256 (Since the whole ASCII size is 256, 128 also works here). Traverse the character of both s and t on the same position, if their mapping values in m1 and m2 are different, means they are not mapping correctly, returen false; else we construct the mapping, since m1 and m2 are both initialized as 0, we want to use a new value when i == 0, so i + 1 works here.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · IsomorphicStrings.java
> ```java
> /*
>  * 
>  Given two strings s and t, determine if they are isomorphic.
>
> Two strings are isomorphic if the characters in s can be replaced to get t.
>
> All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.
>
> Example 1:
>
> Input: s = "egg", t = "add"
> Output: true
> Example 2:
>
> Input: s = "foo", t = "bar"
> Output: false
> Example 3:
>
> Input: s = "paper", t = "title"
> Output: true
> Note:
> You may assume both s and t have the same length.
>
>
> The idea is that we need to map a char to another one, for example, "egg" and "add", we need to constract the mapping 'e' -> 'a' and 'g' -> 'd'. Instead of directly mapping 'e' to 'a', another way is to mark them with same value, for example, 'e' -> 1, 'a'-> 1, and 'g' -> 2, 'd' -> 2, this works same.
>
> So we use two arrays here m1 and m2, initialized space is 256 (Since the whole ASCII size is 256, 128 also works here). Traverse the character of both s and t on the same position, if their mapping values in m1 and m2 are different, means they are not mapping correctly, returen false; else we construct the mapping, since m1 and m2 are both initialized as 0, we want to use a new value when i == 0, so i + 1 works here.
>
>  */
> package Elite2020;
>
> import java.util.Scanner;
>
> public class IsomorphicStrings {
>
> 	public static boolean isIsomorphic (String s, String t) {
>         int[] m1 = new int[256];
>         int[] m2 = new int[256];
>         int n = s.length();
>         for (int i = 0; i < n; i++) {
>             if (m1[s.charAt(i)] != m2[t.charAt(i)]) return false;
>             m1[s.charAt(i)] = i + 1;
>             m2[t.charAt(i)] = i + 1;
>         }
>         return true;
>     }
> 	
> 	 public static void main(String args[] ) {
> 		 Scanner sc = new Scanner(System.in);
> 			String s=sc.next();
> 			String t=sc.next();
>
>
> 		    System.out.println(isIsomorphic(s,t));
> 	}
>
> 	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day13%20Solutions/IsomorphicStrings.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day13 Solutions/IsomorphicStrings.java
