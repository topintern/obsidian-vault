---
kind: "coding-problem"
title: "Concatenated Words (Day 27)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 27 Solutions/ConcatenatedWords.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Concatenated Words (Day 27)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a list of words (without duplicates), please write a program that returns all concatenated words in the given list of words.
A concatenated word is defined as a string that is comprised entirely of at least two shorter words in the given array.

Example:
Input: ["cat","cats","catsdogcats","dog","dogcatsdog","hippopotamuses","rat","ratcatdogcat"]

Output: ["catsdogcats","dogcatsdog","ratcatdogcat"]

Explanation: "catsdogcats" can be concatenated by "cats", "dog" and "cats"; 
 "dogcatsdog" can be concatenated by "dog", "cats" and "dog"; 
"ratcatdogcat" can be concatenated by "rat", "cat", "dog" and "cat".


=========================================

If you do know one optimized solution for above question is using DP, this problem is just one more step further. We iterate through each word and see if it can be formed by using other words.

Of course it is also obvious that a word can only be formed by words shorter than it. So we can first sort the input by length of each word, and only try to form one word by using words in front of it.

=======TestCases============
case =1
input =a b abc ab d abcd aef g h gcd
output =[ab, abcd] 

case =2
input =hi how hihowareyou are you hellohow youare hell
output =[hihowareyou, youare]

case =3
input =can you dare canyoudare for foryou dareyou
output =[canyoudare, dareyou, foryou]

case =4
input =ram mohan rammohan nagireddy nagi reddy ramireddy
output =[nagireddy, rammohan]

case =5
input =keshav memorial institute of technology
output =[]

case =6
input =a b c d e f g h i j k l m n o p q r s t u v w x y z abcd howare you kishore keshav kmit
output =[abcd, howare, keshav, kishore, kmit, you]

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ConcatenatedWords.java
> ```java
> /*
>  * 
>  Given a list of words (without duplicates), please write a program that returns all concatenated words in the given list of words.
> A concatenated word is defined as a string that is comprised entirely of at least two shorter words in the given array.
>
> Example:
> Input: ["cat","cats","catsdogcats","dog","dogcatsdog","hippopotamuses","rat","ratcatdogcat"]
>
> Output: ["catsdogcats","dogcatsdog","ratcatdogcat"]
>
> Explanation: "catsdogcats" can be concatenated by "cats", "dog" and "cats"; 
>  "dogcatsdog" can be concatenated by "dog", "cats" and "dog"; 
> "ratcatdogcat" can be concatenated by "rat", "cat", "dog" and "cat".
>
>
> =========================================
>
> If you do know one optimized solution for above question is using DP, this problem is just one more step further. We iterate through each word and see if it can be formed by using other words.
>
> Of course it is also obvious that a word can only be formed by words shorter than it. So we can first sort the input by length of each word, and only try to form one word by using words in front of it.
>
> =======TestCases============
> case =1
> input =a b abc ab d abcd aef g h gcd
> output =[ab, abcd] 
>
> case =2
> input =hi how hihowareyou are you hellohow youare hell
> output =[hihowareyou, youare]
>
> case =3
> input =can you dare canyoudare for foryou dareyou
> output =[canyoudare, dareyou, foryou]
>
> case =4
> input =ram mohan rammohan nagireddy nagi reddy ramireddy
> output =[nagireddy, rammohan]
>
> case =5
> input =keshav memorial institute of technology
> output =[]
>
> case =6
> input =a b c d e f g h i j k l m n o p q r s t u v w x y z abcd howare you kishore keshav kmit
> output =[abcd, howare, keshav, kishore, kmit, you]
>
>
>  */
>
>
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.*;
>
> public class ConcatenatedWords {
>
> 	public static List<String> findAllConcatenatedWordsInADict(String[] words) {
>         List<String> result = new ArrayList<>();
>         Set<String> preWords = new HashSet<>();
>         Arrays.sort(words, new Comparator<String>() {
>             public int compare (String s1, String s2) {
>                 return s1.length() - s2.length();
>             }
>         });
>         
>         for (int i = 0; i < words.length; i++) {
>             if (canForm(words[i], preWords)) {
>                 result.add(words[i]);
>             }
>             preWords.add(words[i]);
>         }
>         
>         return result;
>     }
> 	
>     private static boolean canForm(String word, Set<String> dict) {
>         if (dict.isEmpty()) return false;
> 	boolean[] dp = new boolean[word.length() + 1];
> 	dp[0] = true;
> 	for (int i = 1; i <= word.length(); i++) {
> 	    for (int j = 0; j < i; j++) {
> 		if (!dp[j]) continue;
> 		if (dict.contains(word.substring(j, i))) {
> 		    dp[i] = true;
> 		    break;
> 		}
> 	    }
> 	}
> 	return dp[word.length()];
>     }
>     
>     public static void main(String args[] ) throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		String[] words = str.split(" ");
>
> 		System.out.println(findAllConcatenatedWordsInADict(words));   
> 		
> 		}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2027%20Solutions/ConcatenatedWords.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 27 Solutions/ConcatenatedWords.java
