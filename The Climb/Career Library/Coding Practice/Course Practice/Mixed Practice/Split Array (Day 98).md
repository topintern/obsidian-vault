---
kind: "coding-problem"
title: "Split Array (Day 98)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 98 Solutions/SplitArray.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Split Array (Day 98)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Problem

The source has reference code without a separate problem statement. Establish its inputs, expected outputs, and constraints before practising.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SplitArray.java
> ```java
> import java.util.Scanner;
> import java.util.HashSet;
>
> public class SplitArray {
>     public static boolean splitArray(int[] nums) {
>         if (nums.length < 7)
>             return false;
>         int[] sum = new int[nums.length];
>         sum[0] = nums[0];
>         for (int i = 1; i < nums.length; i++) {
>             sum[i] = sum[i - 1] + nums[i];
>         }
>         for (int j = 3; j < nums.length - 3; j++) {
>             HashSet<Integer> set = new HashSet<>();
>             for (int i = 1; i < j - 1; i++) {
>                 if (sum[i - 1] == sum[j - 1] - sum[i])
>                     set.add(sum[i - 1]);
>             }
>             for (int k = j + 2; k < nums.length - 1; k++) {
>                 if (sum[nums.length - 1] - sum[k] == sum[k - 1] - sum[j] && set.contains(sum[k - 1] - sum[j]))
>                     return true;
>             }
>         }
>         return false;
>     }
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		int n=sc.nextInt();
> 		int[] nums=new int[n];
> 		for(int i=0;i<n;i++)
> 		{
> 			nums[i]=sc.nextInt();
> 		}
> 		System.out.println(splitArray(nums));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2098%20Solutions/SplitArray.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 98 Solutions/SplitArray.java
