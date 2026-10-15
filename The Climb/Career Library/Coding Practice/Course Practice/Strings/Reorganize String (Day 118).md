---
kind: "coding-problem"
title: "Reorganize String (Day 118)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 118 Solutions/ReorganizeString.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Reorganize String (Day 118)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You are provided a string of characters(lowercase only),
You can chnage the order of the characters of the string.
After changing the order, the resultant string should be 
no two immidiate characters equal.

Return true, if you are able to find such resultant string, 
Otherwise false.

Input Format:
-------------
A String S

Output Format:
--------------
Print a boolean value.


Sample Input-1:
---------------
aaabd

Sample Output-1:
----------------
true

Sample Input-2:
---------------
aaab

Sample Output-2:
----------------
false

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ReorganizeString.java
> ```java
> /*
> You are provided a string of characters(lowercase only),
> You can chnage the order of the characters of the string.
> After changing the order, the resultant string should be 
> no two immidiate characters equal.
>
> Return true, if you are able to find such resultant string, 
> Otherwise false.
>
> Input Format:
> -------------
> A String S
>
> Output Format:
> --------------
> Print a boolean value.
>
>
> Sample Input-1:
> ---------------
> aaabd
>
> Sample Output-1:
> ----------------
> true
>
> Sample Input-2:
> ---------------
> aaab
>
> Sample Output-2:
> ----------------
> false
>
> */
> import java.util.*;
>
> class ReorganizeString {
>  public String reorganizeString(String S) {
>         int[] hash = new int[26];
>         for (int i = 0; i < S.length(); i++) {
>             hash[S.charAt(i) - 'a']++;
>         } 
>         int max = 0, letter = 0;
>         for (int i = 0; i < hash.length; i++) {
>             if (hash[i] > max) {
>                 max = hash[i];
>                 letter = i;
>             }
>         }
>         if (max > (S.length() + 1) / 2) {
>             return ""; 
>         }
>         char[] res = new char[S.length()];
>         int idx = 0;
>         while (hash[letter] > 0) {
>             res[idx] = (char) (letter + 'a');
>             idx += 2;
>             hash[letter]--;
>         }
>         for (int i = 0; i < hash.length; i++) {
>             while (hash[i] > 0) {
>                 if (idx >= res.length) {
>                     idx = 1;
>                 }
>                 res[idx] = (char) (i + 'a');
>                 idx += 2;
>                 hash[i]--;
>             }
>         }
>         return String.valueOf(res);
>     }
>
> 	public static void main( String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		String s=sc.next();
> 		String res=new ReorganizeString().reorganizeString(s);
> 		if(res.length()>0)
> 			System.out.println("true");
> 		else
> 			System.out.println("false");
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20118%20Solutions/ReorganizeString.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 118 Solutions/ReorganizeString.java
