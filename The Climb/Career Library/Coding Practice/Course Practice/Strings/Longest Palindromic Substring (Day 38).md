---
kind: "coding-problem"
title: "Longest Palindromic Substring (Day 38)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 38 Solutions/LongestPalindromicSubstring.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Longest Palindromic Substring (Day 38)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a string s, find the longest palindromic substring in s. 
 You may assume that the maximum length of s is 1000.

Example 1:

Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.


Example 2:

Input: "cbbd"
Output: "bb"

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · LongestPalindromicSubstring.txt
> ```java
> /*
>  * 
>  Given a string s, find the longest palindromic substring in s. 
>  You may assume that the maximum length of s is 1000.
>
> Example 1:
>
> Input: "babad"
> Output: "bab"
> Note: "aba" is also a valid answer.
>
>
> Example 2:
>
> Input: "cbbd"
> Output: "bb"
>
>
>
>  */
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
>
> public class LongestPalindromicSubstring {
>
> 	private static int lo;
> 	private static int maxLen;
>
> 	public static String longestPalindrome(String s) {
> 		int len = s.length();
> 		if (len < 2)
> 			return s;
> 		
> 	    for (int i = 0; i < len-1; i++) {
> 	     	extendPalindrome(s, i, i);  //assume odd length, try to extend Palindrome as possible
> 	     	extendPalindrome(s, i, i+1); //assume even length.
> 	    }
> 	    return s.substring(lo, lo + maxLen);
> 	}
>
> 	private static void extendPalindrome(String s, int j, int k) {
> 		while (j >= 0 && k < s.length() && s.charAt(j) == s.charAt(k)) {
> 			j--;
> 			k++;
> 		}
> 		if (maxLen < k - j - 1) {
> 			lo = j + 1;
> 			maxLen = k - j - 1;
> 		}
> 	}
> 	
> 	 public static void main(String args[] ) throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 			String str = br.readLine();
> 			
> 			System.out.println(longestPalindrome(str));   
> 			
> 			}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2038%20Solutions/LongestPalindromicSubstring.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 38 Solutions/LongestPalindromicSubstring.txt
