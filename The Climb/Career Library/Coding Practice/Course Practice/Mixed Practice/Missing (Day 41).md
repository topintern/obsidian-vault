---
kind: "coding-problem"
title: "Missing (Day 41)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 41 Solutions/Missing.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Missing (Day 41)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given an unsorted integer array, find the smallest missing positive integer.

Example 1:

Input:1 2 0
Output: 3
Example 2:

Input: 3 4 -1 1
Output: 2
Example 3:

Input: 7 8 9 11 12
Output: 1
Note:

Your algorithm should run in O(n) time and uses constant extra space.

------------------------------------------------------------------------------

case=1
input=2 6 3 8 4 9 -1 -2 11 15
output=1

case=2
input=1 2 6 3 8 4 9 11 15
output=5

case=3
input=10 12 1 11 13 2 8 7 9 6 5 3
output=4

case=4
input=10 12 1 11 13 2 8 7 9 6 5 3 4 16 20 19 18 17 
output=14

case=5
input=1 3 4 2 5 7 6 12 13 15 20 10 8 9
output=11

case=6
input=10 11 12 1 2 3 4 5 6 7 8 9 13 14 16 15 18 19
output=17

case =7
input =8 7 6 5 4 2 1
output =3

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Missing.java
> ```java
> /*
>  * 
>  Given an unsorted integer array, find the smallest missing positive integer.
>
> Example 1:
>
> Input:1 2 0
> Output: 3
> Example 2:
>
> Input: 3 4 -1 1
> Output: 2
> Example 3:
>
> Input: 7 8 9 11 12
> Output: 1
> Note:
>
> Your algorithm should run in O(n) time and uses constant extra space.
>
> ------------------------------------------------------------------------------
>
> case=1
> input=2 6 3 8 4 9 -1 -2 11 15
> output=1
>
> case=2
> input=1 2 6 3 8 4 9 11 15
> output=5
>
> case=3
> input=10 12 1 11 13 2 8 7 9 6 5 3
> output=4
>
> case=4
> input=10 12 1 11 13 2 8 7 9 6 5 3 4 16 20 19 18 17 
> output=14
>
> case=5
> input=1 3 4 2 5 7 6 12 13 15 20 10 8 9
> output=11
>
> case=6
> input=10 11 12 1 2 3 4 5 6 7 8 9 13 14 16 15 18 19
> output=17
>
> case =7
> input =8 7 6 5 4 2 1
> output =3
>
>
>  */
>
>
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class Missing {
>
> 	public static int firstMissingPositive(int[] nums) {
>         if(nums == null || nums.length == 0) return 1;          //case: nums == null or nums == [], return 1
>         for(int i = 0;i < nums.length;i++){                     //use nums array itself, the ideal array should be {1,2,3,4}
>             int curr = nums[i];                                 //swap if nums[index] != index + 1;
>             while(curr - 1 >= 0 && curr - 1 < nums.length && curr != nums[curr-1]){
>                 int next = nums[curr-1];
>                 nums[curr-1] = curr;
>                 curr = next;
>             }
>         }
>         for(int i = 0;i< nums.length;i++){                      //check if nums[index] == index + 1;
>             if(nums[i] != i+1) return i+1;
>         }
>         return nums.length+1;                                   //corner case: {1,2,3,4} return 5
>     }
> 	
> 	public static void main(String args[] ) throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		String[] numberline = str.split(" ");
> 		int[] nums = Arrays.asList(numberline).stream().mapToInt(Integer::parseInt).toArray();
>
> 		System.out.println(firstMissingPositive(nums));   
> 		
> 		}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2041%20Solutions/Missing.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 41 Solutions/Missing.java
