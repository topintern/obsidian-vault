---
kind: "coding-problem"
title: "Timeintervalsgreedy (Day 3)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 3 Solutions/timeintervalsgreedy.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Timeintervalsgreedy (Day 3)

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

> [!example]- Reference 1 · timeintervalsgreedy.java
> ```java
> import java.util.*;
> import java.io.*;
> class timeintervalsgreedy{
> 	public static void main(String args[])
> 	{
>         Scanner sc=new Scanner(System.in);
>         int n;
>         n=sc.nextInt();
>         int time[][]=new int[n][2];
>         for(int i=0;i<n;i++)
>         {
>             time[i][0]=sc.nextInt();
>             time[i][1]=sc.nextInt();
>         }
>         Arrays.sort(time,(a,b)->{return a[0]-b[0];});
>         int c=1;
>         PriorityQueue<Integer> p=new PriorityQueue<Integer>();
>         for(int i=0;i<n;i++)
>         {
>             if(!p.isEmpty())
>             {
>               int prev_end=p.peek();
>               if(time[i][0]>=prev_end)
>                 p.poll();
>             
>             else
>             {
>                 c++;
>             }
>         }
>         p.add(time[i][1]);
>         }
>         System.out.println(c);
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%203%20Solutions/timeintervalsgreedy.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 3 Solutions/timeintervalsgreedy.java
