---
kind: "coding-problem"
title: "Next Nearest Time (Day 5)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 5 Solutions/NextNearestTime.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Next Nearest Time (Day 5)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a String, represents the time in the format "HH:MM" which is 24 hours format, form the next nearest time by reusing the digits in the given string. 
 There is no limit on how many times a digit can be reused.

You may assume the given input string is always valid. 
For example, 01:34, 12:09 are all valid. 1:34, 12:9 are all invalid.

Example 1:
	Input= 12:35
	Output= 12:51
Explanation: The next nearest time choosing from digits 1, 2, 3, 5, is 12:51, which occurs 16 minutes later.  
It is not 12:32, because this occurs 23 hours and 57 minutes later.

Example 2:
	Input= 16:56
	Output= 11:11
Explanation: The next nearest time choosing from digits 1, 6, 5, 6 is 11:11. 
It may be assumed that the returned time is next day's time since it is smaller than the input time numerically.
Accepted

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · NextNearestTime.java
> ```java
> /*
>  Given a String, represents the time in the format "HH:MM" which is 24 hours format, form the next nearest time by reusing the digits in the given string. 
>  There is no limit on how many times a digit can be reused.
>
> You may assume the given input string is always valid. 
> For example, 01:34, 12:09 are all valid. 1:34, 12:9 are all invalid.
>
> Example 1:
> 	Input= 12:35
> 	Output= 12:51
> Explanation: The next nearest time choosing from digits 1, 2, 3, 5, is 12:51, which occurs 16 minutes later.  
> It is not 12:32, because this occurs 23 hours and 57 minutes later.
>
> Example 2:
> 	Input= 16:56
> 	Output= 11:11
> Explanation: The next nearest time choosing from digits 1, 6, 5, 6 is 11:11. 
> It may be assumed that the returned time is next day's time since it is smaller than the input time numerically.
> Accepted
>
>  */
>
> import java.util.*;
>
> public class NextNearestTime {
> 	
>     static String nextNearestTime(String time) {
>         int cur = 60 * Integer.parseInt(time.substring(0, 2));
>         cur += Integer.parseInt(time.substring(3));
>         Set<Integer> allowed = new HashSet();
>         for (char c: time.toCharArray()) if (c != ':') {
>             allowed.add(c - '0');
>         }
>
>         while (true) {
>             cur = (cur + 1) % (24 * 60);
>             int[] digits = new int[]{cur / 60 / 10, cur / 60 % 10, cur % 60 / 10, cur % 60 % 10};
>             search : {
>                 for (int d: digits) if (!allowed.contains(d)) break search;
>                 return String.format("%02d:%02d", cur / 60, cur % 60);
>             }
>         }
>     }
>
> public static void main(String args[] ) {
> 		 Scanner sc = new Scanner(System.in);
> 			String str=sc.next();
> 		    System.out.println(nextNearestTime(str));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%205%20Solutions/NextNearestTime.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 5 Solutions/NextNearestTime.java
