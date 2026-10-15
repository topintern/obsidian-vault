---
kind: "coding-problem"
title: "Longest String Chain (Day 39)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 39 Solutions/LongestStringChain.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Longest String Chain (Day 39)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a list of words, each word consists of English lowercase letters.

Let's say word1 is a predecessor of word2 if and only if we can add exactly one letter anywhere in word1 to make it equal to word2.  For example, "abc" is a predecessor of "abac".

A word chain is a sequence of words [word_1, word_2, ..., word_k] with k >= 1, where word_1 is a predecessor of word_2, word_2 is a predecessor of word_3, and so on.

Return the longest possible length of a word chain with words chosen from the given list of words.

 

Example 1:

Input: a b ba bca bda bdca
Output: 4
Explanation: one of the longest word chain is "a","ba","bda","bdca".
 
 
 
 ==============================
 
 Explanation
Sort the words by word's length. (also can apply bucket sort)
For each word, loop on all possible previous word with 1 letter missing.
If we have seen this previous word, update the longest chain for the current word.
Finally return the longest word chain.


Complexity
Time O(NlogN) for sorting,
Time O(NSS) for the for loop, where the second S refers to the string generation and S <= 16.
Space O(NS)


===========TestCases=======
case =1
input =a ab abc abcd abcde abcdef abcdeg
output =6

case =2
input =a b c d e f ab ac ad ae af abc ade afg adbc adec afgh abcde 
output =4

case =3
input =a b c d e f g h i
output =1

case =4
input =k n ng kmi kmit i it git
output =3

case =5
input =a b c d ab ac ad dae cae bae
output =2

case =6
input =abc abcd abcde abd abde abdef a ab
output =5

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · LongestStringChain.txt
> ```java
> /*
>  * 
>  
>  Given a list of words, each word consists of English lowercase letters.
>
> Let's say word1 is a predecessor of word2 if and only if we can add exactly one letter anywhere in word1 to make it equal to word2.  For example, "abc" is a predecessor of "abac".
>
> A word chain is a sequence of words [word_1, word_2, ..., word_k] with k >= 1, where word_1 is a predecessor of word_2, word_2 is a predecessor of word_3, and so on.
>
> Return the longest possible length of a word chain with words chosen from the given list of words.
>
>  
>
> Example 1:
>
> Input: a b ba bca bda bdca
> Output: 4
> Explanation: one of the longest word chain is "a","ba","bda","bdca".
>  
>  
>  
>  ==============================
>  
>  Explanation
> Sort the words by word's length. (also can apply bucket sort)
> For each word, loop on all possible previous word with 1 letter missing.
> If we have seen this previous word, update the longest chain for the current word.
> Finally return the longest word chain.
>
>
> Complexity
> Time O(NlogN) for sorting,
> Time O(NSS) for the for loop, where the second S refers to the string generation and S <= 16.
> Space O(NS)
>
>
> ===========TestCases=======
> case =1
> input =a ab abc abcd abcde abcdef abcdeg
> output =6
>
> case =2
> input =a b c d e f ab ac ad ae af abc ade afg adbc adec afgh abcde 
> output =4
>
> case =3
> input =a b c d e f g h i
> output =1
>
> case =4
> input =k n ng kmi kmit i it git
> output =3
>
> case =5
> input =a b c d ab ac ad dae cae bae
> output =2
>
> case =6
> input =abc abcd abcde abd abde abdef a ab
> output =5
>
>  */
>
> package Elite2020;
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.*;
>
> public class LongestStringChain {
> 	public static int longestStrChain(String[] words) {
>         Map<String, Integer> dp = new HashMap<>();
>         Arrays.sort(words, (a, b)->a.length() - b.length());
>         int res = 0;
>         for (String word : words) {
>             int best = 0;
>             for (int i = 0; i < word.length(); ++i) {
>                 String prev = word.substring(0, i) + word.substring(i + 1);
>                 best = Math.max(best, dp.getOrDefault(prev, 0) + 1);
>             }
>             dp.put(word, best);
>             res = Math.max(res, best);
>         }
>         return res;
>     }
> 	
> 	public static void main(String args[] ) throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		String[] words = str.split(" ");
>
> 		System.out.println(longestStrChain(words));   
> 		
> 		}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2039%20Solutions/LongestStringChain.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 39 Solutions/LongestStringChain.txt
