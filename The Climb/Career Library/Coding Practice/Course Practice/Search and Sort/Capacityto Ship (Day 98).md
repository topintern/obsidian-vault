---
kind: "coding-problem"
title: "Capacityto Ship (Day 98)"
collection: "Course Practice"
topic: "Search and Sort"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 98 Solutions/CapacitytoShip.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Capacityto Ship (Day 98)

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

> [!example]- Reference 1 · CapacitytoShip.txt
> ```java
> import java.util.Scanner;
> class CapacitytoShip {
>     public static int shipWithinDays(int[] weights, int D) {
>         int left = 0, right = 0;
>         for (int w: weights) {
>             left = Math.max(left, w);
>             right += w;
>         }
>         while (left < right) {
>             int mid = (left + right) / 2, need = 1, cur = 0;
>             for (int w: weights) {
>                 if (cur + w > mid) {
>                     need += 1;
>                     cur = 0;
>                 }
>                 cur += w;
>             }
>             if (need > D) left = mid + 1;
>             else right = mid;
>         }
>         return left;
>     }
> 	
> 	public static void main(String args[])
>     {
>         Scanner sc=new Scanner(System.in);
>         int n=sc.nextInt();
> 		int d=sc.nextInt();
>         int[] arr=new int[n];
>         for(int i=0;i<n;i++)
>             arr[i]=sc.nextInt();
>         System.out.println(shipWithinDays(arr,d));
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2098%20Solutions/CapacitytoShip.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 98 Solutions/CapacitytoShip.txt
