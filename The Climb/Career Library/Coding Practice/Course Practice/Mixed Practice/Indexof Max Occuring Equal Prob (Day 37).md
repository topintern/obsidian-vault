---
kind: "coding-problem"
title: "Indexof Max Occuring Equal Prob (Day 37)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 37 Solutions/IndexofMaxOccuringEqualProb.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Indexof Max Occuring Equal Prob (Day 37)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given an array of integers, find the most occurring element of the array and return any one of its indexes randomly with equal probability.

Examples:

Input: 
-1 4 9 7 7 2 7 3 0 9 6 5 7 8 9

Output:  
Element with maximum frequency present at index 6
OR
Element with maximum frequency present at Index 3
OR
Element with maximum frequency present at index 4
OR
Element with maximum frequency present at index 12

All outputs above have equal probability.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · IndexofMaxOccuringEqualProb.txt
> ```java
> /*
>  * 
>  Given an array of integers, find the most occurring element of the array and return any one of its indexes randomly with equal probability.
>
> Examples:
>
> Input: 
> -1 4 9 7 7 2 7 3 0 9 6 5 7 8 9
>
> Output:  
> Element with maximum frequency present at index 6
> OR
> Element with maximum frequency present at Index 3
> OR
> Element with maximum frequency present at index 4
> OR
> Element with maximum frequency present at index 12
>
> All outputs above have equal probability.
>
>
>
>  */
>
> package Elite2020;
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
> import java.util.*;
>
> public class IndexofMaxOccuringEqualProb {
>
> 	
> 	// Function to return index of most occurring element 
> 			// of the array randomly with equal probability 
> 			static void findRandomIndexOfMax(int arr[], int n) 
> 			{ 
> 			    // freq store frequency of each element in the array 
> 			    HashMap<Integer, Integer> mp = new HashMap<Integer, Integer>(); 
> 			    for (int i = 0; i < n; i++) 
> 			        if(mp.containsKey(arr[i])) 
> 			        { 
> 			            mp.put(arr[i], mp.get(arr[i]) + 1); 
> 			        } 
> 			        else
> 			        { 
> 			            mp.put(arr[i], 1); 
> 			        } 
> 			  
> 			    int max_element = Integer.MIN_VALUE; // stores max occurring element 
> 			  
> 			    // stores count of max occurring element 
> 			    int max_so_far = Integer.MIN_VALUE; 
> 			  
> 			    // traverse each pair in map and find maximum 
> 			    // occurring element and its frequency 
> 			    for (Map.Entry<Integer, Integer> p : mp.entrySet())  
> 			    { 
> 			        if (p.getValue() > max_so_far) 
> 			        { 
> 			            max_so_far = p.getValue(); 
> 			            max_element = p.getKey(); 
> 			        } 
> 			    } 
> 			      
> 			    // generate a random number between [1, max_so_far] 
> 			    int r = (int) ((new Random().nextInt(max_so_far) % max_so_far) + 1); 
> 			  
> 			    // traverse array again and return index of rth 
> 			    // occurrence of max element 
> 			    for (int i = 0, count = 0; i < n; i++) 
> 			    { 
> 			        if (arr[i] == max_element) 
> 			            count++; 
> 			  
> 			        // print index of rth occurrence of max element 
> 			        if (count == r) 
> 			        { 
> 			            System.out.print("Element with maximum frequency present "
> 			                +"at index " + i +"\n"); 
> 			            break; 
> 			        } 
> 			    } 
> 			} 
> 			  
> 			// Driver code 
> 			public static void main(String[] args) throws IOException
> 		    { 
> 		    	 BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		 		String str = br.readLine();
> 		 		
> 		 		String[] numline = str.split(" ");
> 		 		int[] arr = Arrays.asList(numline).stream().mapToInt(Integer::parseInt).toArray();
> 		     
> 			    int n = arr.length; 
> 			    findRandomIndexOfMax(arr, n); 
> 			} 
> 			
> 			
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2037%20Solutions/IndexofMaxOccuringEqualProb.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 37 Solutions/IndexofMaxOccuringEqualProb.txt
