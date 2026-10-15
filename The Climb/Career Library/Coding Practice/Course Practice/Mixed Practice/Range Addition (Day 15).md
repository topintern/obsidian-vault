---
kind: "coding-problem"
title: "Range Addition (Day 15)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 15 Solutions/RangeAddition.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Range Addition (Day 15)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Assume you have an array of length n initialized with all 0's and are given k update operations.

Each operation is represented as a triplet: [startIndex, endIndex, inc] which increments each element of subarray A[startIndex ... endIndex] (startIndex and endIndex inclusive) with inc.

Return the modified array after all k operations were executed.

Example:

Input: length = 5, updates = [[1,3,2],[2,4,3],[0,2,-2]]
Output: [-2,0,3,5,3]

### Explanation:


Initial state:
[0,0,0,0,0]

After applying operation [1,3,2]:
[0,2,2,2,0]

After applying operation [2,4,3]:
[0,2,5,5,3]

After applying operation [0,2,-2]:
[-2,0,3,5,3]


====================================================================

Just store every start index for each value and at end index plus one minus it

for example it will look like:

[1 , 3 , 2] , [2, 3, 3] (length = 5)

res[ 0, 2 ,0, 0 -2 ]

res[ 0 ,2, 3, 0, -5]

sum 0, 2, 5, 5, 0

res[0, 2, 5, 5, 0]

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · RangeAddition.java
> ```java
> /*
>  * 
>  Assume you have an array of length n initialized with all 0's and are given k update operations.
>
> Each operation is represented as a triplet: [startIndex, endIndex, inc] which increments each element of subarray A[startIndex ... endIndex] (startIndex and endIndex inclusive) with inc.
>
> Return the modified array after all k operations were executed.
>
> Example:
>
> Input: length = 5, updates = [[1,3,2],[2,4,3],[0,2,-2]]
> Output: [-2,0,3,5,3]
> Explanation:
>
> Initial state:
> [0,0,0,0,0]
>
> After applying operation [1,3,2]:
> [0,2,2,2,0]
>
> After applying operation [2,4,3]:
> [0,2,5,5,3]
>
> After applying operation [0,2,-2]:
> [-2,0,3,5,3]
>
>
> ====================================================================
>
> Just store every start index for each value and at end index plus one minus it
>
> for example it will look like:
>
> [1 , 3 , 2] , [2, 3, 3] (length = 5)
>
> res[ 0, 2 ,0, 0 -2 ]
>
> res[ 0 ,2, 3, 0, -5]
>
> sum 0, 2, 5, 5, 0
>
> res[0, 2, 5, 5, 0]
>
>
>  */
>
> package Elite2020;
>
> import java.util.Arrays;
> import java.util.Scanner;
>
> public class RangeAddition {
>
> 	public static int[] getModifiedArray(int length, int[][] updates) {
>
> 	    int[] res = new int[length];
> 	     for(int[] update : updates) {
> 	        int value = update[2];
> 	        int start = update[0];
> 	        int end = update[1];
> 	        
> 	        res[start] += value;
> 	        
> 	        if(end < length - 1)
> 	            res[end + 1] -= value;
> 	        
> 	    }
> 	    
> 	    int sum = 0;
> 	    for(int i = 0; i < length; i++) {
> 	        sum += res[i];
> 	        res[i] = sum;
> 	    }
> 	    
> 	    return res;
> 	}
> 	
> 	
> 	public static void main(String args[] ) {
> 		 Scanner scan = new Scanner(System.in);
> 			int l=scan.nextInt();
>
> 			int n=scan.nextInt();
>
> 			int[][] updates=new int[n][3];
> 		       for(int i=0; i<n; i++)
> 		       {
> 		           for(int j=0; j<3; j++)
> 		           {
> 		        	   updates[i][j] = scan.nextInt();
> 		           }
> 		       }
> 		       System.out.println(Arrays.toString(getModifiedArray(l,updates)));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2015%20Solutions/RangeAddition.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 15 Solutions/RangeAddition.java
