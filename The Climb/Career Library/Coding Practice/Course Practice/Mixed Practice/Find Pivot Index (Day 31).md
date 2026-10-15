---
kind: "coding-problem"
title: "Find Pivot Index (Day 31)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 31 Solutions/FindPivotIndex.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Find Pivot Index (Day 31)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given an array of integers nums, write a method that returns the "pivot" index of this array.

We define the pivot index as the index where the sum of the numbers to the left of the index is equal to the sum of the numbers to the right of the index.

If no such index exists, we should return -1. If there are multiple pivot indexes, you should return the left-most pivot index.

Example 1:

Input:1 7 3 6 5 6
Output: 3


### Explanation: 

The sum of the numbers to the left of index 3 (nums[3] = 6) is equal to the sum of numbers to the right of index 3.
Also, 3 is the first index where this occurs.
 

Input: 1 2 3
Output: -1

### Explanation: 

There is no index that satisfies the conditions in the problem statement.
 

Note:

The length of nums will be in the range [0, 10000].
Each element nums[i] will be an integer in the range [-1000, 1000].

case =1
input =1 2 3 4 5 6 7 8 9 0 9 8 7 6 5 4 3 2 1
output =9

case =2
input =2 4 3 6 4 7 9 3 5 2 4 7 4 5 6 3 8 2 4 1 9
output =-1

case =3
input =1 14 2 13 3 12 8 4 11 5 10 6 9
output =6

case =4
input =23 15 78 45 65 4 10 154 62
output =5

case =5
input =125 126 6 75 65 45 46 20
output =2

case =6
input =895 0 0 665 123 54 53
output =1

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · FindPivotIndex.java
> ```java
> /*
>  * 
>  Given an array of integers nums, write a method that returns the "pivot" index of this array.
>
> We define the pivot index as the index where the sum of the numbers to the left of the index is equal to the sum of the numbers to the right of the index.
>
> If no such index exists, we should return -1. If there are multiple pivot indexes, you should return the left-most pivot index.
>
> Example 1:
>
> Input:1 7 3 6 5 6
> Output: 3
>
> Explanation: 
> The sum of the numbers to the left of index 3 (nums[3] = 6) is equal to the sum of numbers to the right of index 3.
> Also, 3 is the first index where this occurs.
>  
>
> Input: 1 2 3
> Output: -1
> Explanation: 
> There is no index that satisfies the conditions in the problem statement.
>  
>
> Note:
>
> The length of nums will be in the range [0, 10000].
> Each element nums[i] will be an integer in the range [-1000, 1000].
>
> case =1
> input =1 2 3 4 5 6 7 8 9 0 9 8 7 6 5 4 3 2 1
> output =9
>
> case =2
> input =2 4 3 6 4 7 9 3 5 2 4 7 4 5 6 3 8 2 4 1 9
> output =-1
>
> case =3
> input =1 14 2 13 3 12 8 4 11 5 10 6 9
> output =6
>
> case =4
> input =23 15 78 45 65 4 10 154 62
> output =5
>
> case =5
> input =125 126 6 75 65 45 46 20
> output =2
>
> case =6
> input =895 0 0 665 123 54 53
> output =1
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
>
> public class FindPivotIndex {
>
> 	  public static int pivotIndex(int[] nums) {
> 	        int sum = 0, leftsum = 0;
> 	        for (int x: nums) sum += x;
> 	        for (int i = 0; i < nums.length; ++i) {
> 	            if (leftsum == sum - leftsum - nums[i]) return i;
> 	            leftsum += nums[i];
> 	        }
> 	        return -1;
> 	    }
> 	  
> 	  public static void main(String args[] ) throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 			String str = br.readLine();
> 			String[] numbers = str.split(" ");
> 			int[] arr = Arrays.asList(numbers).stream().mapToInt(Integer::parseInt).toArray();
> 			System.out.println(pivotIndex(arr));
> 			}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2031%20Solutions/FindPivotIndex.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 31 Solutions/FindPivotIndex.java
