---
kind: "coding-problem"
title: "Sliding Window Max (Day 34)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 34 Solutions/SlidingWindowMax.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Sliding Window Max (Day 34)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given an array nums, there is a sliding window of size k 
which is moving from the very left of the array to the very right. 

You can only see the k numbers in the window. 
Each time the sliding window moves right by one position. 
Return the max sliding window.

Example:
    Input = 1 3 -1 -3 5 3 6 7
            3
    Output: 3 3 5 5 6 7 


### Explanation: 

    Window position                Max
    ---------------               -----
    [1  3  -1] -3  5  3  6  7      3
    1 [3  -1  -3] 5  3  6  7       3
    1  3 [-1  -3  5] 3  6  7       5
    1  3  -1 [-3  5  3] 6  7       5
    1  3  -1  -3 [5  3  6] 7       6
    1  3  -1  -3  5 [3  6  7]      7

Note:
    You may assume k is always valid, 1 ≤ k ≤ input array's size for non-empty array.

Follow up:
Could you solve it in linear time?

=========TestCases========
case =1 
input =76 2 4 23 5 67 4 89
3
output =76 23 23 67 67 89

case =2 
input =7 2 14 -23 55 6 42 8 23 46 82
4
output =[14, 55, 55, 55, 55, 42, 46, 82]

case =3 
input =71 2 14 123 55 6 62 38 23 46 82
5
output =[123, 123, 123, 123, 62, 62, 82]

case =4 
input =2 14 -23 55 6 42 8 23 46
6
output =[55, 55, 55, 55]

case =5
input =76 2 4 23 5 67 4 89 2 14 -23 55 6 42 8 23 46
6
output =[76, 67, 89, 89, 89, 89, 89, 89, 55, 55, 55, 55]

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SlidingWindowMax.java
> ```java
> /*
>
> Given an array nums, there is a sliding window of size k 
> which is moving from the very left of the array to the very right. 
>
> You can only see the k numbers in the window. 
> Each time the sliding window moves right by one position. 
> Return the max sliding window.
>
> Example:
>     Input = 1 3 -1 -3 5 3 6 7
>             3
>     Output: 3 3 5 5 6 7 
>
> Explanation: 
>     Window position                Max
>     ---------------               -----
>     [1  3  -1] -3  5  3  6  7      3
>     1 [3  -1  -3] 5  3  6  7       3
>     1  3 [-1  -3  5] 3  6  7       5
>     1  3  -1 [-3  5  3] 6  7       5
>     1  3  -1  -3 [5  3  6] 7       6
>     1  3  -1  -3  5 [3  6  7]      7
>
> Note:
>     You may assume k is always valid, 1 ≤ k ≤ input array's size for non-empty array.
>
> Follow up:
> Could you solve it in linear time?
>
> =========TestCases========
> case =1 
> input =76 2 4 23 5 67 4 89
> 3
> output =76 23 23 67 67 89
>
> case =2 
> input =7 2 14 -23 55 6 42 8 23 46 82
> 4
> output =[14, 55, 55, 55, 55, 42, 46, 82]
>
> case =3 
> input =71 2 14 123 55 6 62 38 23 46 82
> 5
> output =[123, 123, 123, 123, 62, 62, 82]
>
> case =4 
> input =2 14 -23 55 6 42 8 23 46
> 6
> output =[55, 55, 55, 55]
>
> case =5
> input =76 2 4 23 5 67 4 89 2 14 -23 55 6 42 8 23 46
> 6
> output =[76, 67, 89, 89, 89, 89, 89, 89, 55, 55, 55, 55]
>
>
> */
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class SlidingWindowMax {
>
> 	
> 	public static int[] maxSlidingWindow(int[] nums, int k) {
> 	    int n = nums.length;
> 	    if (n * k == 0) return new int[0];
> 	    if (k == 1) return nums;
>
> 	    int [] left = new int[n];
> 	    left[0] = nums[0];
> 	    int [] right = new int[n];
> 	    right[n - 1] = nums[n - 1];
> 	    for (int i = 1; i < n; i++) {
> 	      // from left to right
> 	      if (i % k == 0) left[i] = nums[i];  // block_start
> 	      else left[i] = Math.max(left[i - 1], nums[i]);
>
> 	      // from right to left
> 	      int j = n - i - 1;
> 	      if ((j + 1) % k == 0) right[j] = nums[j];  // block_end
> 	      else right[j] = Math.max(right[j + 1], nums[j]);
> 	    }
>
> 	    int [] output = new int[n - k + 1];
> 	    for (int i = 0; i < n - k + 1; i++)
> 	      output[i] = Math.max(left[i + k - 1], right[i]);
>
> 	    return output;
> 	  }
> 	
> 	public static void main(String args[] ) throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		
> 		String[] numline = str.split(" ");
> 		int[] nums = Arrays.asList(numline).stream().mapToInt(Integer::parseInt).toArray();
> 		int k=Integer.parseInt( br.readLine());
> 		System.out.println(Arrays.toString(maxSlidingWindow(nums,k)));   
> 		
> 		}
> 	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2034%20Solutions/SlidingWindowMax.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 34 Solutions/SlidingWindowMax.java
