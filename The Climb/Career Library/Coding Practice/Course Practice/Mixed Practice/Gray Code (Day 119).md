---
kind: "coding-problem"
title: "Gray Code (Day 119)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 119 Solutons/GrayCode.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Gray Code (Day 119)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a integer value N, indicates number of bits in a binary number.

Your task is to design a Binary Code System, 
where two consecutive values in BCS having N bits, must have one bit difference only.
For example refer the sample testcases.

Find and print the integer values of BCS, starting from 0.


Input Format:
-------------
A integer N, number of bits in BCS

Output Format:
--------------
Print the list of integer values, in BCS form. 


Sample Input-1:
---------------
2

Sample Output-1:
----------------
[0, 1, 3, 2]


### Explanation

------------
00 - 0
01 - 1
11 - 3
10 - 2

Sample Input-2:
---------------
3

Sample Output-2:
----------------
[0, 1, 3, 2, 6, 7, 5, 4]


### Explanation

------------
000 - 0
001 - 1
011 - 3
010 - 2
110 - 6
111 - 7
101 - 5
100 - 4

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · GrayCode.java
> ```java
> /*
> Given a integer value N, indicates number of bits in a binary number.
>
> Your task is to design a Binary Code System, 
> where two consecutive values in BCS having N bits, must have one bit difference only.
> For example refer the sample testcases.
>
> Find and print the integer values of BCS, starting from 0.
>
>
> Input Format:
> -------------
> A integer N, number of bits in BCS
>
> Output Format:
> --------------
> Print the list of integer values, in BCS form. 
>
>
> Sample Input-1:
> ---------------
> 2
>
> Sample Output-1:
> ----------------
> [0, 1, 3, 2]
>
> Explanation:
> ------------
> 00 - 0
> 01 - 1
> 11 - 3
> 10 - 2
>
> Sample Input-2:
> ---------------
> 3
>
> Sample Output-2:
> ----------------
> [0, 1, 3, 2, 6, 7, 5, 4]
>
> Explanation:
> ------------
> 000 - 0
> 001 - 1
> 011 - 3
> 010 - 2
> 110 - 6
> 111 - 7
> 101 - 5
> 100 - 4
>
> */
>
> import java.util.*;
>
> class GrayCode {
> 	public List<Integer> grayCode(int n) {
> 		List<Integer> rs=new ArrayList<Integer>();
> 		rs.add(0);
> 		for(int i=0;i<n;i++){
> 			int size=rs.size();
> 			for(int k=size-1;k>=0;k--)
> 				rs.add(rs.get(k) | 1<<i);
> 		}
> 		return rs;
> 	}
> 	public static void main( String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		int N=sc.nextInt();
> 		System.out.println(new GrayCode().grayCode(N));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20119%20Solutons/GrayCode.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 119 Solutons/GrayCode.java
