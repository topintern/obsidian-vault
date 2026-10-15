---
kind: "coding-problem"
title: "Triplet Sum (Day 41)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 41 Solutions/TripletSum.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Triplet Sum (Day 41)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given an array and a value, find if there is a triplet in array whose sum is equal to the given value. If there is such a triplet present in array, then print the triplet and return true. Else return false. 
 
 
 For example, 
 
Input: 12 3 4 1 6 9
24
 
output:12 1 9

Input: 17 5 21 12 3 4 11 26 9
57
 
output:-1
 
 
-----------------------------------------------------

case =1 
input =32 3 4 1 6 19
52
output =[1, 19, 32]

case =2 
input =8 75 61 17 5 21 12 3 4 11 26 9
58
output =[11, 21, 26]

case =3 
input =10 20 15 30 40 50 60 70 80 90
60
output =[10, 20, 30]

case =4
input =5 10 20 12 40 25 15
30
output =[5, 10, 15]


case =5
input =7 14 22 35 42 50 56 1 83 
84
output =[7, 35, 42]

case =6
input =17 5 21 12 3 4 11 26 9
57
output =-1

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · TripletSum.java
> ```java
> /*
>  * 
>  Given an array and a value, find if there is a triplet in array whose sum is equal to the given value. If there is such a triplet present in array, then print the triplet and return true. Else return false. 
>  
>  
>  For example, 
>  
> Input: 12 3 4 1 6 9
> 24
>  
> output:12 1 9
>
> Input: 17 5 21 12 3 4 11 26 9
> 57
>  
> output:-1
>  
>  
> -----------------------------------------------------
>
> case =1 
> input =32 3 4 1 6 19
> 52
> output =[1, 19, 32]
>
> case =2 
> input =8 75 61 17 5 21 12 3 4 11 26 9
> 58
> output =[11, 21, 26]
>
> case =3 
> input =10 20 15 30 40 50 60 70 80 90
> 60
> output =[10, 20, 30]
>
> case =4
> input =5 10 20 12 40 25 15
> 30
> output =[5, 10, 15]
>
>
> case =5
> input =7 14 22 35 42 50 56 1 83 
> 84
> output =[7, 35, 42]
>
> case =6
> input =17 5 21 12 3 4 11 26 9
> 57
> output =-1
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
> import java.util.HashSet;
>
> public class TripletSum {
>
> 	
> 	
>     static void findTriplet(int A[], 
>                                 int arr_size, int sum) 
>     { 
>         for (int i = 0; i < arr_size - 2; i++) { 
>   
>             
>             HashSet<Integer> s = new HashSet<Integer>(); 
>             int curr_sum = sum - A[i]; 
>             for (int j = i + 1; j < arr_size; j++) { 
>                 if (s.contains(curr_sum - A[j]) && curr_sum - A[j] != (int)s.toArray()[s.size() - 1]) { 
>                     System.out.println(A[i]+" "+A[j]+" "+(curr_sum - A[j])); 
>                     System.exit(0);
>                 } 
>                 s.add(A[j]); 
>             } 
>         } 
>         System.out.println("-1"); 
>  
>     } 
>   
>     public static void main(String args[] ) throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		
> 		String[] numline = str.split(" ");
> 		int[] nums = Arrays.asList(numline).stream().mapToInt(Integer::parseInt).toArray();
> 		int k=Integer.parseInt( br.readLine());
> 		findTriplet(nums,nums.length,k);   
> 		
> 		}
>     
>     
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2041%20Solutions/TripletSum.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 41 Solutions/TripletSum.java
