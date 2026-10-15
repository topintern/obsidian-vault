---
kind: "coding-problem"
title: "Dayofthe Year (Day 45)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 45 Solutions/DayoftheYear.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Dayofthe Year (Day 45)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a string date representing a Gregorian calendar date formatted as YYYY-MM-DD, 
return the day number of the year.

Example 1:
Input: date = "2019-01-09"
Output: 9
Explanation: Given date is the 9th day of the year in 2019.

Example 2:
Input: date = "2019-02-10"
Output: 41

Example 3:
Input: date = "2003-03-01"
Output: 60

Example 4:
Input: date = "2004-03-01"
Output: 61

Note: If the given date is invalid. print -1.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · DayoftheYear.java
> ```java
> /*
>  * 
> Given a string date representing a Gregorian calendar date formatted as YYYY-MM-DD, 
> return the day number of the year.
>
> Example 1:
> Input: date = "2019-01-09"
> Output: 9
> Explanation: Given date is the 9th day of the year in 2019.
>
> Example 2:
> Input: date = "2019-02-10"
> Output: 41
>
> Example 3:
> Input: date = "2003-03-01"
> Output: 60
>
> Example 4:
> Input: date = "2004-03-01"
> Output: 61
>
> Note: If the given date is invalid. print -1.
>
>  */
>
> import java.util.Scanner;
>
> public class DayoftheYear {
>
> 	 public static int dayOfYear(String date) {
> 		
> 	        int y=Integer.parseInt(date.substring(0, 4));
> 	        int m=Integer.parseInt(date.substring(5, 7));
> 	        int res=Integer.parseInt(date.substring(8));
> 	        
> 	        if(y%4==0&&y%100!=0&&m>2&&res!=29) res++;
> 	        
> 	        int[] days={31,28,31,30,31,30,31,31,30,31,30,31};
> 	        
> 	        for(int i=0;i<m-1;i++) res+=days[i];
> 	        return res;
> 	    }
> 	 public static void main(String args[] ) 
> 	 {
> 		Scanner scan = new Scanner(System.in);
> 		String str=scan.next();
> 		System.out.println(dayOfYear(str));
> 	}
> 	
> 	static boolean isLeap(int year) 
> 	{ 
> 		return (((year % 4 == 0) && 
> 				(year % 100 != 0)) || 
> 				(year % 400 == 0)); 
> 	} 
>
> 	static boolean isValidDate(int d, int m, int y) 
> 	{ 
> 		if (m < 1 || m > 12) 
> 			return false; 
> 		if (d < 1 || d > 31) 
> 			return false; 
>
> 		if (m == 2) 
> 		{ 
> 			if (isLeap(y)) 
> 				return (d <= 29); 
> 			else
> 				return (d <= 28); 
> 		} 
>
> 		if (m == 4 || m == 6 || 
> 			m == 9 || m == 11) 
> 			return (d <= 30); 
>
> 		return true; 
> 	} 
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2045%20Solutions/DayoftheYear.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 45 Solutions/DayoftheYear.java
