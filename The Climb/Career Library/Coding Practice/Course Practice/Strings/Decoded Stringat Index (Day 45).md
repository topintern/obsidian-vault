---
kind: "coding-problem"
title: "Decoded Stringat Index (Day 45)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 45 Solutions/DecodedStringatIndex.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Decoded Stringat Index (Day 45)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

An enngitd string S is given.  To find and write the dengitd string to a tape, the enngitd string is read one character at a time and the following steps are taken:

If the character read is a letter, that letter is written onto the tape.
If the character read is a digit (say d), the entire current tape is repeatedly written d-1 more times in total.
Now for some enngitd string S, and an index K, find and return the K-th letter (1 indexed) in the dengitd string.


Example 1:

Input: S = "kmit2ngit3", K = 10
Output: "o"

### Explanation: 

The dengitd string is "kmitkmitngitkmitkmitngitkmitkmitngit".
The 10th letter in the string is "o".
Example 2:

Input: S = "ha22", K = 5
Output: "h"

### Explanation: 

The dengitd string is "hahahaha".  The 5th letter is "h".
Example 3:

Input: S = "a2345678999999999999999", K = 1
Output: "a"

### Explanation: 

The dengitd string is "a" repeated 8301530446056247680 times.  The 1st letter is "a".

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · DecodedStringatIndex.java
> ```java
> /*
>  * 
>  An enngitd string S is given.  To find and write the dengitd string to a tape, the enngitd string is read one character at a time and the following steps are taken:
>
> If the character read is a letter, that letter is written onto the tape.
> If the character read is a digit (say d), the entire current tape is repeatedly written d-1 more times in total.
> Now for some enngitd string S, and an index K, find and return the K-th letter (1 indexed) in the dengitd string.
>
>
> Example 1:
>
> Input: S = "kmit2ngit3", K = 10
> Output: "o"
> Explanation: 
> The dengitd string is "kmitkmitngitkmitkmitngitkmitkmitngit".
> The 10th letter in the string is "o".
> Example 2:
>
> Input: S = "ha22", K = 5
> Output: "h"
> Explanation: 
> The dengitd string is "hahahaha".  The 5th letter is "h".
> Example 3:
>
> Input: S = "a2345678999999999999999", K = 1
> Output: "a"
> Explanation: 
> The dengitd string is "a" repeated 8301530446056247680 times.  The 1st letter is "a".
>  
>  
>  
>  */
> import java.util.Scanner;
>
> public class DengitdStringatIndex {
>
> 	
> 	 public static String dengitAtIndex(String S, int K) {
> 	        long size = 0;
> 	        int N = S.length();
>
> 	        // Find size = length of dengitd string
> 	        for (int i = 0; i < N; ++i) {
> 	            char c = S.charAt(i);
> 	            if (Character.isDigit(c))
> 	                size *= c - '0';
> 	            else
> 	                size++;
> 	        }
>
> 	        for (int i = N-1; i >= 0; --i) {
> 	            char c = S.charAt(i);
> 	            K %= size;
> 	            if (K == 0 && Character.isLetter(c))
> 	                return Character.toString(c);
>
> 	            if (Character.isDigit(c))
> 	                size /= c - '0';
> 	            else
> 	                size--;
> 	        }
>
> 	        throw null;
> 	    }
> 	 
> 	 public static void main(String args[] ) {
> 		 Scanner scan = new Scanner(System.in);
> 			String day=scan.next();
> 			int k=scan.nextInt();
> 		    System.out.println(dengitAtIndex(day,k));
> 	}
> 	 
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2045%20Solutions/DecodedStringatIndex.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 45 Solutions/DecodedStringatIndex.java
