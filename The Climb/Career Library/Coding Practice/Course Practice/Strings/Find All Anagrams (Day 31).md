---
kind: "coding-problem"
title: "Find All Anagrams (Day 31)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 31 Solutions/FindAllAnagrams.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Find All Anagrams (Day 31)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a string s and a non-empty string p, find all the start indices of p's anagrams in s.

Strings consists of lowercase English letters only and the length of both strings s and p will not be larger than 20,100.

The order of output does not matter.

Example 1:

Input:cbaebabacd
abc

Output:
[0, 6]


### Explanation

The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
Example 2:

Input:abab
ab

Output:
[0, 1, 2]


### Explanation

The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".

-------------------------------------------------------------

case =1
input =abababbbababbabababba
ab
output =[0, 1, 2, 3, 4, 7, 8, 9, 10, 12, 13, 14, 15, 16, 17, 19]

case =2
input =kmitmkittttkimmkitmkit
kmit
output =[0, 2, 3, 4, 10, 14, 15, 16, 17, 18]

case =3
input =ljhdsihirnbkjnvljdsvijndfk
hij
output =[]

case =4
input =xyzxyzyxyzyxyxyzyxyxyzyxxyxyzxy
xyz
output =[0, 1, 2, 3, 5, 7, 9, 13, 15, 19, 21, 26, 27, 28]

case =5
input =qwewertqwerqwertewqwerer
qwe
output =[0, 7, 11, 16, 18]

case =6
input =hnthnthhthtyhnthnthnth
hnt
output =[0, 1, 2, 3, 4, 12, 13, 14, 15, 16, 17, 18, 19]

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · FindAllAnagrams.java
> ```java
> /*
>  * 
>  Given a string s and a non-empty string p, find all the start indices of p's anagrams in s.
>
> Strings consists of lowercase English letters only and the length of both strings s and p will not be larger than 20,100.
>
> The order of output does not matter.
>
> Example 1:
>
> Input:cbaebabacd
> abc
>
> Output:
> [0, 6]
>
> Explanation:
> The substring with start index = 0 is "cba", which is an anagram of "abc".
> The substring with start index = 6 is "bac", which is an anagram of "abc".
> Example 2:
>
> Input:abab
> ab
>
> Output:
> [0, 1, 2]
>
> Explanation:
> The substring with start index = 0 is "ab", which is an anagram of "ab".
> The substring with start index = 1 is "ba", which is an anagram of "ab".
> The substring with start index = 2 is "ab", which is an anagram of "ab".
>
> -------------------------------------------------------------
>
> case =1
> input =abababbbababbabababba
> ab
> output =[0, 1, 2, 3, 4, 7, 8, 9, 10, 12, 13, 14, 15, 16, 17, 19]
>
> case =2
> input =kmitmkittttkimmkitmkit
> kmit
> output =[0, 2, 3, 4, 10, 14, 15, 16, 17, 18]
>
> case =3
> input =ljhdsihirnbkjnvljdsvijndfk
> hij
> output =[]
>
> case =4
> input =xyzxyzyxyzyxyxyzyxyxyzyxxyxyzxy
> xyz
> output =[0, 1, 2, 3, 5, 7, 9, 13, 15, 19, 21, 26, 27, 28]
>
> case =5
> input =qwewertqwerqwertewqwerer
> qwe
> output =[0, 7, 11, 16, 18]
>
> case =6
> input =hnthnthhthtyhnthnthnth
> hnt
> output =[0, 1, 2, 3, 4, 12, 13, 14, 15, 16, 17, 18, 19]
>
>
>
>
>  */
> package Elite2020;
>
> import java.util.*;
>
> public class FindAllAnagrams {
>
> 	 public static List<Integer> findAnagrams(String s, String p) {
> 		    int ns = s.length(), np = p.length();
> 		    if (ns < np) return new ArrayList();
>
> 		    int [] pCount = new int[26];
> 		    int [] sCount = new int[26];
> 		    // build reference array using string p
> 		    for (char ch : p.toCharArray()) {
> 		      pCount[(int)(ch - 'a')]++;
> 		    }
>
> 		    List<Integer> output = new ArrayList();
> 		    // sliding window on the string s
> 		    for (int i = 0; i < ns; ++i) {
> 		      // add one more letter 
> 		      // on the right side of the window
> 		      sCount[(int)(s.charAt(i) - 'a')]++;
> 		      // remove one letter 
> 		      // from the left side of the window
> 		      if (i >= np) {
> 		        sCount[(int)(s.charAt(i - np) - 'a')]--;
> 		      }
> 		      // compare array in the sliding window
> 		      // with the reference array
> 		      if (Arrays.equals(pCount, sCount)) {
> 		        output.add(i - np + 1);
> 		      }
> 		    }
> 		    return output;
> 		  }
> 	 
> 	 public static void main(String args[] ) {
> 		 Scanner sc = new Scanner(System.in);
> 			String s=sc.next();
> 			String p=sc.next();
> 		    System.out.println(findAnagrams(s,p));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2031%20Solutions/FindAllAnagrams.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 31 Solutions/FindAllAnagrams.java
