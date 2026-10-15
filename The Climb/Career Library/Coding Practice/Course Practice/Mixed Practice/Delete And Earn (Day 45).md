---
kind: "coding-problem"
title: "Delete And Earn (Day 45)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 45 Solutions/DeleteAndEarn.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Delete And Earn (Day 45)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given an array nums of integers, you can perform operations on the array.

In each operation, you pick any nums[i] and delete it to earn nums[i] points. After, you must delete every element equal to nums[i] - 1 or nums[i] + 1.

You start with 0 points. Return the maximum number of points you can earn by applying such operations.

Example 1:

Input: 3 4 2
Output: 6

### Explanation: 

Delete 4 to earn 4 points, consequently 3 is also deleted.
Then, delete 2 to earn 2 points. 6 total points are earned.
 

Example 2:

Input: 2 2 3 3 3 4
Output: 9

### Explanation: 

Delete 3 to earn 3 points, deleting both 2's and the 4.
Then, delete 3 again to earn 3 points, and 3 again to earn 3 points.
9 total points are earned.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · DeleteAndEarn.java
> ```java
> /*
>  * 
> Given an array nums of integers, you can perform operations on the array.
>
> In each operation, you pick any nums[i] and delete it to earn nums[i] points. After, you must delete every element equal to nums[i] - 1 or nums[i] + 1.
>
> You start with 0 points. Return the maximum number of points you can earn by applying such operations.
>
> Example 1:
>
> Input: 3 4 2
> Output: 6
> Explanation: 
> Delete 4 to earn 4 points, consequently 3 is also deleted.
> Then, delete 2 to earn 2 points. 6 total points are earned.
>  
>
> Example 2:
>
> Input: 2 2 3 3 3 4
> Output: 9
> Explanation: 
> Delete 3 to earn 3 points, deleting both 2's and the 4.
> Then, delete 3 again to earn 3 points, and 3 again to earn 3 points.
> 9 total points are earned.
>   
>  */
>
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class DeleteAndEarn {
>
> 	 public static int deleteAndEarn(int[] nums) {
> 	        int n = 10001;
> 	        int[] values = new int[n];
> 	        for (int num : nums)
> 	            values[num] += num;
>
> 	        int take = 0, skip = 0;
> 	        for (int i = 0; i < n; i++) {
> 	            int takei = skip + values[i];
> 	            int skipi = Math.max(skip, take);
> 	            take = takei;
> 	            skip = skipi;
> 	        }
> 	        return Math.max(take, skip);
> 	    }
> 	 
> 	 public static void main(String args[] ) throws IOException {
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 			String str = br.readLine();
> 			String[] numbers = str.split(" ");
> 			int[] nums = Arrays.asList(numbers).stream().mapToInt(Integer::parseInt).toArray();
> 			System.out.println(deleteAndEarn(nums));
> 	}	 
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2045%20Solutions/DeleteAndEarn.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 45 Solutions/DeleteAndEarn.java
