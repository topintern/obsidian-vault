---
kind: "coding-problem"
title: "Dice Throws (Day 13)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day13 Solutions/DiceThrows.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Dice Throws (Day 13)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You have d dice, and each die has f faces numbered 1, 2, ..., f.

Return the number of possible ways (out of fd total ways) modulo 10^9 + 7 to roll the dice so the sum of the face up numbers equals target.

 



Example 1:

Input: d = 1, f = 6, target = 3
Output: 1

### Explanation: 

You throw one die with 6 faces.  There is only one way to get a sum of 3.

Example 2:

Input: d = 2, f = 6, target = 7
Output: 6

### Explanation: 

You throw two dice, each with 6 faces.  There are 6 ways to get a sum of 7:
1+6, 2+5, 3+4, 4+3, 5+2, 6+1.

Example 3:

Input: d = 2, f = 5, target = 10
Output: 1

### Explanation: 

You throw two dice, each with 5 faces.  There is only one way to get a sum of 10: 5+5.

Example 4:

Input: d = 1, f = 2, target = 3
Output: 0

### Explanation: 

You throw one die with 2 faces.  There is no way to get a sum of 3.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · DiceThrows.java
> ```java
> /*
>  * 
> You have d dice, and each die has f faces numbered 1, 2, ..., f.
>
> Return the number of possible ways (out of fd total ways) modulo 10^9 + 7 to roll the dice so the sum of the face up numbers equals target.
>
>  
>
>
>
> Example 1:
>
> Input: d = 1, f = 6, target = 3
> Output: 1
> Explanation: 
> You throw one die with 6 faces.  There is only one way to get a sum of 3.
>
> Example 2:
>
> Input: d = 2, f = 6, target = 7
> Output: 6
> Explanation: 
> You throw two dice, each with 6 faces.  There are 6 ways to get a sum of 7:
> 1+6, 2+5, 3+4, 4+3, 5+2, 6+1.
>
> Example 3:
>
> Input: d = 2, f = 5, target = 10
> Output: 1
> Explanation: 
> You throw two dice, each with 5 faces.  There is only one way to get a sum of 10: 5+5.
>
> Example 4:
>
> Input: d = 1, f = 2, target = 3
> Output: 0
> Explanation: 
> You throw one die with 2 faces.  There is no way to get a sum of 3.
>
>  */
>
> package Elite2020;
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.*;
>
> public class DiceThrows {
> 	    static Map<String, Integer> memo = new HashMap<>();
> 	    public static int numRollsToTarget(int d, int f, int target) {
> 	        if (d == 0 && target == 0) {
> 	            return 1;
> 	        }
> 	        if (d == 0 || target == 0) {
> 	            return 0;
> 	        }
> 	        String str = d + " " + target;
> 	        if (memo.containsKey(str)) {
> 	            return memo.get(str);
> 	        }
> 	        int res = 0;
> 	        for (int i = 1; i <= f; i++) {
> 	            if (target >= i) {
> 	                res = (res + numRollsToTarget(d - 1, f, target - i));
> 	            } else {
> 	                break;
> 	            }
> 	        }
> 	        memo.put(str, res);
> 	        return res;
> 	    }
> 	      
> 	     
> 	    public static void main(String[] args) throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 	    	int ndice=Integer.parseInt(br.readLine());
> 			int faces=Integer.parseInt(br.readLine());
> 			int target=Integer.parseInt(br.readLine());
> 			
> 			
> 	        System.out.println(numRollsToTarget(ndice, faces, target)); 
> 	    
> 	    } 
> 	}
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day13%20Solutions/DiceThrows.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day13 Solutions/DiceThrows.java
