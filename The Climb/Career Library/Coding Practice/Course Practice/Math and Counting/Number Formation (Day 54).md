---
kind: "coding-problem"
title: "Number Formation (Day 54)"
collection: "Course Practice"
topic: "Math and Counting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 54 Solutions/NumberFormation.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Number Formation (Day 54)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You are given an array A of N integers. Each integer is a single digit number in the range[0 9] . 
You are also given a number K. Now, 
you need to count how many subsequences of the array A exist such that they form a K digit valid number.

A subsequence of size K is called a valid number if there are no leading zeros in the number formed.

Notes:

    A subsequence of an array is not necessarily contiguous.
    Suppose the given array is 0 1 0 2, then if you choose subsequence to be 002, 
	then it is not a valid 3 digit number. 
    Also, it will not be considered as a single digit number. A valid 3 digit number in the array is 102. 
    

Input Fomat

The first line contains an integer N as input denoting the size of the array.
Next line contains N space separated integers that denote elements of the array.
Next line contains an integer K


### Output Format


In the output, you need to print the count of valid K digit numbers



### Sample Input 

5
1 1 0 1 0
3


### Sample Output :


9


### Explanation :


in the given sample following are the 9 possible subsequences that form a valid 3 digit number.

[1 2 3]=110
[1 2 4]=111
[1 2 5]=110
[1 3 4]=101
[1 3 5]=100
[1 4 5]=110
[2 3 4]=101
[2 3 5]=100
[2 4 5]=110

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · NumberFormation.java
> ```java
> /*
> You are given an array A of N integers. Each integer is a single digit number in the range[0 9] . 
> You are also given a number K. Now, 
> you need to count how many subsequences of the array A exist such that they form a K digit valid number.
>
> A subsequence of size K is called a valid number if there are no leading zeros in the number formed.
>
> Notes:
>
>     A subsequence of an array is not necessarily contiguous.
>     Suppose the given array is 0 1 0 2, then if you choose subsequence to be 002, 
> 	then it is not a valid 3 digit number. 
>     Also, it will not be considered as a single digit number. A valid 3 digit number in the array is 102. 
>     
>
> Input Fomat
>
> The first line contains an integer N as input denoting the size of the array.
> Next line contains N space separated integers that denote elements of the array.
> Next line contains an integer K
>
> Output Format
>
> In the output, you need to print the count of valid K digit numbers
>
>
> Sample Input :
> 5
> 1 1 0 1 0
> 3
>
> Sample Output :
>
> 9
>
> Explanation :
>
> in the given sample following are the 9 possible subsequences that form a valid 3 digit number.
>
> [1 2 3]=110
> [1 2 4]=111
> [1 2 5]=110
> [1 3 4]=101
> [1 3 5]=100
> [1 4 5]=110
> [2 3 4]=101
> [2 3 5]=100
> [2 4 5]=110
>
>
> */
>
> import java.io.*;
>
> class NumberFormation {
> 	static int count = 0;
> 	public static boolean checkValid(int[] arr) {
> 		return arr[0] != 0;
> 	}
> 	public static void seq(int from, int depth, int l, int[] arr, int[] seq) {
>
> 		for (int i = from; i < arr.length; i++) {
> 			seq[depth] = arr[i];
> 			if (depth == seq.length - 1) {
> 				if (checkValid(seq))
> 					count++;
> 			} else {
> 				seq(i + 1, depth + 1, 0, arr, seq);
> 			}
> 		}
> 	}
>
> 	public static void main(String args[]) throws Exception {
> 		BufferedReader inp = new BufferedReader(new InputStreamReader(System.in));
> 		int T = Integer.parseInt(inp.readLine());
> 		String[] arrStr = inp.readLine().split(" ");
> 		int[] arr = new int[arrStr.length];
> 		int[] seq = new int[Integer.parseInt(inp.readLine())];
> 		for (int i = 0; i < arr.length; i++) {
> 			arr[i] = Integer.parseInt(arrStr[i]);
> 		}
> 		seq(0, 0, 0, arr, seq);
> 		System.out.println(count);
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2054%20Solutions/NumberFormation.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 54 Solutions/NumberFormation.java
