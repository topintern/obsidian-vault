---
kind: "coding-problem"
title: "Container With Most Water (Day 25)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elie Day 25 Solutions/ContainerWithMostWater.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Container With Most Water (Day 25)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains 
 the most water.

Note: You may not slant the container and n is at least 2.

 



The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

 

Example:

Input: [1,8,6,2,5,4,8,3,7]
Output: 49

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ContainerWithMostWater.java
> ```java
> /*
>  * 
>  * 
>  Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains 
>  the most water.
>
> Note: You may not slant the container and n is at least 2.
>
>  
>
>
>
> The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
>
>  
>
> Example:
>
> Input: [1,8,6,2,5,4,8,3,7]
> Output: 49
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
> public class ContainerWithMostWater {
> 	public static int maxArea(int[] height) {
>         int maxarea = 0, l = 0, r = height.length - 1;
>         while (l < r) {
>             maxarea = Math.max(maxarea, Math.min(height[l], height[r]) * (r - l));
>             if (height[l] < height[r])
>                 l++;
>             else
>                 r--;
>         }
>         return maxarea;
>     }
> 	
> 	 public static void main(String args[] ) throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 			String str = br.readLine();
> 			String[] numberline = str.split(" ");
> 			int[] heights = Arrays.asList(numberline).stream().mapToInt(Integer::parseInt).toArray();
>
> 			System.out.println(maxArea(heights));   
> 			
> 			}
>
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elie%20Day%2025%20Solutions/ContainerWithMostWater.java) · CODING RESOURCES/ELITE FS COMPLETE/Elie Day 25 Solutions/ContainerWithMostWater.java
