---
kind: "coding-problem"
title: "Remove Consecutive Duplicates (Day 40)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 40 Solutions/RemoveConsecutiveDuplicates.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Remove Consecutive Duplicates (Day 40)

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

> [!example]- Reference 1 · RemoveConsecutiveDuplicates.java
> ```java
>
> import java.util.Scanner;
>
> /*
>  * 
> Given a string S, remove all the consecutive duplicates. 
> keep one character and remove all subsequent same characters.
>
>
>
> Sample Input: 
> rraabbccdf
>
> Sample Output: 
> rabcdf
>
>
> =============================================================
>
> case=1
> input=tessellator
> output=teselator
>
> case=2
> input=interstellar
> output=interstelar
>
> case=3
> input=killbillkillbill
> output=kilbilkilbil
>
> case=4
> input=jjjjwwjwxxxaaaebeeiii
> output=jwjwxaebei
>
> case=5
> input=abcdefghabcdefgh
> output=abcdefghabcdefgh
>
> case=6
> input=ililililllllllliiiiililiililil
> output=ililililililililil
>
>  * 
>  */
> public class RemoveConsecutiveDuplicates {
>
> 	// Recursively removes consecutive duplicates from str and returns
> 	// new string.
> 	static String removeDup(String str) {
> 		// If length of string is 1 or 0
> 		if (str.length() == 0 || str.length() == 1)
> 			return str;
>
> 		// Remove leftmost same characters and recur for remaining
> 		// string
> 		if (str.charAt(0) == str.charAt(1)) {
> 			// last_removed = str.charAt(0);
> 			while (str.length() > 1 && str.charAt(0) == str.charAt(1))
> 				str = str.substring(1, str.length());
> 			return removeDup(str);
> 		}
>
> 		// At this point, the first character is definitely different
> 		// from its adjacent. Ignore first character and recursively
> 		// remove characters from remaining string
> 		String rem_str = removeDup(str.substring(1, str.length()));
>
> 		// If the two first characters of str and rem_str don't match,
> 		// append first character of str before the first character of
> 		// rem_str
> 		return (str.charAt(0) + rem_str);
> 	}
>
> 	/* main program */
> 	public static void main(String args[]) {
> 		Scanner sc = new Scanner(System.in);
> 		String str = sc.nextLine();
> 		System.out.println(removeDup(str));
>
> 	}
>
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2040%20Solutions/RemoveConsecutiveDuplicates.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 40 Solutions/RemoveConsecutiveDuplicates.java
