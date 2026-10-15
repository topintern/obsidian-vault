---
kind: "coding-problem"
title: "Min Add Parentheses (Day 38)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 38 Solutions/minAddParentheses.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Min Add Parentheses (Day 38)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a string S of '(' and ')' parentheses, we add the minimum number of parentheses ( '(' or ')', and in any positions ) 
so that the resulting parentheses string is valid.

Formally, a parentheses string is valid if and only if:

It is the empty string, or
It can be written as AB (A concatenated with B), where A and B are valid strings, or
It can be written as (A), where A is a valid string.
Given a parentheses string, return the minimum number of parentheses we must add to make the resulting string valid.

 
 
 Example 1:

Input: ())
Output: 1
Example 2:

Input: (((
Output: 3
Example 3:

Input: ()
Output: 0
Example 4:

Input: ()))((
Output: 4
 

Note:

S.length <= 1000
S only consists of '(' and ')' characters.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · minAddParentheses.txt
> ```java
> /*
> Given a string S of '(' and ')' parentheses, we add the minimum number of parentheses ( '(' or ')', and in any positions ) 
> so that the resulting parentheses string is valid.
>
> Formally, a parentheses string is valid if and only if:
>
> It is the empty string, or
> It can be written as AB (A concatenated with B), where A and B are valid strings, or
> It can be written as (A), where A is a valid string.
> Given a parentheses string, return the minimum number of parentheses we must add to make the resulting string valid.
>
>  
>  
>  Example 1:
>
> Input: ())
> Output: 1
> Example 2:
>
> Input: (((
> Output: 3
> Example 3:
>
> Input: ()
> Output: 0
> Example 4:
>
> Input: ()))((
> Output: 4
>  
>
> Note:
>
> S.length <= 1000
> S only consists of '(' and ')' characters.
>
>
>  
>  */
>
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
>
> public class minAddParentheses {
> 	public static int minAddToMakeValid(String S) {
>         int left = 0, right = 0;
>         for (int i = 0; i < S.length(); ++i) {
>             if (S.charAt(i) == '(') {
>                 right++;
>             } else if (right > 0) {
>                 right--;
>             } else {
>                 left++;
>             }
>         }
>         return left + right;
>     }
> 	
> 	  public static void main(String args[])  throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 			String S = br.readLine();
>
> 			System.out.println(minAddToMakeValid(S));
> 	  
> 	    } 
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2038%20Solutions/minAddParentheses.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 38 Solutions/minAddParentheses.txt
