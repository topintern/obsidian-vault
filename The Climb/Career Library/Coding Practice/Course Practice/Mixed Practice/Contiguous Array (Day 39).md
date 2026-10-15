---
kind: "coding-problem"
title: "Contiguous Array (Day 39)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 39 Solutions/ContiguousArray.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Contiguous Array (Day 39)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

Example 1:
Input:0 1
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.

Example 2:
Input:0 1 0
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.

==========================================

The idea is to change 0 in the original array to -1. Thus, if we find SUM[i, j] == 0 then we know there are even number of -1 and 1 between index i and j. Also put the sum to index mapping to a HashMap to make search faster.

========TestCase===
case =1
input =0 1 0 1 0
output =4

case =2
input =0 0 0 1 1 1 0 1 0 1 0 1 0 0
output =12

case =3
input =0 0 0 0 0 0 0
output =0

case =4
input =1 0 1 0 1 0 1 1 1 0 0 0 1 0 1 0 1 0
output =18

case =5
input =1 1 1 1 0 0 0 0 1 1 1 1 0 0 0 0
output =16

case =6
input =1 0 1 0 1 1 0 0 1 1 1 0 0 0 1 1 1 1 0 0 0 0
output =22

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ContiguousArray.txt
> ```java
> /*
>  * 
>  Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.
>
> Example 1:
> Input:0 1
> Output: 2
> Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
>
> Example 2:
> Input:0 1 0
> Output: 2
> Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
>
> ==========================================
>
> The idea is to change 0 in the original array to -1. Thus, if we find SUM[i, j] == 0 then we know there are even number of -1 and 1 between index i and j. Also put the sum to index mapping to a HashMap to make search faster.
>
> ========TestCase===
> case =1
> input =0 1 0 1 0
> output =4
>
> case =2
> input =0 0 0 1 1 1 0 1 0 1 0 1 0 0
> output =12
>
> case =3
> input =0 0 0 0 0 0 0
> output =0
>
> case =4
> input =1 0 1 0 1 0 1 1 1 0 0 0 1 0 1 0 1 0
> output =18
>
> case =5
> input =1 1 1 1 0 0 0 0 1 1 1 1 0 0 0 0
> output =16
>
> case =6
> input =1 0 1 0 1 1 0 0 1 1 1 0 0 0 1 1 1 1 0 0 0 0
> output =22
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
> public class ContiguousArray {
>
> 	 public static int findMaxLength(int[] nums) {
> 	        Map<Integer, Integer> map = new HashMap<>();
> 	        map.put(0, -1);
> 	        int maxlen = 0, count = 0;
> 	        for (int i = 0; i < nums.length; i++) {
> 	            count = count + (nums[i] == 1 ? 1 : -1);
> 	            if (map.containsKey(count)) {
> 	                maxlen = Math.max(maxlen, i - map.get(count));
> 	            } else {
> 	                map.put(count, i);
> 	            }
> 	        }
> 	        return maxlen;
> 	    }
> 	 
> 	 public static void main(String args[] ) throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 			String str = br.readLine();
> 			String[] numberline = str.split(" ");
> 			int[] nums = Arrays.asList(numberline).stream().mapToInt(Integer::parseInt).toArray();
>
> 			System.out.println(findMaxLength(nums));   
> 			
> 			}
> 	 
> 	
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2039%20Solutions/ContiguousArray.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 39 Solutions/ContiguousArray.txt
