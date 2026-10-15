---
kind: "coding-problem"
title: "Short Pallindrome (Day 68)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 68 Solutions/ShortPallindrome.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Short Pallindrome (Day 68)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Consider a string, S, of n lowercase English letters where each character, 
Si denotes the letter at index i in S. 
We define an (a,b,c,d) palindromic tuple of S to be a sequence of indices
in S satisfying the following criteria:
	-Sa=Sd, meaning the characters located at indices a and d are the same.
	-Sb=Sc, meaning the characters located at indices b and c are the same.
	-a, b, c, and d are ascending in value and are valid indices within string .
Given S, find and print the number of (a,b,c,d) tuples satisfying the above conditions. 

Input Format:
	-A single string denoting S.
NOTE: It is guaranteed that  only contains lowercase English letters.

Output Format:
	-Print the the number of (a,b,c,d) tuples satisfying the given conditions. 
	As this value can be quite large, print it modulo 1000000007.

Sample Input1:
kkkkkkz
Sample Output1:
15
Explanation1:
The letter z will not be part of a valid tuple because you need
at least two of the same character to satisfy the conditions defined above. 
Because all tuples consisting of four k's are valid, 
we just need to find the number of ways that we can choose four of the six k's. 
This means our answer is 6P4 mod 1000000007=15.

Sample Input2:
ghhggh
Sample Output2:
4
Explanation2:
The valid tuples are: (0,1,2,3), (0,1,2,4), (1,3,4,5), (2,3,4,5)
Thus, our answer is 4.

Sample Input3:
akakak
Sample Output3:
2
Explanation3:
Tuples possible are (1,2,4,5) and (0,1,3,4) 


========= Testcases Program-3 =========
case =1
input =akakak
output =2

case =2
input =ghhggh
output =4

case =3
input =kkkkkkz
output =15

case =4
input =abbabababba
output =72

case =5
input =nnnnkkkknnnnnkkkkkk
output =696

case =6
input =redivider
output =6

case =7
input =transmission
output =5

case =8
input =qwertywertyertyrty
output =42

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ShortPallindrome.java
> ```java
> /*
>
> Consider a string, S, of n lowercase English letters where each character, 
> Si denotes the letter at index i in S. 
> We define an (a,b,c,d) palindromic tuple of S to be a sequence of indices
> in S satisfying the following criteria:
> 	-Sa=Sd, meaning the characters located at indices a and d are the same.
> 	-Sb=Sc, meaning the characters located at indices b and c are the same.
> 	-a, b, c, and d are ascending in value and are valid indices within string .
> Given S, find and print the number of (a,b,c,d) tuples satisfying the above conditions. 
>
> Input Format:
> 	-A single string denoting S.
> NOTE: It is guaranteed that  only contains lowercase English letters.
>
> Output Format:
> 	-Print the the number of (a,b,c,d) tuples satisfying the given conditions. 
> 	As this value can be quite large, print it modulo 1000000007.
>
> Sample Input1:
> kkkkkkz
> Sample Output1:
> 15
> Explanation1:
> The letter z will not be part of a valid tuple because you need
> at least two of the same character to satisfy the conditions defined above. 
> Because all tuples consisting of four k's are valid, 
> we just need to find the number of ways that we can choose four of the six k's. 
> This means our answer is 6P4 mod 1000000007=15.
>
> Sample Input2:
> ghhggh
> Sample Output2:
> 4
> Explanation2:
> The valid tuples are: (0,1,2,3), (0,1,2,4), (1,3,4,5), (2,3,4,5)
> Thus, our answer is 4.
>
> Sample Input3:
> akakak
> Sample Output3:
> 2
> Explanation3:
> Tuples possible are (1,2,4,5) and (0,1,3,4) 
>
>
> ========= Testcases Program-3 =========
> case =1
> input =akakak
> output =2
>
> case =2
> input =ghhggh
> output =4
>
> case =3
> input =kkkkkkz
> output =15
>
> case =4
> input =abbabababba
> output =72
>
> case =5
> input =nnnnkkkknnnnnkkkkkk
> output =696
>
> case =6
> input =redivider
> output =6
>
> case =7
> input =transmission
> output =5
>
> case =8
> input =qwertywertyertyrty
> output =42
>
> */
>
> import java.io.*;
> import java.util.*;
>
> public class ShortPallindrome {
> 	private static final long MOD = 1000000007L;
>
> 	public static void main(String[] args) throws Exception {
> 		BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
>
> 		String s = bf.readLine();
> 		int n = s.length();
>
> 		int[][] countR = new int[n][26];
> 		countR[n - 1][s.charAt(n - 1) - 'a']++;
> 		for (int i = n - 2; i >= 0; i--) {
> 			System.arraycopy(countR[i + 1], 0, countR[i], 0, 26);
> 			countR[i][s.charAt(i) - 'a']++;
> 		}
>
> 		int[] countL = new int[26];
> 		int[] countL2 = new int[676];
>
> 		long res = 0;
> 		countL[s.charAt(0) - 'a']++;
> 		for (int i = 1; i < n - 1; i++) {
> 			int index = s.charAt(i) - 'a';
> 			for (int j = 0; j < 26; j++) {
> 				long t = countL2[index * 26 + j];
> 				t *= (long) countR[i + 1][j];
> 				t %= MOD;
> 				res += t;
> 				res %= MOD;
> 			}
>
> 			for (int j = 0; j < 26; j++) {
> 				countL2[index * 26 + j] += countL[j];
> 				countL2[index * 26 + j] %= MOD;
> 			}
> 			countL[index]++;
> 		}
> 		System.out.println(res);
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2068%20Solutions/ShortPallindrome.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 68 Solutions/ShortPallindrome.java
