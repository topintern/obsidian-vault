---
kind: "coding-problem"
title: "One Plus (Day 27)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 27 Solutions/OnePlus.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# One Plus (Day 27)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a non-empty array of digits representing a non-negative integer, plus one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.

Time Complexity: O(n)

Example 1:

Input: [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
Example 2:

Input: [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.

========TestCases=============

case =1
input =9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9
output =[1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]

case =2
input =7 8 9 0 9
output =[7, 8, 9, 1, 0]

case =3
input =9 9 9 9 9
output =[1, 0, 0, 0, 0, 0]

case =4
input =9 8 7 6 5 4 3 2 9
output =[9, 8, 7, 6, 5, 4, 3, 3, 0]

case =5
input =6 5 4 7 9 8 7 9 7 9
output =[6, 5, 4, 7, 9, 8, 7, 9, 8, 0]


case =6
input =9 8 9 9 9 9
output =[9, 9, 0, 0, 0, 0]

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · OnePlus.java
> ```java
> /*
>  * 
>  Given a non-empty array of digits representing a non-negative integer, plus one to the integer.
>
> The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.
>
> You may assume the integer does not contain any leading zero, except the number 0 itself.
>
> Time Complexity: O(n)
>
> Example 1:
>
> Input: [1,2,3]
> Output: [1,2,4]
> Explanation: The array represents the integer 123.
> Example 2:
>
> Input: [4,3,2,1]
> Output: [4,3,2,2]
> Explanation: The array represents the integer 4321.
>
> ========TestCases=============
>
> case =1
> input =9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9 9
> output =[1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
>
> case =2
> input =7 8 9 0 9
> output =[7, 8, 9, 1, 0]
>
> case =3
> input =9 9 9 9 9
> output =[1, 0, 0, 0, 0, 0]
>
> case =4
> input =9 8 7 6 5 4 3 2 9
> output =[9, 8, 7, 6, 5, 4, 3, 3, 0]
>
> case =5
> input =6 5 4 7 9 8 7 9 7 9
> output =[6, 5, 4, 7, 9, 8, 7, 9, 8, 0]
>
>
> case =6
> input =9 8 9 9 9 9
> output =[9, 9, 0, 0, 0, 0]
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
> public class OnePlus {
>
> 	public static int[] plusOne(int[] digits) {
>         
> 	    int n = digits.length;
> 	    for(int i=n-1; i>=0; i--) {
> 	        if(digits[i] < 9) {
> 	            digits[i]++;
> 	            return digits;
> 	        }
> 	        
> 	        digits[i] = 0;
> 	    }
> 	    
> 	    int[] newNumber = new int [n+1];
> 	    newNumber[0] = 1;
> 	    
> 	    return newNumber;
> 	}
> 	
> 	 public static void main(String args[] ) throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 			String str = br.readLine();
> 			String[] numbers = str.split(" ");
> 			int[] arr = Arrays.asList(numbers).stream().mapToInt(Integer::parseInt).toArray();
> 			System.out.println(Arrays.toString(plusOne(arr)));
> 			}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2027%20Solutions/OnePlus.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 27 Solutions/OnePlus.java
