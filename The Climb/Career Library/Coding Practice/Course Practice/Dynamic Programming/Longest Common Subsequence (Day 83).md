---
kind: "coding-problem"
title: "Longest Common Subsequence (Day 83)"
collection: "Course Practice"
topic: "Dynamic Programming"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 83 Solutions/LongestCommonSubsequence.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Longest Common Subsequence (Day 83)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given two strings text1 and text2, return the length of their longest common subsequence.

A subsequence of a string is a new string generated from the original string with some 
characters(can be none) deleted without changing the relative order of the remaining characters.
(eg, "ace" is a subsequence of "abcde" while "aec" is not). A common subsequence of two strings
is a subsequence that is common to both strings.

If there is no common subsequence, return 0.

Example 1:
    
    Input: abcde ace 
    Output: 3  
    Explanation: The longest common subsequence is "ace" and its length is 3.

Example 2:

    Input: abc abc
    Output: 3
    Explanation: The longest common subsequence is "abc" and its length is 3.

Example 3:

    Input: abc def
    Output: 0
    Explanation: There is no such common subsequence, so the result is 0.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · LongestCommonSubsequence.java
> ```java
> /*
> Given two strings text1 and text2, return the length of their longest common subsequence.
>
> A subsequence of a string is a new string generated from the original string with some 
> characters(can be none) deleted without changing the relative order of the remaining characters.
> (eg, "ace" is a subsequence of "abcde" while "aec" is not). A common subsequence of two strings
> is a subsequence that is common to both strings.
>
> If there is no common subsequence, return 0.
>
> Example 1:
>     
>     Input: abcde ace 
>     Output: 3  
>     Explanation: The longest common subsequence is "ace" and its length is 3.
>
> Example 2:
>
>     Input: abc abc
>     Output: 3
>     Explanation: The longest common subsequence is "abc" and its length is 3.
>
> Example 3:
>
>     Input: abc def
>     Output: 0
>     Explanation: There is no such common subsequence, so the result is 0.
>
> */
>
> import java.util.*;
>
> class LongestCommonSubsequence
> {
>     public static int longestCommonSubsequence(String text1, String text2) {
>         if(text1.length() == 0 || text2.length() == 0) return 0;
>         int m = text1.length();
>         int n = text2.length();
>         int[][] dp = new int[m + 1][n + 1];
>         for(int i = 1; i <= m; i++){
>             for(int j = 1; j <= n; j++){
>                 if(text1.charAt(i - 1) == text2.charAt(j - 1)){
>                     dp[i][j] = 1 + dp[i - 1][j - 1];
>                 }else{
>                     dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
>                 }
>             }
>         }
>         return dp[m][n];
>     }
>     public static void main(String args[])
>     {
>         Scanner sc=new Scanner(System.in);
>         String s1=sc.next();
>         String s2=sc.next();
>         System.out.println(longestCommonSubsequence(s1,s2));
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2083%20Solutions/LongestCommonSubsequence.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 83 Solutions/LongestCommonSubsequence.java
