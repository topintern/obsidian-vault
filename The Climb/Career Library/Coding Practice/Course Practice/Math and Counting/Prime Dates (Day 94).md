---
kind: "coding-problem"
title: "Prime Dates (Day 94)"
collection: "Course Practice"
topic: "Math and Counting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 94 Solutions/PrimeDates.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Prime Dates (Day 94)

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

> [!example]- Reference 1 · PrimeDates.txt
> ```java
> import java.util.*;
> import java.lang.*;
> import java.io.*;
> import java.math.*;
>
> public class Main {
>     
>     public static int month[];
>     
>     public static void main (String[] args) throws java.lang.Exception {
>         Scanner in  = new Scanner(System.in);
>
>         month = new int[15];
>
>         String s = in.nextLine();
>
>         StringTokenizer str = new StringTokenizer(s, "- ");
>
>         int d1 = Integer.parseInt(str.nextToken());
>         int m1 = Integer.parseInt(str.nextToken());
>         int y1 = Integer.parseInt(str.nextToken());
>         int d2 = Integer.parseInt(str.nextToken());
>         int m2 = Integer.parseInt(str.nextToken());
>         int y2 = Integer.parseInt(str.nextToken());
>       
>         int result = findPrimeDates(d1, m1, y1, d2, m2, y2);
>         System.out.println(result);
>    }
>
>     public static void updateLeapYear(int year) {
>         if(year % 400 == 0) {
>             month[2] = 29;	//change -1 org: month[2] = 28;
>         } else if(year % 100 == 0) {
>             month[2] = 28;	//change -2	org: month[2] = 29;
>         } else if(year % 4 == 0) {
>             month[2] = 29;
>         } else {
>             month[2] = 28;
>         }
>     }
>     
>     public static void storeMonth() {
>         month[1] = 31;
>         month[2] = 28;
>         month[3] = 31;
>         month[4] = 30;
>         month[5] = 31;
>         month[6] = 30;
>         month[7] = 31;
>         month[8] = 31;
>         month[9] = 30;
>         month[10] = 31;
>         month[11] = 30;
>         month[12] = 31;
>     }
>    
>    public static int findPrimeDates(int d1, int m1, int y1, int d2, int m2, int y2) {
>         storeMonth();
>     
>         int result = 0;
>     
>         while(true) {
>             int x = d1;
>             x = x * 100 + m1;
>             x = x * 10000 + y1;	//change -3 org: x = x * 1000 + y1; 
>             if(x % 4 == 0 || x % 7 == 0) {	//change -4	org: if(x % 4 == 0 && x % 7 == 0)
>                 result = result + 1;
>             }
>             if(d1 == d2 && m1 == m2 && y1 == y2) {
>                 break;
>             }
>             updateLeapYear(y1);
>             d1 = d1 + 1;
>             if(d1 > month[m1]) {
>                 m1 = m1 + 1;
>                 d1 = 1;
>                 if(m1 > 12) {
>                     y1 =  y1 + 1;
>                     m1 =  1;		//change -5 org: m1 =  m1 + 1;
>                 }
>             }
>         }
>         return result;
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2094%20Solutions/PrimeDates.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 94 Solutions/PrimeDates.txt
