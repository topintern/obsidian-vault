---
kind: "coding-problem"
title: "Shortest Dis Words (Day 36)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 36 Solutions/ShortestDisWords.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Shortest Dis Words (Day 36)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a list of words and two words word1 and word2, return the shortest distance between these two words in the list.

word1 and word2 may be the same and they represent two individual words in the list.

Example:
Assume that words = ["practice", "makes", "perfect", "coding", "makes"].

Input: practice makes perfect coding makes
makes coding
Output: 1


Input: practice makes perfect coding makes
makes makes
Output: 3

Input: good bad worst good good bad bad
bad bad
Output: 1

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ShortestDisWords.java
> ```java
> /*
>  * 
>  * 
>  * 
>
> Given a list of words and two words word1 and word2, return the shortest distance between these two words in the list.
>
> word1 and word2 may be the same and they represent two individual words in the list.
>
> Example:
> Assume that words = ["practice", "makes", "perfect", "coding", "makes"].
>
> Input: practice makes perfect coding makes
> makes coding
> Output: 1
>
>
> Input: practice makes perfect coding makes
> makes makes
> Output: 3
>
> Input: good bad worst good good bad bad
> bad bad
> Output: 1
>
>
>  */
>
> package Leetcode;
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
>
> public class ShortestDisWords {
> 	
> 	 public static int shortestWordDistance(String[] words, String word1, String word2) {
> 		  int index1 = -1,index2=-1, shortDist = Integer.MAX_VALUE;      
> 		    for(int i = 0, j= 0;j<words.length;i++,j++)
> 		    {
> 		        if(words[i].equals(word1))
> 		        {
> 		            index1 = i;		            
> 		            if(index2 > -1 && index1 != index2)
> 		            shortDist = Math.min(shortDist,Math.abs(index1-index2));    
> 		        } 
> 		        if(words[j].equals(word2))
> 		        {
> 		            index2 = j;
> 		            if(index1 > -1 && index1 != index2)
> 		            shortDist = Math.min(shortDist,Math.abs(index1-index2)); 
> 		        }		        
> 		    }		        
> 		   return shortDist;       
>      }
> 	 
> 	 public static void main(String args[] ) throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 			String str = br.readLine();
> 			String[] wordslist = str.split(" ");
> 			str = br.readLine();
> 			String[] words = str.split(" ");
> 			String word1=words[0];
> 			String word2=words[1];
> 			System.out.println(shortestWordDistance(wordslist,word1,word2));
> 	 } 
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2036%20Solutions/ShortestDisWords.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 36 Solutions/ShortestDisWords.java
