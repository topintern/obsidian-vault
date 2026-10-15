---
kind: "coding-problem"
title: "Dayof Week (Day 45)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 45 Solutions/DayofWeek.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Dayof Week (Day 45)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a date, return the corresponding day of the week for that date.
The input is given as three integers representing the day, month and year respectively.
Return the answer as one of the following values {"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"}.

Example 1:
	Input: 31-08-2019
	Output: Saturday

Example 2:
	Input: 18-07-1999
	Output: Sunday

Example 3:
	Input: 15-08-1993
	Output: Sunday
 

Constraints:
If the given date is invalid. print -1.
Date should be in the range from 01-01-1901 to 31-12-2099, otherwise -2.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · DayofWeek.java
> ```java
> /*
>  * 
> Given a date, return the corresponding day of the week for that date.
> The input is given as three integers representing the day, month and year respectively.
> Return the answer as one of the following values {"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"}.
>
> Example 1:
> 	Input: 31-08-2019
> 	Output: Saturday
>
> Example 2:
> 	Input: 18-07-1999
> 	Output: Sunday
>
> Example 3:
> 	Input: 15-08-1993
> 	Output: Sunday
>  
>
> Constraints:
> If the given date is invalid. print -1.
> Date should be in the range from 01-01-1901 to 31-12-2099, otherwise -2.
>  */
>
> import java.util.Scanner;
>
> public class DayofWeek {
>
> 	
> 	int[] months = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
> 	// day staring from today
> 	String[] days = {"Friday", "Saturday", "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday"};
> 	public String dayOfTheWeek(int day, int month, int year) {
> 			int curr = daysFromStart(13, 03, 2020); // today's date
> 			int cnt = daysFromStart(day, month, year);
> 			return days[((cnt - curr) % 7 + 7) % 7];
> 	}
>
> 	private int daysFromStart(int day, int month, int year) {
> 			int sum = 0;
> 			for (int i = 1971; i < year; i++) {
> 					sum += 365;
> 					if (isLeapYear(i)) {
> 							sum++;
> 					}
> 			}
> 			for (int i = 1; i < month; i++) {
> 					sum += months[i - 1];
> 					if (i == 2 && isLeapYear(year)) {
> 							sum++;
> 					}
> 			}
> 			sum += day - 1;
> 			return sum;
> 	}
>
> 	private boolean isLeapYear(int year) {
> 			return (year % 4 == 0 && year % 100 != 0) || year % 400 == 0;
> 	}
> 	
> 	 public static void main(String args[] ) {
> 		 Scanner scan = new Scanner(System.in);
> 			int day=scan.nextInt();
> 			int month=scan.nextInt();
>
> 			int year=scan.nextInt();
> 			DayofWeek dow=new DayofWeek();
> 		    System.out.println(dow.dayOfTheWeek(day,month,year));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2045%20Solutions/DayofWeek.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 45 Solutions/DayofWeek.java
