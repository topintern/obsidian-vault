---
kind: "coding-problem"
title: "Gameof Strings (Day 75)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 75 Solutions/GameofStrings.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Gameof Strings (Day 75)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Pandit is playing a game of strings. As it is well known that he isn't very bright. 
So he needs your help in winning this game.

The game is very simple. You are given a string S of length N and an integer K. 
You have to print first K occurences(if for any character count < K then print them all) of every character in the given order.

 


### INPUT FORMAT


First line contains 2 integers N and K.

Second line contains the string S, comprising of only lowercase alphabets.



### OUTPUT FORMAT


Print the required string.


### Sample input 

10 3
abcaacbccb


### Sample output 

abcaacbcb

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · GameofStrings.txt
> ```java
> /*
>
> Pandit is playing a game of strings. As it is well known that he isn't very bright. 
> So he needs your help in winning this game.
>
> The game is very simple. You are given a string S of length N and an integer K. 
> You have to print first K occurences(if for any character count < K then print them all) of every character in the given order.
>
>  
>
> INPUT FORMAT
>
> First line contains 2 integers N and K.
>
> Second line contains the string S, comprising of only lowercase alphabets.
>
>
> OUTPUT FORMAT
>
> Print the required string.
>
> Sample input :
> 10 3
> abcaacbccb
>
> Sample output :
> abcaacbcb
>
>
> */
>
> import java.io.BufferedReader;
> import java.io.InputStreamReader;
> import java.util.HashMap;
> import java.util.Map;
>
> class GameofStrings {
> 	public static void main(String args[]) throws Exception {
>
> 		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String[] s = br.readLine().split(" ");
> 		int count = Integer.parseInt(s[1]);
> 		char[] tmp = br.readLine().toCharArray();
> 		StringBuilder builder = new StringBuilder();
> 		Map<Character, Integer> map = new HashMap<>();
> 		for (int i = 0; i < tmp.length; i++) {
> 			Integer cnt = map.get(tmp[i]);
> 			if (cnt == null || cnt == 0) {
> 				map.put(tmp[i], 1);
> 			} else {
> 				map.put(tmp[i], ++cnt);
> 			}
> 			if (cnt == null || cnt <= count) {
> 				builder.append(tmp[i]);
> 			}
> 		}
> 		System.out.println(builder.toString());
>
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2075%20Solutions/GameofStrings.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 75 Solutions/GameofStrings.txt
