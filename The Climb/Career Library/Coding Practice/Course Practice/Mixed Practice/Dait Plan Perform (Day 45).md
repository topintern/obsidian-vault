---
kind: "coding-problem"
title: "Dait Plan Perform (Day 45)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 45 Solutions/DaitPlanPerform.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Dait Plan Perform (Day 45)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

A dieter consumes calories[i] calories on the i-th day. 

Given an integer k, for every consecutive sequence of k days (calories[i], calories[i+1], ..., calories[i+k-1] for all 0 <= i <= n-k), 
they look at T, the total calories consumed during that sequence of k days (calories[i] + calories[i+1] + ... + calories[i+k-1]):

If T < lower, they performed poorly on their diet and lose 1 point; 
If T > upper, they performed well on their diet and gain 1 point;
Otherwise, they performed normally and there is no change in points.
Initially, the dieter has zero points. Return the total number of points the dieter has after dieting for calories.length days.

Note that the total points can be negative.

Example 1:
	Input: 	1 2 3 4 5			// Calories as line input.
				1 3 3				// indiactes k, lower, upper values.
	Output: 0
	Explanation: 
						Since k = 1, we consider each element of the array separately and compare it to lower and upper.
						calories[0] and calories[1] are less than lower so 2 points are lost.
						calories[3] and calories[4] are greater than upper so 2 points are gained.

Example 2:
	Input: 	3 2
				2 0 1
	Output: 1
	Explanation: 	
						Since k = 2, we consider subarrays of length 2.
						calories[0] + calories[1] > upper so 1 point is gained.

Example 3:
	Input: 	6 5 0 0
				2 1 5
	Output: 0
	Explanation:
					calories[0] + calories[1] > upper so 1 point is gained.
					lower <= calories[1] + calories[2] <= upper so no change in points.
					calories[2] + calories[3] < lower so 1 point is lost.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · DaitPlanPerform.java
> ```java
> /*
>  * 
>  A dieter consumes calories[i] calories on the i-th day. 
>
> Given an integer k, for every consecutive sequence of k days (calories[i], calories[i+1], ..., calories[i+k-1] for all 0 <= i <= n-k), 
> they look at T, the total calories consumed during that sequence of k days (calories[i] + calories[i+1] + ... + calories[i+k-1]):
>
> If T < lower, they performed poorly on their diet and lose 1 point; 
> If T > upper, they performed well on their diet and gain 1 point;
> Otherwise, they performed normally and there is no change in points.
> Initially, the dieter has zero points. Return the total number of points the dieter has after dieting for calories.length days.
>
> Note that the total points can be negative.
>
> Example 1:
> 	Input: 	1 2 3 4 5			// Calories as line input.
> 				1 3 3				// indiactes k, lower, upper values.
> 	Output: 0
> 	Explanation: 
> 						Since k = 1, we consider each element of the array separately and compare it to lower and upper.
> 						calories[0] and calories[1] are less than lower so 2 points are lost.
> 						calories[3] and calories[4] are greater than upper so 2 points are gained.
>
> Example 2:
> 	Input: 	3 2
> 				2 0 1
> 	Output: 1
> 	Explanation: 	
> 						Since k = 2, we consider subarrays of length 2.
> 						calories[0] + calories[1] > upper so 1 point is gained.
>
> Example 3:
> 	Input: 	6 5 0 0
> 				2 1 5
> 	Output: 0
> 	Explanation:
> 					calories[0] + calories[1] > upper so 1 point is gained.
> 					lower <= calories[1] + calories[2] <= upper so no change in points.
> 					calories[2] + calories[3] < lower so 1 point is lost.
>  
>
>  */
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class DaitPlanPerform {
>
> 	public static int dietPlanPerformance(int[] calories, int k, int lower, int upper) {
>         int point = 0;
>         for (int i = 0, win = 0; i < calories.length; ++i) {
>             win += calories[i];
>             if (i >= k - 1) {           					// reach a k sequence already.
>                 if (i > k - 1) { win -= calories[i - k]; }  // more than k sequence already
>                 if (win < lower) { --point ; }
>                 else if (win > upper) { ++point; }
>             }
>         }
>         return point;
>     }
> 	
> 	 public static void main(String args[] ) throws IOException {
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 			String str = br.readLine();
> 			String[] numbers = str.split(" ");
> 			int[] nums = Arrays.asList(numbers).stream().mapToInt(Integer::parseInt).toArray();
> 			int k=Integer.parseInt(br.readLine());
> 			int lower=Integer.parseInt(br.readLine());
> 			int upper=Integer.parseInt(br.readLine());
> 			System.out.println(dietPlanPerformance(nums,k,lower,upper));
> 	}
> 	 
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2045%20Solutions/DaitPlanPerform.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 45 Solutions/DaitPlanPerform.java
