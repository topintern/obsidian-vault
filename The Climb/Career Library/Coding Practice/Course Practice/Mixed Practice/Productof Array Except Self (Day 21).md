---
kind: "coding-problem"
title: "Productof Array Except Self (Day 21)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 21 Solutions/ProductofArrayExceptSelf.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Productof Array Except Self (Day 21)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given an array nums of n integers where n > 1,  
return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

Example:
	Input:  1 2 3 4
	Output: 24 12 8 6

Note: Please solve it without division and in O(n).

------TestCases-------
case =1
input =2 6 8 10 16
output ='7680 2560 1920 1536 960'

case =2
input =-2 -1 0 1 2
output ='0 0 4 0 0'

case =3
input =2 9 3 8 4 7 5 6 1
output ='181440 40320 120960 45360 90720 51840 72576 60480 362880'

case =4
input =12 14 16 18 20
output ='80640 69120 60480 53760 48384'

case =5
input =23 34 -23 -34 5 -5
output ='-664700 -449650 664700 449650 -3057620 3057620'

case =6
input =10 8 6 4 1 2 3 5 7 9
output ='362880 453600 604800 907200 3628800 1814400 1209600 725760 518400 403200'

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ProductofArrayExceptSelf.java
> ```java
> /*
> Given an array nums of n integers where n > 1,  
> return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].
>
> Example:
> 	Input:  1 2 3 4
> 	Output: 24 12 8 6
>
> Note: Please solve it without division and in O(n).
>
> ------TestCases-------
> case =1
> input =2 6 8 10 16
> output ='7680 2560 1920 1536 960'
>
> case =2
> input =-2 -1 0 1 2
> output ='0 0 4 0 0'
>
> case =3
> input =2 9 3 8 4 7 5 6 1
> output ='181440 40320 120960 45360 90720 51840 72576 60480 362880'
>
> case =4
> input =12 14 16 18 20
> output ='80640 69120 60480 53760 48384'
>
> case =5
> input =23 34 -23 -34 5 -5
> output ='-664700 -449650 664700 449650 -3057620 3057620'
>
> case =6
> input =10 8 6 4 1 2 3 5 7 9
> output ='362880 453600 604800 907200 3628800 1814400 1209600 725760 518400 403200'
>
> */
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.*;
>
> class ProductofArrayExceptSelf
> {
> 	public static int[] productExceptSelf(int[] nums) {
>
>         // The length of the input array 
>         int length = nums.length;
>
>         // Final answer array to be returned
>         int[] answer = new int[length];
>
>         // answer[i] contains the product of all the elements to the left
>         // Note: for the element at index '0', there are no elements to the left,
>         // so the answer[0] would be 1
>         answer[0] = 1;
>         for (int i = 1; i < length; i++) {
>
>             // answer[i - 1] already contains the product of elements to the left of 'i - 1'
>             // Simply multiplying it with nums[i - 1] would give the product of all 
>             // elements to the left of index 'i'
>             answer[i] = nums[i - 1] * answer[i - 1];
>         }
>
>         // R contains the product of all the elements to the right
>         // Note: for the element at index 'length - 1', there are no elements to the right,
>         // so the R would be 1
>         int R = 1;
>         for (int i = length - 1; i >= 0; i--) {
>
>             // For the index 'i', R would contain the 
>             // product of all elements to the right. We update R accordingly
>             answer[i] = answer[i] * R;
>             R *= nums[i];
>         }
>
>         return answer;
>     }
> 	 public static void main(String args[] ) throws IOException {
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		String[] numberline = str.split(" ");
> 		int[] nums = Arrays.asList(numberline).stream().mapToInt(Integer::parseInt).toArray();
> 		for(int i:productExceptSelf(nums))
> 		System.out.print(i+" ");   
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2021%20Solutions/ProductofArrayExceptSelf.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 21 Solutions/ProductofArrayExceptSelf.java
