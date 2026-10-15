---
kind: "coding-problem"
title: "Perfect Squares (Day 29)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 29 Solutions/PerfectSquares.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Perfect Squares (Day 29)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.

Example 1:

Input: n = 12
Output: 3 
Explanation: 12 = 4 + 4 + 4.
Example 2:

Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · PerfectSquares.java
> ```java
> /*
>  * 
>  Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.
>
> Example 1:
>
> Input: n = 12
> Output: 3 
> Explanation: 12 = 4 + 4 + 4.
> Example 2:
>
> Input: n = 13
> Output: 2
> Explanation: 13 = 4 + 9.
>
>
>
>  */
>
>
>
> import java.util.*;
>
> public class PerfectSquares {
>
> 	public static int numSquares(int n) {
>
> 	    ArrayList<Integer> square_nums = new ArrayList<Integer>();
> 	    for (int i = 1; i * i <= n; ++i) {
> 	      square_nums.add(i * i);
> 	    }
>
> 	    Set<Integer> queue = new HashSet<Integer>();
> 	    queue.add(n);
>
> 	    int level = 0;
> 	    while (queue.size() > 0) {
> 	      level += 1;
> 	      Set<Integer> next_queue = new HashSet<Integer>();
>
> 	      for (Integer remainder : queue) {
> 	        for (Integer square : square_nums) {
> 	          if (remainder.equals(square)) {
> 	            return level;
> 	          } else if (remainder < square) {
> 	            break;
> 	          } else {
> 	            next_queue.add(remainder - square);
> 	          }
> 	        }
> 	      }
> 	      queue = next_queue;
> 	    }
> 	    return level;
> 	  }
> 	
> 	
> 	 public static void main(String args[] ) {
> 		 Scanner scan = new Scanner(System.in);
> 		       int n=scan.nextInt();     
> 		       System.out.println(numSquares(n));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2029%20Solutions/PerfectSquares.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 29 Solutions/PerfectSquares.java
