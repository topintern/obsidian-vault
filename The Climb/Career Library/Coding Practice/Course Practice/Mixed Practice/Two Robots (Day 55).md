---
kind: "coding-problem"
title: "Two Robots (Day 55)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 55 Solutions/TwoRobots.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Two Robots (Day 55)

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

> [!example]- Reference 1 · TwoRobots.txt
> ```java
> URL : https://www.hackerrank.com/challenges/two-robots/problem
> /*
> You have a warehouse with M containers filled with an infinite number of candies. 
> The containers are arranged in a single row, equally spaced to be 1 meter apart. 
> You also have 2 robots that can pick up 1 piece of candy and transport it between any two containers.
>
> The robots take instructions in the form of queries consisting of two integers,  Ma and Mb, respectively. 
> To execute a query, a robot travels to container Ma, picks up 1 candy, transports it to container Mb, 
> and then stops at Mb until it receives another query.
>
> Calculate the minimum total distance the robots must travel to execute N queries in order.
>
> Note: You choose which robot executes each query.
>
> Input Format:
> The first line has two space-separated integers, M (the number of containers) and N (the number of queries).
> The  subsequent lines each contain two space-separated integers, Ma and Mb respectively,
> each line Ni describes the ith query.
>
> Output Format:
> Print an integer denoting the minimum total distance that the robots must travel to execute the queries in order.
>
> Sample Input-1
> 			5 4
> 			1 5
> 			3 2
> 			4 1
> 			2 4
> Sample Output-1
> 			11
>
> Sample Input-2
> 			10 3
> 			2 4
> 			5 4
> 			9 8
> Sample Output-2
> 			5
>
> Explanation
> 	Sample-1:
> 		Robot-1: 1 5, Distance is 4 meters.
> 		Robot-2: 3 2, Distance is 1 meter.
> 		Robot-1: From 5 4 ,then 4 1, Distance is 4 meters.
> 		Robot-2: From 2 2, then 2 4, Distance is 2 meters.
> 		Sum the distances traveled ( 4 + 1+ 4 + 2 = 11 ).
>
> 	Sample-2:
> 		Robot-1: 2 4 , Distance is 4 meters.
> 		Robot-1: From 4 5, then 5 4, Distance is 2 meters.
> 		Robot-1: 9 8, Distance is 1 meters.
> 		Sum the distances traveled (2 + 2 + 1 = 5).
>
>
> ========= Testcases Program-1 =========
> case =1
> input =7 10
> 3 4
> 6 1
> 5 7
> 1 4
> 4 5
> 5 2
> 5 2
> 5 3
> 7 2
> 3 5
> output =34
>
> case =2
> input =8 10
> 6 1
> 2 6
> 8 2
> 3 5
> 7 2
> 1 5
> 2 1
> 1 8
> 2 8
> 2 7
> output =59
>
> case =3
> input =5 7
> 4 1
> 5 3
> 5 2
> 3 1
> 4 5
> 4 3
> 1 3
> output =21
>
> case =4
> input =6 5
> 6 5
> 1 5
> 1 5
> 2 5
> 3 1
> output =23
>
> case =5
> input =5 8
> 4 3
> 1 3
> 3 1
> 2 3
> 5 1
> 2 4
> 4 3
> 4 5
> output =19
>
> case =6
> input =10 7
> 2 1
> 5 7
> 1 8
> 8 2
> 8 5
> 7 4
> 2 9
> output =32
>
> case =7
> input =10 9
> 5 9
> 7 9
> 8 10
> 9 3
> 10 9
> 4 7
> 10 4
> 5 9
> 8 1
> output =40
>
> case =8
> input =5 4
> 1 5
> 3 2
> 4 1
> 2 4
> output =11
>
> */
>
> import java.io.*;
> import java.util.*;
>
> public class TwoRobots {
>     public static void main(String[] args) throws IOException {
>         BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
> 		StringTokenizer tokenizer = new StringTokenizer(reader.readLine());
> 		int m = Integer.parseInt(tokenizer.nextToken());
> 		int n = Integer.parseInt(tokenizer.nextToken());
> 		boolean st = false;
> 		int[] dp = new int[m+1];
> 		int l = 0;
> 		int maxVal = 10000000;
> 		for (int j = 0; j < n; j++) {
> 			tokenizer = new StringTokenizer(reader.readLine());
> 			int ma = Integer.parseInt(tokenizer.nextToken());
> 			int mb = Integer.parseInt(tokenizer.nextToken());
> 			int[] ndp = new int[m+1];
> 			Arrays.fill(ndp, maxVal);
> 			if (!st) {
> 				ndp[0] = Math.abs(ma-mb);
> 				st = true;
> 			} else {
> 				for (int k = 1; k <= m; k++) {
> 					if (dp[k]!=maxVal) ndp[l] = Math.min(dp[k] + Math.abs(ma-k) + Math.abs(ma-mb), ndp[l]);
> 				}
> 				for (int k = 0; k <= m; k++) {
> 					if (dp[k]!=maxVal && k!=l) ndp[k] = dp[k] + Math.abs(l-ma)+Math.abs(ma - mb);
> 				}
> 				ndp[l] = Math.min(ndp[l], dp[0] + Math.abs(ma-mb));
> 			}
> 			l = mb;
> 			dp = ndp;
> 			}
>             int mn = maxVal;
>             for (int j = 0; j <= m; j++) {
>                 if (dp[j] != maxVal) mn = Math.min(mn, dp[j]);
>             }
>             System.out.println(mn);
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2055%20Solutions/TwoRobots.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 55 Solutions/TwoRobots.txt
