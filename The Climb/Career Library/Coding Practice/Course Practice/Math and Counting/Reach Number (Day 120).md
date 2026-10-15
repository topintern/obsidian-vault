---
kind: "coding-problem"
title: "Reach Number (Day 120)"
collection: "Course Practice"
topic: "Math and Counting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 120 Solutions/ReachNumber.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Reach Number (Day 120)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You are given a natural number N, and intially you are at position 0.
Your task is to jump to the position N, in minimum of steps.
The condition is to jump from a position P is as follows:
	- Your initial position P is at 0, P=0.
	- You can jump k steps forward or backward, on kth step.
	  i.e, either P= P+k, or P=P-k;

NOTE: N is in the range of [-10^9 , 10^9]

Input Format:
-------------
An integer N

Output Format:
--------------
Print an integer, minimum num of jumps


Sample Input-1:
---------------
3

Sample Output-1:
----------------
2


### Explanation

-------------
On the first step you jump from 0 to 1.
On the second step you jump from 1 to 3.


Sample Input-2:
---------------
2

Sample Output-2:
----------------
3


### Explanation

-------------
On the first step you jump from 0 to 1.
On the second step you jump  from 1 to -1.
On the third step you jump from -1 to 2.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ReachNumber.java
> ```java
> /*
> You are given a natural number N, and intially you are at position 0.
> Your task is to jump to the position N, in minimum of steps.
> The condition is to jump from a position P is as follows:
> 	- Your initial position P is at 0, P=0.
> 	- You can jump k steps forward or backward, on kth step.
> 	  i.e, either P= P+k, or P=P-k;
>
> NOTE: N is in the range of [-10^9 , 10^9]
>
> Input Format:
> -------------
> An integer N
>
> Output Format:
> --------------
> Print an integer, minimum num of jumps
>
>
> Sample Input-1:
> ---------------
> 3
>
> Sample Output-1:
> ----------------
> 2
>
> Explanation:
> -------------
> On the first step you jump from 0 to 1.
> On the second step you jump from 1 to 3.
>
>
> Sample Input-2:
> ---------------
> 2
>
> Sample Output-2:
> ----------------
> 3
>
> Explanation:
> -------------
> On the first step you jump from 0 to 1.
> On the second step you jump  from 1 to -1.
> On the third step you jump from -1 to 2.
>
> */
> import java.util.*;
>
> class ReachNumber {
>     public int reachNumber(int target) {
>         int step = 0, dis = 0;
>         target = Math.abs(target); 
>         while (dis < target || (dis - target) % 2 != 0) {
>             step++; 
>             dis += step;
>         }
>         return step; 
>     } 
> 	
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		int n=sc.nextInt();
> 		System.out.println(new ReachNumber().reachNumber(n));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20120%20Solutions/ReachNumber.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 120 Solutions/ReachNumber.java
