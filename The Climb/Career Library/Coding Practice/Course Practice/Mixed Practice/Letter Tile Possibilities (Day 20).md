---
kind: "coding-problem"
title: "Letter Tile Possibilities (Day 20)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 20 Solutions/LetterTilePossibilities.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Letter Tile Possibilities (Day 20)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You have a set of tiles, where each tile has one letter tiles[i] printed on it.  
Return the number of possible non-empty sequences of letters you can make.


Example 1:
Input: "AAB"
Output: 8
Explanation: The possible sequences are "A", "B", "AA", "AB", "BA", "AAB", "ABA", "BAA".

Example 2:
Input: "AAABBC"
Output: 188

 
Note:
    1 <= tiles.length <= 7
    tiles consists of uppercase English letters.

-------TestCases-------

case =1
input =ABCD
output =64

case =2
input =ABBCCDDE
output =14458

case =3
input =AAABAA
output =26

case =4
input =BBCBCBCC
output =250

case =5
input =ABCXYZA
output =7012

case =6
input =ABBCCDACE
output =44225

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · LetterTilePossibilities.java
> ```java
> /*
> You have a set of tiles, where each tile has one letter tiles[i] printed on it.  
> Return the number of possible non-empty sequences of letters you can make.
>
>
> Example 1:
> Input: "AAB"
> Output: 8
> Explanation: The possible sequences are "A", "B", "AA", "AB", "BA", "AAB", "ABA", "BAA".
>
> Example 2:
> Input: "AAABBC"
> Output: 188
>
>  
> Note:
>     1 <= tiles.length <= 7
>     tiles consists of uppercase English letters.
>
> -------TestCases-------
>
> case =1
> input =ABCD
> output =64
>
> case =2
> input =ABBCCDDE
> output =14458
>
> case =3
> input =AAABAA
> output =26
>
> case =4
> input =BBCBCBCC
> output =250
>
> case =5
> input =ABCXYZA
> output =7012
>
> case =6
> input =ABBCCDACE
> output =44225
>
> */
> import java.util.*;
> class LetterTilePossibilities
> {
> 	public static int numTilePossibilities(String tiles) {
> 	int[] count = new int[26];
> 	
> 	for (char c : tiles.toCharArray()) 
> 		count[c - 'A']++;
> 	
> 	return dfs(count);
> 	}
>     
> 	static int dfs(int[] arr) {
> 		int sum = 0;
>
> 		for (int i = 0; i < 26; i++) {
> 		    if (arr[i] == 0) 
> 			continue;
> 		    sum++;
> 		    arr[i]--;
> 		    sum += dfs(arr);
> 		    arr[i]++;
> 		}
> 		return sum;
> 	}
>
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		String s=sc.next();
> 		System.out.println(numTilePossibilities(s));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2020%20Solutions/LetterTilePossibilities.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 20 Solutions/LetterTilePossibilities.java
