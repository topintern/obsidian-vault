---
kind: "coding-problem"
title: "House Robber2 (Day 96)"
collection: "Course Practice"
topic: "Dynamic Programming"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 96 Solutions/HouseRobber2.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# House Robber2 (Day 96)

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

> [!example]- Reference 1 · HouseRobber2.java
> ```java
> import java.util.Scanner;
>
> class HouseRobber2 {
>    private static int rober(int[] num, int lo, int hi) {
>     int include = 0, exclude = 0;
>     for (int j = lo; j <= hi; j++) {
>         int i = include, e = exclude;
>         include = e + num[j];
>         exclude = Math.max(e, i);
>     }
>     return Math.max(include, exclude);
>     }
>     
>     public static int rob(int[] nums) {
>     if (nums.length == 1) return nums[0];
>     return Math.max(rober(nums, 0, nums.length - 2), rober(nums, 1, nums.length - 1));
>     }
>     public static void main(String args[])
>     {
>         Scanner sc=new Scanner(System.in);
>         int n=sc.nextInt();
>         int[] arr=new int[n];
>         for(int i=0;i<n;i++)
>             arr[i]=sc.nextInt();
>         System.out.println(rob(arr));
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2096%20Solutions/HouseRobber2.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 96 Solutions/HouseRobber2.java
