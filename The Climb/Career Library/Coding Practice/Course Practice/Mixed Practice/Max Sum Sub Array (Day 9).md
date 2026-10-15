---
kind: "coding-problem"
title: "Max Sum Sub Array (Day 9)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 9 Solutions/MaxSumSubArray.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Max Sum Sub Array (Day 9)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Example:

Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
Follow up:

If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MaxSumSubArray.java
> ```java
> /*
>  * 
>  * 
>
> Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.
>
> Example:
>
> Input: [-2,1,-3,4,-1,2,1,-5,4],
> Output: 6
> Explanation: [4,-1,2,1] has the largest sum = 6.
> Follow up:
>
> If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.
>
>
>  */
>
>
> package Elite2020;
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class MaxSumSubArray {
> 	
> 	 public static int maxSubArray(int[] nums) {
> 		    int n = nums.length, maxSum = nums[0];
> 		    for(int i = 1; i < n; ++i) {
> 		      if (nums[i - 1] > 0) 
> 				  nums[i] += nums[i - 1];
> 		      maxSum = Math.max(nums[i], maxSum);
> 		    }
> 		    return maxSum;
> 		  }
> 	
> 	 public static void main(String args[] ) throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		
> 			String str = br.readLine();
> 			String[] numberline = str.split(" ");
> 			int[] arr = Arrays.asList(numberline).stream().mapToInt(Integer::parseInt).toArray();
> 			System.out.println(maxSubArray(arr));   // returns 4
> 			
> 			}
>
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%209%20Solutions/MaxSumSubArray.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 9 Solutions/MaxSumSubArray.java
