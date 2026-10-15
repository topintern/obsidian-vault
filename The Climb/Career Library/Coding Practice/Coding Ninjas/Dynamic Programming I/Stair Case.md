---
kind: "coding-problem"
title: "Stair Case"
collection: "Coding Ninjas"
topic: "Dynamic Programming I"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-1/staircase q.txt","CODING RESOURCES/coding ninjas/Dp-1/staircase s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Stair Case

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

A child is running up a staircase with n steps and can hop either 1 step, 2 steps or 3 steps at a time. Implement a method to count how many possible ways the child can run up to the stairs. You need to return all possible number of ways.
Time complexity of your code should be O(n).

### Input format

Integer n (No. of steps)

### Constraints

n <= 70

### Sample Input 1

```text
4
```

### Sample Output 1

```text
7
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · staircase s.txt
> ```java
>
> public class Solution {
> 	
> 	/* Your class should be named Solution.
> 	 * Don't write main() function.
> 	 * Don't read input, it is passed as function argument.
> 	 * Return output and don't print it.
> 	 * Taking input and printing output is handled automatically.
> 	 */
> 	
> public static long staircase(int n){
> 		
> 		if(n == 0)
> 			return 1;
> 		if(n == 1){
> 			return 1;
> 		}
> 		if(n == 2){
> 			return 2;
> 		}
> 		
> 		long ways[] = new long[n + 1];
> 		ways[0] = 1;
> 		ways[1] = 1;
> 		ways[2] =2;
> 		for(int i = 3; i <= n; i++){
> 			ways[i] = ways[i - 1] + ways[i - 2] + ways[i - 3];
> 		}
> 		return ways[n];
> 	}
> 	
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/staircase%20q.txt) · CODING RESOURCES/coding ninjas/Dp-1/staircase q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/staircase%20s.txt) · CODING RESOURCES/coding ninjas/Dp-1/staircase s.txt
