---
kind: "coding-problem"
title: "Is Subsequence (Day 40)"
collection: "Course Practice"
topic: "Dynamic Programming"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 40 Solutions/IsSubsequence.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Is Subsequence (Day 40)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given two strings A and B, check if A is subsequence of B.

B is a very long string, and A is a short string 

A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, "def" is a subsequence of "adheazgbf" while "zab" is not).

Example 1:

input:
def
adheazgbf

output:
true

Example 2:

input:
zab
adheazgbf

output:
false
===========================================

public int indexOf(char ch, int strt)

Parameters:
ch :a character.
strt : the index to start the search from.


case=1
input=ramraj
shivramaraju
output=true

case=2
input=akhil
arkahmiul
output=true

case=3
input=reddy
raaaaebbdbbdxzy
output=true

case=4
input=reddy
eaaaarbbdbbdxzy
output=false

case=5
input=mohan
nahom
output=false

case=5
input=nagi
nrghahiygjj
output=false

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · IsSubsequence.java
> ```java
> /*
>  * 
> Given two strings A and B, check if A is subsequence of B.
>
> B is a very long string, and A is a short string 
>
> A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, "def" is a subsequence of "adheazgbf" while "zab" is not).
>
> Example 1:
>
> input:
> def
> adheazgbf
>
> output:
> true
>
> Example 2:
>
> input:
> zab
> adheazgbf
>
> output:
> false
> ===========================================
>
> public int indexOf(char ch, int strt)
>
> Parameters:
> ch :a character.
> strt : the index to start the search from.
>
>
> case=1
> input=ramraj
> shivramaraju
> output=true
>
> case=2
> input=akhil
> arkahmiul
> output=true
>
> case=3
> input=reddy
> raaaaebbdbbdxzy
> output=true
>
> case=4
> input=reddy
> eaaaarbbdbbdxzy
> output=false
>
> case=5
> input=mohan
> nahom
> output=false
>
> case=5
> input=nagi
> nrghahiygjj
> output=false
>
>  */
>
>
>
> import java.util.Scanner;
>
> public class IsSubsequence {
>
> 	public static boolean isSubsequence(String s, String t) {
>         int index = -1;
>         for (char c : s.toCharArray()) {
>             index = t.indexOf(c, index + 1);
>             if (index == -1) return false;
>         }
>         return true;
>     }
> 	
> 	  public static void main(String args[] ) {
> 			 Scanner sc = new Scanner(System.in);
> 				String s=sc.next();
> 				String t=sc.next();
> 			    System.out.println(isSubsequence(s,t));
> 		}
> 	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2040%20Solutions/IsSubsequence.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 40 Solutions/IsSubsequence.java
