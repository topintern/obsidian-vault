---
kind: "coding-problem"
title: "Longest Increasing Subseq1 (Day 28)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 28 Solutions/LongestIncreasingSubseq1.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Longest Increasing Subseq1 (Day 28)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given an unsorted array of integers, find the length of longest increasing subsequence.

Example:

Input: [10,9,2,5,3,7,101,18]
Output: 4 
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
Note:

There may be more than one LIS combination, it is only necessary for you to return the length.
Your algorithm should run in O(n2) complexity.
Follow up: Could you improve it to O(n log n) time complexity?

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · LongestIncreasingSubseq1.java
> ```java
> /*
>  * 
>  Given an unsorted array of integers, find the length of longest increasing subsequence.
>
> Example:
>
> Input: [10,9,2,5,3,7,101,18]
> Output: 4 
> Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
> Note:
>
> There may be more than one LIS combination, it is only necessary for you to return the length.
> Your algorithm should run in O(n2) complexity.
> Follow up: Could you improve it to O(n log n) time complexity?
>
>
>  */
>
>
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.*;
>
> public class LongestIncreasingSubseq {
>
> 	 public static int lengthOfLIS(int[] nums) {
> 	        int[] dp = new int[nums.length];
> 	        int len = 0;
> 	        for (int num : nums) {
> 	            int i = Arrays.binarySearch(dp, 0, len, num);
> 	            if (i < 0) {
> 	                i = -(i + 1);
> 	            }
> 	            dp[i] = num;
> 	            if (i == len) {
> 	                len++;
> 	            }
> 	        }
> 	        return len;
> 	    }
> 	 
> 	 public static void main(String args[] ) throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 			String str = br.readLine();
> 			String[] numbers = str.split(" ");
> 			int[] nums = Arrays.asList(numbers).stream().mapToInt(Integer::parseInt).toArray();
> 			System.out.println(lengthOfLIS(nums));
> 			}
> 	 
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2028%20Solutions/LongestIncreasingSubseq1.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 28 Solutions/LongestIncreasingSubseq1.java
