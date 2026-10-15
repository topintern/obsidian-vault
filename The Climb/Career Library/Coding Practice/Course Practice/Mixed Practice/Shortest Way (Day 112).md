---
kind: "coding-problem"
title: "Shortest Way (Day 112)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 112 Solutions/ShortestWay.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Shortest Way (Day 112)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Kiran is playing with strings and its subsequences.
A subsequence can be formed from a string by deleting some characters(may be string itself)

Kiran has given two strings S and T, your task to form T by concatenating the subsequences of S  

Return the minimum number of subsequences required to form T.
If the task is impossible, return -1 .

Input Format:
-------------
Line-1 -> Two strings S and T

Output Format:
--------------
Print an integer as result.


Sample Input-1:
---------------
abc abcbc

Sample Output-1:
----------------
2


### Explanation: 

------------
T = "abcbc" can be formed by "abc" and "bc",
which are subsequences of S = "abc".


Sample Input-2:
---------------
abc acdbc

Sample Output-2:
----------------
-1


### Explanation: 

------------
string T cannot be constructed from the
subsequences of string S due to the character "d" in string T.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ShortestWay.java
> ```java
> /*
> Kiran is playing with strings and its subsequences.
> A subsequence can be formed from a string by deleting some characters(may be string itself)
>
> Kiran has given two strings S and T, your task to form T by concatenating the subsequences of S  
>
> Return the minimum number of subsequences required to form T.
> If the task is impossible, return -1 .
>
> Input Format:
> -------------
> Line-1 -> Two strings S and T
>
> Output Format:
> --------------
> Print an integer as result.
>
>
> Sample Input-1:
> ---------------
> abc abcbc
>
> Sample Output-1:
> ----------------
> 2
>
> Explanation: 
> ------------
> T = "abcbc" can be formed by "abc" and "bc",
> which are subsequences of S = "abc".
>
>
> Sample Input-2:
> ---------------
> abc acdbc
>
> Sample Output-2:
> ----------------
> -1
>
> Explanation: 
> ------------
> string T cannot be constructed from the
> subsequences of string S due to the character "d" in string T.
>
> */
>
> import java.util.*;
>
> class ShortestWay{
> 	public int shortestWay(String source, String target) {
> 		char[] cs = source.toCharArray(), ts = target.toCharArray();
> 		int[][] idx = new int[cs.length][26];
> 		idx[cs.length - 1][cs[cs.length - 1] - 'a'] = cs.length; 
> 		for (int i = cs.length - 2; i >= 0; i--) {
> 			idx[i] = Arrays.copyOf(idx[i + 1],26);
> 			idx[i][cs[i] - 'a'] = i + 1; 
> 		}
> 		int j = 0, res = 1;
> 		for (int i = 0; i < ts.length; i++) {
> 			if (j == cs.length) {
> 				j = 0;
> 				res++;
> 			}
> 			j = idx[j][ts[i] - 'a'];
> 			if (idx[0][ts[i] - 'a'] == 0) return -1;
> 			if (j == 0) {
> 				res++;
> 				i--;
> 			}
> 		}
> 		return res;
> 	}
> 	
> 	 public static void main(String args[] ) {
>
> 		    Scanner sc = new Scanner(System.in);
> 			String word1=sc.next();
> 			String word2=sc.next();
> 			System.out.println(new ShortestWay().shortestWay(word1,word2));
> 	 } 	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20112%20Solutions/ShortestWay.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 112 Solutions/ShortestWay.java
