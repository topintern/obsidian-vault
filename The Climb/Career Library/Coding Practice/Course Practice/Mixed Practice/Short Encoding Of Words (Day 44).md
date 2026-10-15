---
kind: "coding-problem"
title: "Short Encoding Of Words (Day 44)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 44 Solutions/ShortEncodingOfWords.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Short Encoding Of Words (Day 44)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a list of words, we may encode it by writing a reference string S and a list of indexes A.

For example, if the list of words is ["time", "me", "bell"], we can write it as S = "time#bell#" and indexes = [0, 2, 5].

Then for each index, we will recover the word by reading from the reference string from that index until we reach a "#" character.

What is the length of the shortest reference string S possible that encodes the given words?

Example:

Input:time me bell
Output: 10
Explanation: S = "time#bell#" and indexes = [0, 2, 5].
 

Note:

1 <= words.length <= 20, if violated print -1
1 <= words[i].length <= 7, if violated print -2
Each word has only lowercase letters.

=======TestCases======
case =1
input =abc cde efg fgh ghi hjkl klmno lmnop opqrstuv tuvx uvwxy wxyz amith kishore neil ram mohan nagi reddy kmit ngit
output =-1

case =2
input =amith kishore neil ram mohan nagireddy kmit ngit
output =-2

case =3
input =amith kishore neil ram mohan nagi reddy kmit ngit
output =50

case =4
input =kmit ngit kmec
output =15

case =5
input =abc cde efg fgh ghi hjkl klmno lmnop opqrstu tuvx uvwxy wxyz
output =61

case =6
input =a aa aaa aaaa aaaaa aaaaaa
output =7

case =7
input =common monster sterlin linp plastic stick ticked
output =49

case =8
input =a ab abc abcd abcde abcdef abcdefg
output =35

case =9
input =time me bells
output =11

case =10
input =abcdefg bcdefg cdefg defg efg fg g
output =8

case =11
input =all lloyd door ortho thor horse sell lloyd dust stool tool link ink knee neet eternal algo go goto tour
output =86

case =12
input =link ink knee nest stamp ample please send end
output =39

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ShortEncodingOfWords.java
> ```java
> /*
>  * 
>  Given a list of words, we may encode it by writing a reference string S and a list of indexes A.
>
> For example, if the list of words is ["time", "me", "bell"], we can write it as S = "time#bell#" and indexes = [0, 2, 5].
>
> Then for each index, we will recover the word by reading from the reference string from that index until we reach a "#" character.
>
> What is the length of the shortest reference string S possible that encodes the given words?
>
> Example:
>
> Input:time me bell
> Output: 10
> Explanation: S = "time#bell#" and indexes = [0, 2, 5].
>  
>
> Note:
>
> 1 <= words.length <= 20, if violated print -1
> 1 <= words[i].length <= 7, if violated print -2
> Each word has only lowercase letters.
>
> =======TestCases======
> case =1
> input =abc cde efg fgh ghi hjkl klmno lmnop opqrstuv tuvx uvwxy wxyz amith kishore neil ram mohan nagi reddy kmit ngit
> output =-1
>
> case =2
> input =amith kishore neil ram mohan nagireddy kmit ngit
> output =-2
>
> case =3
> input =amith kishore neil ram mohan nagi reddy kmit ngit
> output =50
>
> case =4
> input =kmit ngit kmec
> output =15
>
> case =5
> input =abc cde efg fgh ghi hjkl klmno lmnop opqrstu tuvx uvwxy wxyz
> output =61
>
> case =6
> input =a aa aaa aaaa aaaaa aaaaaa
> output =7
>
> case =7
> input =common monster sterlin linp plastic stick ticked
> output =49
>
> case =8
> input =a ab abc abcd abcde abcdef abcdefg
> output =35
>
> case =9
> input =time me bells
> output =11
>
> case =10
> input =abcdefg bcdefg cdefg defg efg fg g
> output =8
>
> case =11
> input =all lloyd door ortho thor horse sell lloyd dust stool tool link ink knee neet eternal algo go goto tour
> output =86
>
> case =12
> input =link ink knee nest stamp ample please send end
> output =39
>
>  */
>
>
> import java.util.*;
>
> public class ShortEncodingOfWords {
>
> 	public static int minimumLengthEncoding(String[] words) {
>         Set<String> s = new HashSet<>(Arrays.asList(words));
>         for (String w : words)
>             for (int i = 1; i < w.length(); ++i)
>                 s.remove(w.substring(i));
>         int res = 0;
>         for (String w : s) res += w.length() + 1;
>         return res;
>     }
> 	
> 	
> 	public static void main(String[] args) {
>
> 		Scanner sc = new Scanner(System.in);
> 		String wordsString = sc.nextLine();
> 	    	String words[]= wordsString.split(" ");	   
> 			if(words.length>20 || words.length<=0){
> 				System.out.print("-1");
> 				return;
> 			}
> 			for(String s:words)
> 				if(s.length()>7 || s.length()<0){
> 				System.out.print("-2");
> 				return;
> 			}
> 	    	System.out.print(minimumLengthEncoding(words));        
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2044%20Solutions/ShortEncodingOfWords.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 44 Solutions/ShortEncodingOfWords.java
