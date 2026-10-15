---
kind: "coding-problem"
title: "One Edit (Day 3)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 3 Solutions/OneEdit.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# One Edit (Day 3)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Problem

The source has reference code without a separate problem statement. Establish its inputs, expected outputs, and constraints before practising.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · OneEdit.java
> ```java
> package Leetcode;
>
>
> /*
>  * 
>  * 
>  Given two strings s and t, determine if they are both one edit distance apart.
>
> Note: 
>
> There are 3 possiblities to satisify one edit distance apart:
>
> Insert a character into s to get t
> Delete a character from s to get t
> Replace a character of s to get t
> Example 1:
>
> Input: ab acb
> Output: true
> Explanation: We can insert 'c' into s to get t.
> Example 2:
>
> Input: cab ad
> Output: false
> Explanation: We cannot get t from s by only one step.
> Example 3:
>
> Input: 1203 1213
> Output: true
> Explanation: We can replace '0' with '1' to get t.
>
>
>  */
> import java.util.Scanner;
>
> public class OneEdit {
> 	
> 		  public static boolean isOneEditDistance(String s, String t) {
> 		    int ns = s.length();
> 		    int nt = t.length();
>
> 		    // Ensure that s is shorter than t.
> 		    if (ns > nt)
> 		      return isOneEditDistance(t, s);
>
> 		    // The strings are NOT one edit away distance  
> 		    // if the length diff is more than 1.
> 		    if (nt - ns > 1)
> 		      return false;
>
> 		    for (int i = 0; i < ns; i++)
> 		      if (s.charAt(i) != t.charAt(i))
> 		        // if strings have the same length
> 		        if (ns == nt)
> 		          return s.substring(i + 1).equals(t.substring(i + 1));
> 		        // if strings have different lengths
> 		        else
> 		          return s.substring(i).equals(t.substring(i + 1));
>
> 		    // If there is no diffs on ns distance
> 		    // the strings are one edit away only if
> 		    // t has one more character. 
> 		    return (ns + 1 == nt);
> 		  }
> 		  public static void main(String args[] ) {
> 				 Scanner sc = new Scanner(System.in);
> 					String s=sc.next();
> 					String t=sc.next();
>
> 				    System.out.println(isOneEditDistance(s,t));
> 			}
> 		
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%203%20Solutions/OneEdit.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 3 Solutions/OneEdit.java
