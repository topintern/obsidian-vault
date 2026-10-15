---
kind: "coding-problem"
title: "Move Zeros (Day 29)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 29 Solutions/MoveZeros.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Move Zeros (Day 29)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Example:

Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
Note:

You must do this in-place without making a copy of the array.
Minimize the total number of operations.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MoveZeros.java
> ```java
> /*
>  * 
>  Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.
>
> Example:
>
> Input: [0,1,0,3,12]
> Output: [1,3,12,0,0]
> Note:
>
> You must do this in-place without making a copy of the array.
> Minimize the total number of operations.
>
>
>
>
>
>  */
>
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class MoveZeros {
>
> 	public static void moveZeroes(int[] nums) {
>
> 	    int j = 0;
> 	    for(int i = 0; i < nums.length; i++) {
> 	        if(nums[i] != 0) {
> 	            int temp = nums[j];
> 	            nums[j] = nums[i];
> 	            nums[i] = temp;
> 	            j++;
> 	        }
> 	    }
> 	}
> 	
> 	public static void main(String args[] ) throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		
> 		String[] numline = str.split(" ");
> 		int[] nums = Arrays.asList(numline).stream().mapToInt(Integer::parseInt).toArray();
> 		moveZeroes(nums);
> 		System.out.println(Arrays.toString(nums));   
> 		
> 		}
> 	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2029%20Solutions/MoveZeros.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 29 Solutions/MoveZeros.java
