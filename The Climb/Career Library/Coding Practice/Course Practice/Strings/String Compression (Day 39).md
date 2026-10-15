---
kind: "coding-problem"
title: "String Compression (Day 39)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 39 Solutions/StringCompression.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# String Compression (Day 39)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given an array of characters, compress it in-place.

The length after compression must always be smaller than or equal to the original array.

Every element of the array should be a character (not int) of length 1.

After you are done modifying the input array in-place, return the new length of the array.

 
Follow up:
Could you solve it using only O(1) extra space?


Input:aabbccc

Output:6
Return 6, and the first 6 characters of the input array should be: a2b2c3


### Explanation

"aa" is replaced by "a2". "bb" is replaced by "b2". "ccc" is replaced by "c3".
 

Example 2:

Input:a

Output:1
first 1 characters of the input  should be: a


### Explanation

Nothing is replaced.
 

Example 3:

Input:abbbbbbbbbbbb


Output:4

and the first 4 characters of the input should be: ab12


### Explanation

Since the character "a" does not repeat, it is not compressed. "bbbbbbbbbbbb" is replaced by "b12".
Notice each digit has it's own entry in the array.

=========testCases=========
case =1
input =aaaaaaaaaabbbbb
output =5

case =2
input =abcdefg
output =7

case =3
input =abbcccddddeeeeffff
output =11

case =4
input =abababaaaaaaaaaaaaa
output =9

case =5
input =aaaaaaababbbbbbbbb
output =6

case =6
input =abbabbabbabb
output =12

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · StringCompression.txt
> ```java
> /*
>  * 
>  Given an array of characters, compress it in-place.
>
> The length after compression must always be smaller than or equal to the original array.
>
> Every element of the array should be a character (not int) of length 1.
>
> After you are done modifying the input array in-place, return the new length of the array.
>
>  
> Follow up:
> Could you solve it using only O(1) extra space?
>
>
> Input:aabbccc
>
> Output:6
> Return 6, and the first 6 characters of the input array should be: a2b2c3
>
> Explanation:
> "aa" is replaced by "a2". "bb" is replaced by "b2". "ccc" is replaced by "c3".
>  
>
> Example 2:
>
> Input:a
>
> Output:1
> first 1 characters of the input  should be: a
>
> Explanation:
> Nothing is replaced.
>  
>
> Example 3:
>
> Input:abbbbbbbbbbbb
>
>
> Output:4
>
> and the first 4 characters of the input should be: ab12
>
> Explanation:
> Since the character "a" does not repeat, it is not compressed. "bbbbbbbbbbbb" is replaced by "b12".
> Notice each digit has it's own entry in the array.
>
> =========testCases=========
> case =1
> input =aaaaaaaaaabbbbb
> output =5
>
> case =2
> input =abcdefg
> output =7
>
> case =3
> input =abbcccddddeeeeffff
> output =11
>
> case =4
> input =abababaaaaaaaaaaaaa
> output =9
>
> case =5
> input =aaaaaaababbbbbbbbb
> output =6
>
> case =6
> input =abbabbabbabb
> output =12
>
>  */
>
> package Elite2020;
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
>
> public class StringCompression {
>
> 	public static int compress(char[] chars) {
>         int indexAns = 0, index = 0;
>         while(index < chars.length){
>             char currentChar = chars[index];
>             int count = 0;
>             while(index < chars.length && chars[index] == currentChar){
>                 index++;
>                 count++;
>             }
>             chars[indexAns++] = currentChar;
>             if(count != 1)
>                 for(char c : Integer.toString(count).toCharArray()) 
>                     chars[indexAns++] = c;
>         }
>         return indexAns;
>     }
> 	
> 	public static void main(String[] args)  throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		
> 		//string to char array
> 		char[] chars = str.toCharArray();
> 		
> 		System.out.println(compress(chars));
> 		
> 	}
> 	
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2039%20Solutions/StringCompression.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 39 Solutions/StringCompression.txt
