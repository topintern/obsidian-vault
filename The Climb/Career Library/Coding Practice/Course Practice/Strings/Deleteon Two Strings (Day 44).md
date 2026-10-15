---
kind: "coding-problem"
title: "Deleteon Two Strings (Day 44)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 44 Solutions/DeleteonTwoStrings.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Deleteon Two Strings (Day 44)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given two words word1 and word2, find the minimum number of steps required to make word1 and word2 the same, 
 where in each step you can delete one character in either string.

Example 1:
Input:sea
eat
Output: 2
Explanation: You need one step to make "sea" to "ea" and another step to make "eat" to "ea".


=======================================================================

To make them identical, just find the longest common subsequence. 
The rest of the characters have to be deleted from the both the strings, which does not belong to longest common subsequence.

 
 ==========TestCases=============
case =1
input =attitude
tubelight
output =11

case =2
input =abc def
abc def
output =0

case =3
input =abcdefghijk
lmnopqrstuv
output =22

case =4
input =ram mohan is back
mask
output =13

case =5
input =rrrrrrtttttttt uuuuuuuuuvvvvvvv hhhhhhhhhhiii
rruuuttvvvvtttt
output =42

case =6
input =abcdefghijklmnopqrstuvwxyz
keshav memorial institute of technology
output =47

case =7
input =the big brwon fox jumps over a lazy little dog
won over the dog
output =32

case =8
input =Given two words word1 and word2, find the minimum number of steps required to make word1 and word2 the same
Explanation: You need one step to make "sea" to "ea" and another step to make "eat" to "ea".
output =117

case =9
input =qwepasdfghjklzxcvbnm1234567890-!@#%^&()
@#%^&()RTYUIOPERTYUIVBNMHJK
output =52

case =10
input =@#$%^&*()_
_)(*&^%$#@!
output =19

case =11
input =AbC dEfGh IjKlMn OpQr   StUvWxYz
qwe rty uio pas df ghj klzx cvbnm
output =49

case =12
input =testcases for this program are given by
nagireddy and ram mohan
output =42

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · DeleteonTwoStrings.java
> ```java
> /*
>  * 
>  Given two words word1 and word2, find the minimum number of steps required to make word1 and word2 the same, 
>  where in each step you can delete one character in either string.
>
> Example 1:
> Input:sea
> eat
> Output: 2
> Explanation: You need one step to make "sea" to "ea" and another step to make "eat" to "ea".
>
>
> =======================================================================
>
> To make them identical, just find the longest common subsequence. 
> The rest of the characters have to be deleted from the both the strings, which does not belong to longest common subsequence.
>
>  
>  ==========TestCases=============
> case =1
> input =attitude
> tubelight
> output =11
>
> case =2
> input =abc def
> abc def
> output =0
>
> case =3
> input =abcdefghijk
> lmnopqrstuv
> output =22
>
> case =4
> input =ram mohan is back
> mask
> output =13
>
> case =5
> input =rrrrrrtttttttt uuuuuuuuuvvvvvvv hhhhhhhhhhiii
> rruuuttvvvvtttt
> output =42
>
> case =6
> input =abcdefghijklmnopqrstuvwxyz
> keshav memorial institute of technology
> output =47
>
> case =7
> input =the big brwon fox jumps over a lazy little dog
> won over the dog
> output =32
>
> case =8
> input =Given two words word1 and word2, find the minimum number of steps required to make word1 and word2 the same
> Explanation: You need one step to make "sea" to "ea" and another step to make "eat" to "ea".
> output =117
>
> case =9
> input =qwepasdfghjklzxcvbnm1234567890-!@#%^&()
> @#%^&()RTYUIOPERTYUIVBNMHJK
> output =52
>
> case =10
> input =@#$%^&*()_
> _)(*&^%$#@!
> output =19
>
> case =11
> input =AbC dEfGh IjKlMn OpQr   StUvWxYz
> qwe rty uio pas df ghj klzx cvbnm
> output =49
>
> case =12
> input =testcases for this program are given by
> nagireddy and ram mohan
> output =42
>  
>
>  */
>
>
> import java.util.Scanner;
>
> public class DeleteonTwoStrings {
>
> 	public static int minDistance(String word1, String word2) {
> 	    int dp[][] = new int[word1.length()+1][word2.length()+1];
> 	    for(int i = 0; i <= word1.length(); i++) {
> 	        for(int j = 0; j <= word2.length(); j++) {
> 	            if(i == 0 || j == 0) dp[i][j] = 0;
> 	            else dp[i][j] = (word1.charAt(i-1) == word2.charAt(j-1)) ? dp[i-1][j-1] + 1
> 	                    : Math.max(dp[i-1][j], dp[i][j-1]);
> 	        }
> 	    }
> 	    int val =  dp[word1.length()][word2.length()];
> 	    return word1.length() - val + word2.length() - val;
> 	}
>
> 	
> 	 public static void main(String args[] ) {
> 		 Scanner scan = new Scanner(System.in);
> 			String word1=scan.nextLine();
> 			String word2=scan.nextLine();
> 			System.out.println(minDistance(word1,word2));
> 	}
> 	 
> 	 
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2044%20Solutions/DeleteonTwoStrings.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 44 Solutions/DeleteonTwoStrings.java
