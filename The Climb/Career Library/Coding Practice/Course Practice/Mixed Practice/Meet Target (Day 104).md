---
kind: "coding-problem"
title: "Meet Target (Day 104)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 104 Solutions/MeetTarget.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Meet Target (Day 104)

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

> [!example]- Reference 1 · MeetTarget.java
> ```java
> import java.util.*;
>
> class MeetTarget {
>     public static String minimizeError(String[] prices, int target) {
>         float res = 0;
>         PriorityQueue<Double> diffHeap = new PriorityQueue<>();        
>         for (String s : prices) {
>             float f = Float.valueOf(s);
>             double low = Math.floor(f);
>             double high = Math.ceil(f);
>             
>             if (low != high)
>                 diffHeap.offer((high-f)-(f-low));
>             res += f-low;
>             target -= low;
>         }
>         
>         if (target < 0 || target > diffHeap.size())
>             return "-1";
>         while (target-- > 0)
>             res += diffHeap.poll();
>         
> 		return String.format("%.3f", res);
>     }
> 	public static void main(String args[])
> 	{
> 		Scanner sc = new Scanner(System.in);
> 		String[] prices=sc.nextLine().split(" ");
> 		int t=sc.nextInt();
> 		System.out.println(minimizeError(prices,t));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20104%20Solutions/MeetTarget.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 104 Solutions/MeetTarget.java
