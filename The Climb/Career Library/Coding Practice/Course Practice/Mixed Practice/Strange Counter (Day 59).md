---
kind: "coding-problem"
title: "Strange Counter (Day 59)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 59 Solutions/StrangeCounter.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Strange Counter (Day 59)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Bob has a strange counter. At the first second, it displays the number 3. 
Each second, the number displayed by the counter decrements by 1 until it reaches 1.

The counter counts down in cycles. In next second, the timer resets to 2*the initial number of prior cycle
 and continues counting down. 
The diagram below shows the counter values for each time t in the first three cycles:

time	value		time	value		time	value
   1		3		 		4		6		 	  10		12
   2		2		 		5		5		 	  11		11
   3		1		 		6		4		 	  12		10
							7		3		 	  13		9
							8		2		 	  14		8
							9		1		 	  15		7
												  16		6
												  17		5
												  18		4
												  19		3
												  20		2
												  21		1
									
Find and print the value displayed by the counter at time t.

Input Format:
A single integer denoting the value of t.

Output Format:
Print the value displayed by the strange counter at the given time t.

Sample Input
	4
Sample Output	
	6
Explanation
Time  t=4, marks the beginning of the second cycle. 
It is double the number displayed at the beginning of the first cycle:2*3=6. 


========= Testcases Program-1 =========
case =1
input =4
output =6

case =2
input =1
output =3

case =3
input =1000
output =534

case =4
input =32434
output =16716

case =5
input =24
output =22

case =6
input =1023
output =511

case =7
input =9
output =1

case =8
input =17
output =5

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · StrangeCounter.java
> ```java
> /*
> Bob has a strange counter. At the first second, it displays the number 3. 
> Each second, the number displayed by the counter decrements by 1 until it reaches 1.
>
> The counter counts down in cycles. In next second, the timer resets to 2*the initial number of prior cycle
>  and continues counting down. 
> The diagram below shows the counter values for each time t in the first three cycles:
>
> time	value		time	value		time	value
>    1		3		 		4		6		 	  10		12
>    2		2		 		5		5		 	  11		11
>    3		1		 		6		4		 	  12		10
> 							7		3		 	  13		9
> 							8		2		 	  14		8
> 							9		1		 	  15		7
> 												  16		6
> 												  17		5
> 												  18		4
> 												  19		3
> 												  20		2
> 												  21		1
> 									
> Find and print the value displayed by the counter at time t.
>
> Input Format:
> A single integer denoting the value of t.
>
> Output Format:
> Print the value displayed by the strange counter at the given time t.
>
> Sample Input
> 	4
> Sample Output	
> 	6
> Explanation
> Time  t=4, marks the beginning of the second cycle. 
> It is double the number displayed at the beginning of the first cycle:2*3=6. 
>
>
> ========= Testcases Program-1 =========
> case =1
> input =4
> output =6
>
> case =2
> input =1
> output =3
>
> case =3
> input =1000
> output =534
>
> case =4
> input =32434
> output =16716
>
> case =5
> input =24
> output =22
>
> case =6
> input =1023
> output =511
>
> case =7
> input =9
> output =1
>
> case =8
> input =17
> output =5
>
> */
>
> import java.io.*;
> import java.util.*;
>
> public class StrangeCounter {
>
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         long t = in.nextLong();
>         long n = 3;
>         long increm = 3;
>         while(true){
>             if(t <= n){
>                 System.out.println(n - t + 1);
>                 return;
>             }
>             increm *= 2;
>             n += increm;
>         }
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2059%20Solutions/StrangeCounter.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 59 Solutions/StrangeCounter.java
