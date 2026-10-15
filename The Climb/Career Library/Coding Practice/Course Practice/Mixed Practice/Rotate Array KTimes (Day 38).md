---
kind: "coding-problem"
title: "Rotate Array KTimes (Day 38)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 38 Solutions/RotateArrayKTimes.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Rotate Array KTimes (Day 38)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Rotate an array (of size n) k times left
 
 input : 1 2 3 4 5 6 7
 2
 output: 3 4 5 6 7 1 2
 
 Time complexity : O(n)

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · RotateArrayKTimes.txt
> ```java
> /*
>  * 
>  Rotate an array (of size n) k times left
>  
>  input : 1 2 3 4 5 6 7
>  2
>  output: 3 4 5 6 7 1 2
>  
>  Time complexity : O(n)
>
>
>  */
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class RotateArrayKTimes {
>
> 	/*Function to left rotate arr[] of siz n by d*/
> 	static void  leftRotate(int arr[], int d, int n) 
>     { 
>         int i, j, k, temp; 
>         int g_c_d = gcd(d, n); 
>         for (i = 0; i < g_c_d; i++) { 
>             /* move i-th values of blocks */
>             temp = arr[i]; 
>             j = i; 
>             while (true) { 
>                 k = j + d; 
>                 if (k >= n) 
>                     k = k - n; 
>                 if (k == i) 
>                     break; 
>                 arr[j] = arr[k]; 
>                 j = k; 
>             } 
>             arr[j] = temp; 
>         } 
>     } 
>   
>     /*UTILITY FUNCTIONS*/
>   
>     /* function to print an array */
>     static void  printArray(int arr[], int size) 
>     { 
>         int i; 
>         for (i = 0; i < size; i++) 
>             System.out.print(arr[i] + " "); 
>     } 
>   
>     /*Fuction to get gcd of a and b*/
>     static int gcd(int a, int b) 
>     { 
>         if (b == 0) 
>             return a; 
>         else
>             return gcd(b, a % b); 
>     } 
>   
>     // Driver program to test above functions 
>     public static void main(String[] args)  throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		int k=Integer.parseInt(br.readLine());
> 		String[] numbers = str.split(" ");
> 		int[] arr = Arrays.asList(numbers).stream().mapToInt(Integer::parseInt).toArray();
>         leftRotate(arr, k, arr.length); 
>         printArray(arr, arr.length); 
>     } 
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2038%20Solutions/RotateArrayKTimes.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 38 Solutions/RotateArrayKTimes.txt
