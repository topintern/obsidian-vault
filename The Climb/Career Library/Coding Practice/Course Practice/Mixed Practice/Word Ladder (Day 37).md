---
kind: "coding-problem"
title: "Word Ladder (Day 37)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 37 Solutions/WordLadder.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Word Ladder (Day 37)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord, such that:

Only one letter can be changed at a time.
Each transformed word must exist in the word list. Note that beginWord is not a transformed word.
Note:

Return 0 if there is no such transformation sequence.
All words have the same length.
All words contain only lowercase alphabetic characters.
You may assume no duplicates in the word list.
You may assume beginWord and endWord are non-empty and are not the same.
Example 1:

Input:
hit
cog
hot dot dog lot log cog

Output: 5

Explanation: As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5.


Example 2:

Input:
hit
cog
hot dot dog lot log

Output: 0

Explanation: The endWord "cog" is not in wordList, therefore no possible transformation.


=========================================================

The basic idea is:

1). Use BFS to find the shortest distance between start and end, tracing the distance of crossing nodes from start node to end node, and store node's next level neighbors to HashMap;

2). Use DFS to output paths with the same distance as the shortest distance from distance HashMap: compare if the distance of the next level node equals the distance of the current node + 1.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · WordLadder.txt
> ```java
> /*
>  * 
>  Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord, such that:
>
> Only one letter can be changed at a time.
> Each transformed word must exist in the word list. Note that beginWord is not a transformed word.
> Note:
>
> Return 0 if there is no such transformation sequence.
> All words have the same length.
> All words contain only lowercase alphabetic characters.
> You may assume no duplicates in the word list.
> You may assume beginWord and endWord are non-empty and are not the same.
> Example 1:
>
> Input:
> hit
> cog
> hot dot dog lot log cog
>
> Output: 5
>
> Explanation: As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
> return its length 5.
>
>
> Example 2:
>
> Input:
> hit
> cog
> hot dot dog lot log
>
> Output: 0
>
> Explanation: The endWord "cog" is not in wordList, therefore no possible transformation.
>
>
> =========================================================
>
> The basic idea is:
>
> 1). Use BFS to find the shortest distance between start and end, tracing the distance of crossing nodes from start node to end node, and store node's next level neighbors to HashMap;
>
> 2). Use DFS to output paths with the same distance as the shortest distance from distance HashMap: compare if the distance of the next level node equals the distance of the current node + 1.
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
> public class WordLadder {
> 	
> 	 public static int ladderLength(String beginWord, String endWord, List<String> wordList) {
> 	        Set<String> dict = new HashSet<>(wordList), vis = new HashSet<>();
> 	        Queue<String> q = new LinkedList<>();
> 	        q.offer(beginWord);
> 	        for (int len = 1; !q.isEmpty(); len++) {
> 	            for (int i = q.size(); i > 0; i--) {
> 	                String w = q.poll();
> 	                if (w.equals(endWord)) return len;
>
> 	                for (int j = 0; j < w.length(); j++) {
> 	                    char[] ch = w.toCharArray();
> 	                    for (char c = 'a'; c <= 'z'; c++) {
> 	                        if (c == w.charAt(j)) continue;
> 	                        ch[j] = c;
> 	                        String nb = String.valueOf(ch);
> 	                        if (dict.contains(nb) && vis.add(nb)) q.offer(nb);
> 	                    }
> 	                }
> 	            }
> 	        }
> 	        return 0;
> 	    }
> 	 
> 	
> 	public static void main(String[] args)  throws IOException
>     { 
>    	 BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String beginWord = br.readLine();
> 		String endWord = br.readLine();
> 		String wordListline = br.readLine();
> 		List<String> wordList = Arrays.asList(wordListline.split(" "));
> 		  System.out.println(ladderLength(beginWord,endWord,wordList));
>     }
> 		
> 		
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2037%20Solutions/WordLadder.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 37 Solutions/WordLadder.txt
