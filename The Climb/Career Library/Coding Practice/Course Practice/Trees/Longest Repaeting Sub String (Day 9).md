---
kind: "coding-problem"
title: "Longest Repaeting Sub String (Day 9)"
collection: "Course Practice"
topic: "Trees"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 9 Solutions/LongestRepaetingSubString.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Longest Repaeting Sub String (Day 9)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a string S, find out the length of the longest repeating substring(s). Return 0 if no repeating substring exists.

 

Example 1:

Input: abcd
Output: 0
Explanation: There is no repeating substring.
Example 2:

Input: abbaba
Output: 2
Explanation: The longest repeating substrings are "ab" and "ba", each of which occurs twice.
Example 3:

Input: aabcaabdaab
Output: 3
Explanation: The longest repeating substring is "aab", which occurs 3 times.
Example 4:

Input: aaaaa
Output: 4
Explanation: The longest repeating substring is "aaaa", which occurs twice.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · LongestRepaetingSubString.java
> ```java
> /*
>  * 
>  * 
> Given a string S, find out the length of the longest repeating substring(s). Return 0 if no repeating substring exists.
>
>  
>
> Example 1:
>
> Input: abcd
> Output: 0
> Explanation: There is no repeating substring.
> Example 2:
>
> Input: abbaba
> Output: 2
> Explanation: The longest repeating substrings are "ab" and "ba", each of which occurs twice.
> Example 3:
>
> Input: aabcaabdaab
> Output: 3
> Explanation: The longest repeating substring is "aab", which occurs 3 times.
> Example 4:
>
> Input: aaaaa
> Output: 4
> Explanation: The longest repeating substring is "aaaa", which occurs twice.
>  
>  */
>
> package Leetcode;
>
> import java.util.Scanner;
>
> public class LongestRepaetingSubString {
> 	
> 	    class TrieNode{
> 	        TrieNode[] next;
> 	        public TrieNode(){
> 	            next = new TrieNode[26];
> 	        }
> 	    }
> 	    
> 	    public int longestRepeatingSubstring(String S) {
> 	        char[] A = S.toCharArray();
> 	        int res = 0;
> 	        TrieNode root = new TrieNode();
> 	        for(int i=0; i<S.length(); i++){
> 	            TrieNode cur = root;
> 	            for(int j=i; j<S.length(); j++){
> 	                if(cur.next[A[j]-'a']==null){
> 	                    TrieNode newNode = new TrieNode();
> 	                    cur.next[A[j]-'a'] = newNode;
> 	                    cur = newNode;
> 	                }
> 	                else{
> 	                    res = Math.max(res,j-i+1);
> 	                    cur = cur.next[A[j]-'a'];
> 	                }
> 	            }
> 	        }
> 	        return res;
> 	    }
> 	    
> 	    public static void main(String args[] ) {
> 			 Scanner sc = new Scanner(System.in);
> 				String word=sc.next();
> 				LongestRepaetingSubString lr=new LongestRepaetingSubString();
> 			    System.out.println(lr.longestRepeatingSubstring(word));
> 		}
> 	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%209%20Solutions/LongestRepaetingSubString.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 9 Solutions/LongestRepaetingSubString.java
