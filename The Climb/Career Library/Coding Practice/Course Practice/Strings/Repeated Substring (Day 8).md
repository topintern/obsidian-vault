---
kind: "coding-problem"
title: "Repeated Substring (Day 8)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 8 Solutions/RepeatedSubstring.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Repeated Substring (Day 8)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a non-empty string, check if the given string can be constructed
by taking a substring of it and appending multiple copies of the substring together. 

You may assume the given string consists of lowercase English letters only and 
its length will not exceed 10000.

Example 1:
    Input=  abab
    Output= true
    Explanation: It's the substring "ab" twice.

Example 2:
    Input=  aba
    Output= false

Example 3:
    Input=  abcabcabcabc
    Output= true
    Explanation: It's the substring "abc" four times. (And the substring "abcabc" twice.)

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · RepeatedSubstring.java
> ```java
> /*
>  * 
> Given a non-empty string, check if the given string can be constructed
> by taking a substring of it and appending multiple copies of the substring together. 
>
> You may assume the given string consists of lowercase English letters only and 
> its length will not exceed 10000.
>
> Example 1:
>     Input=  abab
>     Output= true
>     Explanation: It's the substring "ab" twice.
>
> Example 2:
>     Input=  aba
>     Output= false
>
> Example 3:
>     Input=  abcabcabcabc
>     Output= true
>     Explanation: It's the substring "abc" four times. (And the substring "abcabc" twice.)
>  */
>
>
> import java.util.Scanner;
>
> public class RepeatedSubstring {
> 	
> 	public static boolean repeatedSubstringPattern(String str) {
> 		int l = str.length();
> 		for(int i=l/2;i>=1;i--) {
> 			if(l%i==0) {
> 				int m = l/i;
> 				String subS = str.substring(0,i);
> 				StringBuilder sb = new StringBuilder();
> 				for(int j=0;j<m;j++) {
> 					sb.append(subS);
> 				}
> 				if(sb.toString().equals(str)) return true;
> 			}
> 		}
> 		return false;
> 	}
> 	
> 	public static void main(String args[] ) {
> 			Scanner sc = new Scanner(System.in);
> 			String str=sc.next();
> 		    System.out.println(repeatedSubstringPattern(str));
> 	}
>
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%208%20Solutions/RepeatedSubstring.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 8 Solutions/RepeatedSubstring.java
