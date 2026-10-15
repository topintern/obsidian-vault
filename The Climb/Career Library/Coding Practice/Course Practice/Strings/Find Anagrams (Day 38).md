---
kind: "coding-problem"
title: "Find Anagrams (Day 38)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 38 Solutions/FindAnagrams.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Find Anagrams (Day 38)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Problem

The source has reference code without a separate problem statement. Establish its inputs, expected outputs, and constraints before practising.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · FindAnagrams.txt
> ```java
> package Elite2020;
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
>
> /*
>
> Given a list of words  print all anagrams together.
>
> For example  if the given list of words is {but,tac,god,act, dog, cat, tub}
> then output would be groups of anagrams [but,tub][tac,act,cat][god, dog]
>
>
> Sample Input:
> pan nap god bat bag dog tub
>
> Output :
> [pan, nap]
> [god, dog]
>  
>
> Note : 
> 1) Print the group of anagrams only if the size of group is more than 1
> 2) Order of words in output should be same as order given in input.
> 3) Print -1, if no group of anagrams found
>
> */
>
> // Java program to print anagrams 
> // together using dictionary 
> import java.util.*; 
>
> public class FindAnagrams { 
>
> 	private static void printAnagrams(String arr[]) 
> 	{ 
> 		HashMap<Integer, List<String> > map = new HashMap<>(); 
>
> 		// loop over all words 
> 		for (int i = 0; i < arr.length; i++) { 
>
> 			// convert to char array, sort and 
> 			// then re-convert to string 
> 			String word = arr[i]; 
> 			char[] letters = word.toCharArray(); 
> 			Arrays.sort(letters); 
> 			String newWord = new String(letters); 
>
> 			// calculate hashcode of string 
> 			// after sorting 
> 			int n = newWord.hashCode(); 
> 			if (map.containsKey(n)) { 
>
> 				// Here, we already have 
> 				// a word for the hashcode 
> 				List<String> words = map.get(n); 
> 				words.add(word); 
> 				map.put(n, words); 
> 			} 
> 			else { 
>
> 				// This is the first time we are 
> 				// adding a word for a specific 
> 				// hashcode 
> 				List<String> words = new ArrayList<>(); 
> 				words.add(word); 
> 				map.put(n, words); 
> 			} 
> 		} 
>
> 		// print all the values where size is > 1 
> 		// If you want to print non-anagrams, 
> 		// just print the values having size = 1
> 		int flag=0;
> 		for (Integer i : map.keySet()) { 
> 			List<String> values = map.get(i); 
> 			if (values.size() > 1) { 
> 			    //values.forEach(s -> System.out.print(s+" "));
> 			   System.out.println(values); 
> 			   flag=1;
> 			} 
> 		} 
> 		if(flag==0)
> 		System.out.println("-1");
> 		 //System.out.println("restful, fluster \n mar, ram, arm \n ");
> 	} 
>
> 	public static void main(String[] args) throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String[] arrwords = br.readLine().split(" ");
> 		
> 		printAnagrams(arrwords); 
> 	} 
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2038%20Solutions/FindAnagrams.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 38 Solutions/FindAnagrams.txt
