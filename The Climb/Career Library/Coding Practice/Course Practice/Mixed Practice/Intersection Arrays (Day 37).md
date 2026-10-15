---
kind: "coding-problem"
title: "Intersection Arrays (Day 37)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 37 Solutions/IntersectionArrays.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Intersection Arrays (Day 37)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Write a Program to find the common string(s) of 2 arrays of strings.
 

Input:ram Laxman krishna
ram Seetha raju

Output: ram


### Explanation 

First line of input represents strings(without space) array 1
Second line of input represents strings(without space) array 2
output is common strings between two array i.e ram.
length of 2 arrays of strings can be different also.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · IntersectionArrays.txt
> ```java
> /*
>  * 
> Write a Program to find the common string(s) of 2 arrays of strings.
>  
>
> Input:ram Laxman krishna
> ram Seetha raju
>
> Output: ram
>
> Explanation :
> First line of input represents strings(without space) array 1
> Second line of input represents strings(without space) array 2
> output is common strings between two array i.e ram.
> length of 2 arrays of strings can be different also.
>
> */
>
> package Elite2020;
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.*;
>
> public class IntersectionArrays {
>
> 	public static void main(String[] args)  throws IOException
>     { 
>    	 BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		
> 		String[] firstArray = str.split(" ");
> 		str = br.readLine();
> 		
> 		String[] secondArray = str.split(" ");
> 	     
> 	    HashSet<String> set = new HashSet<>(); 
> 	     
> 	    set.addAll(Arrays.asList(firstArray));
> 	     
> 	    set.retainAll(Arrays.asList(secondArray));
> 	    
> 	    String[] intersection = {};
> 	    intersection = set.toArray(intersection);
> 	     
> 	    System.out.println(Arrays.toString(intersection));
> 	  }
> 	
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2037%20Solutions/IntersectionArrays.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 37 Solutions/IntersectionArrays.txt
