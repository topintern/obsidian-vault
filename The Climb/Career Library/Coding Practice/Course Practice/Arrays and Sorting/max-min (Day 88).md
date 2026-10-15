---
kind: "coding-problem"
title: "max-min (Day 88)"
collection: "Course Practice"
topic: "Arrays and Sorting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 88 Solutions/max-min-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 88 Solutions/MaxMin.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# max-min (Day 88)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

********Testcases**********
case =1
input =10 4
1 2 3 4 10 20 30 40 100 200
output =3

case =2
input =5 2
1 2 1 2 1
output =0

case =3
input =7 3
10 100 300 200 1000 20 30
output =20

case =4
input =15 4
312 855 382 172 907 11 372 209 294 568 410 557 846 50 111
output =88

case =5
input =20 6
7706 2633 2398 5747 4303 5814 9107 6582 3843 1764 705 5936 3032 9658 12 8524 2490 8668 7655 340
output =1905

case =6
input =30 8
6 2 6 8 0 0 5 1 7 2 3 2 1 9 9 8 5 2 6 9 8 2 8 5 4 6 9 6 5 7
output =1

case =7
input =50 10
81406 10873 57811 50613 83383 91254 71470 58520 53760 5540 20180 13418 3493 23704 41554 2797 1089 54610 19380 9703 62435 19491 20215 10651 6108 70124 45333 4668 48776 19621 41059 79607 40714 88651 77245 38025 54591 71064 73384 23258 24639 77192 39593 47116 73577 15532 37842 53561 38876 70476
output =10512

case =8
input =50 10
5 3 3 2 7 4 1 6 4 6 7 7 2 9 2 7 3 8 2 6 4 2 9 7 5 6 1 1 9 5 9 6 8 6 3 5 4 6 5 3 4 6 5 8 5 3 3 9 9 6
output =1

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MaxMin.java
> ```java
> /*
> *********Testcases**********
> case =1
> input =10 4
> 1 2 3 4 10 20 30 40 100 200
> output =3
>
> case =2
> input =5 2
> 1 2 1 2 1
> output =0
>
> case =3
> input =7 3
> 10 100 300 200 1000 20 30
> output =20
>
> case =4
> input =15 4
> 312 855 382 172 907 11 372 209 294 568 410 557 846 50 111
> output =88
>
> case =5
> input =20 6
> 7706 2633 2398 5747 4303 5814 9107 6582 3843 1764 705 5936 3032 9658 12 8524 2490 8668 7655 340
> output =1905
>
> case =6
> input =30 8
> 6 2 6 8 0 0 5 1 7 2 3 2 1 9 9 8 5 2 6 9 8 2 8 5 4 6 9 6 5 7
> output =1
>
> case =7
> input =50 10
> 81406 10873 57811 50613 83383 91254 71470 58520 53760 5540 20180 13418 3493 23704 41554 2797 1089 54610 19380 9703 62435 19491 20215 10651 6108 70124 45333 4668 48776 19621 41059 79607 40714 88651 77245 38025 54591 71064 73384 23258 24639 77192 39593 47116 73577 15532 37842 53561 38876 70476
> output =10512
>
> case =8
> input =50 10
> 5 3 3 2 7 4 1 6 4 6 7 7 2 9 2 7 3 8 2 6 4 2 9 7 5 6 1 1 9 5 9 6 8 6 3 5 4 6 5 3 4 6 5 8 5 3 3 9 9 6
> output =1
>
>
> */
> import java.util.*;
>
> public class MaxMin {
> 	public static void main(String[] args)  {
> 		Scanner in=new Scanner(System.in);
> 		int numPackets = in.nextInt();
> 		int numKids = in.nextInt();
> 		int[] packets = new int[numPackets];
> 		
> 		for(int i = 0; i < numPackets; i ++)
> 		{
> 			packets[i] = in.nextInt();
> 		}
> 		
> 		int best = Integer.MAX_VALUE;
> 		
> 		Arrays.sort(packets);
> 		for(int j = numKids - 1; j < numPackets; j ++)
> 		{
> 			int i = j - numKids + 1;
> 			int unf = packets[j] - packets[i];
> 			best = Math.min(best, unf);
> 		}
> 		
> 		System.out.println(best);
> 	}
> }
>
>
> 81406 10873 57811 50613 83383 91254 71470 58520 53760 5540 20180 13418 3493 23704 41554 2797 1089 54610 19380 9703 62435 19491 20215 10651 6108 70124 45333 4668 48776 19621 41059 79607 40714 88651 77245 38025 54591 71064 73384 23258 24639 77192 39593 47116 73577 15532 37842 53561 38876 70476
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/max-min-English-32b6b5f6.pdf|max-min-English-32b6b5f6.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/max-min-English-32b6b5f6.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2088%20Solutions/max-min-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 88 Solutions/max-min-English.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2088%20Solutions/MaxMin.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 88 Solutions/MaxMin.java
