---
kind: "coding-problem"
title: "Sub Array Sum (Day 13)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day13 Solutions/SubArraySum.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Sub Array Sum (Day 13)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.

Example 1:
Input:nums = [1,1,1], k = 2

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SubArraySum.java
> ```java
> /*
>  * 
>   Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.
>
> Example 1:
> Input:nums = [1,1,1], k = 2
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
> import java.util.HashMap;
>
> public class SubArraySum {
>
> 	
> 	 public static int subarraySum(int[] nums, int k) {
> 	        int count = 0, sum = 0;
> 	        HashMap < Integer, Integer > map = new HashMap < > ();
> 	        map.put(0, 1);
> 	        for (int i = 0; i < nums.length; i++) {
> 	            sum += nums[i];
> 	            if (map.containsKey(sum - k))
> 	                count += map.get(sum - k);
> 	            map.put(sum, map.getOrDefault(sum, 0) + 1);
> 	        }
> 	        return count;
> 	    }
> 	 
> 	 public static void main(String args[] ) throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 			String str = br.readLine();
> 			String[] numberline = str.split(" ");
> 			int[] nums = Arrays.asList(numberline).stream().mapToInt(Integer::parseInt).toArray();
> 			int k = Integer.parseInt(br.readLine());
>
> 			System.out.println(subarraySum(nums,k));   
> 			
> 			}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day13%20Solutions/SubArraySum.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day13 Solutions/SubArraySum.java
