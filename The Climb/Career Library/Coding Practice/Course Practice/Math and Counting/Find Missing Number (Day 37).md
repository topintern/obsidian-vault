---
kind: "coding-problem"
title: "Find Missing Number (Day 37)"
collection: "Course Practice"
topic: "Math and Counting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 37 Solutions/FindMissingNumber.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Find Missing Number (Day 37)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You are given a list of n-1 integers and these integers are in the range of 1 to n. There are no duplicates in the list. One of the integers is missing in the list. Write an efficient code to find the missing integer.

Example :

Input:1 2 4 6 3 7 8
Output: 5

Time Complexity :O(n)



==================================
Approach # 1

1. Get the sum of numbers which is total = n*(n+1)/2
2. Subtract all the numbers from sum and
   you will get the missing number


Approach # 2

1) XOR all the array elements, let the result of XOR be X1.
  2) XOR all numbers from 1 to n, let XOR be X2.
  3) XOR of X1 and X2 gives the missing number.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · FindMissingNumber.txt
> ```java
> /*
>  * 
>  You are given a list of n-1 integers and these integers are in the range of 1 to n. There are no duplicates in the list. One of the integers is missing in the list. Write an efficient code to find the missing integer.
>
> Example :
>
> Input:1 2 4 6 3 7 8
> Output: 5
>
> Time Complexity :O(n)
>
>
>
> ==================================
> Approach # 1
>
> 1. Get the sum of numbers which is total = n*(n+1)/2
> 2. Subtract all the numbers from sum and
>    you will get the missing number
>
>
> Approach # 2
>
> 1) XOR all the array elements, let the result of XOR be X1.
>   2) XOR all numbers from 1 to n, let XOR be X2.
>   3) XOR of X1 and X2 gives the missing number.
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
> public class FindMissingNumber {
> 	
> 	
> 	//Approach # 1
> 	/*static int getMissingNo(int a[], int n) 
>     { 
>         int i, total; 
>         total = (n + 1) * (n + 2) / 2; 
>         for (i = 0; i < n; i++) 
>             total -= a[i]; 
>         return total; 
>     } */
> 	
> 	
> 	//Approach # 2
> 	
> 	static int getMissingNo(int a[], int n) 
>     { 
>         int x1 = a[0]; 
>         int x2 = 1; 
>   
>         /* For xor of all the elements  
>            in array */
>         for (int i = 1; i < n; i++) 
>             x1 = x1 ^ a[i]; 
>   
>         /* For xor of all the elements  
>            from 1 to n+1 */
>         for (int i = 2; i <= n + 1; i++) 
>             x2 = x2 ^ i; 
>   
>         return (x1 ^ x2); 
>     } 
>     
>     
> 	
>     
>   
>     public static void main(String args[]) throws IOException
>     { 
>     	 BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>  		String str = br.readLine();
>  		
>  		String[] numline = str.split(" ");
>  		int[] a = Arrays.asList(numline).stream().mapToInt(Integer::parseInt).toArray();
>      
>         int miss = getMissingNo(a, a.length); 
>         System.out.println(miss); 
>     } 
>     
>
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2037%20Solutions/FindMissingNumber.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 37 Solutions/FindMissingNumber.txt
