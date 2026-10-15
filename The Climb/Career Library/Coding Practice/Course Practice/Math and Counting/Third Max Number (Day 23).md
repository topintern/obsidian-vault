---
kind: "coding-problem"
title: "Third Max Number (Day 23)"
collection: "Course Practice"
topic: "Math and Counting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/ELITE DAY 23 SOLUTIONS/ThirdMaxNumber.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Third Max Number (Day 23)

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

> [!example]- Reference 1 · ThirdMaxNumber.java
> ```java
> import java.util.*;
> class ThirdMaxNumber {
>
>     static int thirdMax(int[] nums) {
>         Integer max1 = null;
>         Integer max2 = null;
>         Integer max3 = null;
>         for (Integer n : nums) {
>             if (n.equals(max1) || n.equals(max2) || n.equals(max3)) continue;
>             if (max1 == null || n > max1) {
>                 max3 = max2;
>                 max2 = max1;
>                 max1 = n;
>             } else if (max2 == null || n > max2) {
>                 max3 = max2;
>                 max2 = n;
>             } else if (max3 == null || n > max3) {
>                 max3 = n;
>             }
>         }
>         return max3 == null ? max1 : max3;
>     }
>     public static void main(String args[])
>     {
> 	Scanner sc=new Scanner(System.in);
> 	String[] str=sc.nextLine().split(" ");
> 	int arr[]=new int[str.length];
> 	int i=0;
> 	for(String s:str){
> 	    arr[i]=Integer.parseInt(s);
> 	    i++;
> 	}
> 	System.out.print(thirdMax(arr));
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/ELITE%20DAY%2023%20SOLUTIONS/ThirdMaxNumber.java) · CODING RESOURCES/ELITE FS COMPLETE/ELITE DAY 23 SOLUTIONS/ThirdMaxNumber.java
