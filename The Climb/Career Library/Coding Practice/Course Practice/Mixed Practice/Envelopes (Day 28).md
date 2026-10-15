---
kind: "coding-problem"
title: "Envelopes (Day 28)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 28 Solutions/Envelopes.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Envelopes (Day 28)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You have a number of envelopes with widths and heights given as a pair of integers (w, h). One envelope can fit into another if and only if both the width and height of one envelope is greater than the width and height of the other envelope.

What is the maximum number of envelopes can you put one inside other

Note:
Rotation is not allowed.

Example:

Input: [[5,4],[6,4],[6,7],[2,3]]
Output: 3 

### Explanation: 

The maximum number of envelopes you can put one inside other is 3 ([2,3] => [5,4] => [6,7]).

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Envelopes.java
> ```java
> /*
>  * 
>  You have a number of envelopes with widths and heights given as a pair of integers (w, h). One envelope can fit into another if and only if both the width and height of one envelope is greater than the width and height of the other envelope.
>
> What is the maximum number of envelopes can you put one inside other
>
> Note:
> Rotation is not allowed.
>
> Example:
>
> Input: [[5,4],[6,4],[6,7],[2,3]]
> Output: 3 
> Explanation: 
> The maximum number of envelopes you can put one inside other is 3 ([2,3] => [5,4] => [6,7]).
>
>
>  */
>
>
> import java.util.*;
>
> public class Envelopes {
> 	 public static int lengthOfLIS(int[] nums) {
> 	        int[] dp = new int[nums.length];
> 	        int len = 0;
> 	        for (int num : nums) {
> 	            int i = Arrays.binarySearch(dp, 0, len, num);
> 	            if (i < 0) {
> 	                i = -(i + 1);
> 	            }
> 	            dp[i] = num;
> 	            if (i == len) {
> 	                len++;
> 	            }
> 	        }
> 	        return len;
> 	    }
>
> 	    public static int maxEnvelopes(int[][] envelopes) {
> 	        // sort on increasing in first dimension and decreasing in second
> 	        Arrays.sort(envelopes, new Comparator<int[]>() {
> 	            public int compare(int[] arr1, int[] arr2) {
> 	                if (arr1[0] == arr2[0]) {
> 	                    return arr2[1] - arr1[1];
> 	                } else {
> 	                    return arr1[0] - arr2[0];
> 	                }
> 	           }
> 	        });
> 	        // extract the second dimension and run LIS
> 	        int[] secondDim = new int[envelopes.length];
> 	        for (int i = 0; i < envelopes.length; ++i) secondDim[i] = envelopes[i][1];
> 	        return lengthOfLIS(secondDim);
> 	    }
> 	    
> 	
> 	/*
> 	 * public static int maxEnvelopes(int[][] envelopes) {
> 	    if(envelopes == null || envelopes.length == 0 
> 	       || envelopes[0] == null || envelopes[0].length != 2)
> 	        return 0;
> 	    Arrays.sort(envelopes, new Comparator<int[]>(){
> 	        public int compare(int[] arr1, int[] arr2){
> 	            if(arr1[0] == arr2[0])
> 	                return arr2[1] - arr1[1];
> 	            else
> 	                return arr1[0] - arr2[0];
> 	       } 
> 	    });
> 	    int dp[] = new int[envelopes.length];
> 	    int len = 0;
> 	    for(int[] envelope : envelopes){
> 	        int index = Arrays.binarySearch(dp, 0, len, envelope[1]);
> 	        if(index < 0)
> 	            index = -(index + 1);
> 	        dp[index] = envelope[1];
> 	        if(index == len)
> 	            len++;
> 	    }
> 	    return len;
> 	}
> 	*/
> 	public static void main(String args[] ) {
> 		 Scanner scan = new Scanner(System.in);
> 			int n=scan.nextInt();
>
> 			int[][] envelopes=new int[n][2];
> 		       for(int i=0; i<n; i++)
> 		       {
> 		           for(int j=0; j<2; j++)
> 		           {
> 		        	   envelopes[i][j] = scan.nextInt();
> 		           }
> 		       }
> 		       System.out.println(maxEnvelopes(envelopes));
> 	}
> 	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2028%20Solutions/Envelopes.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 28 Solutions/Envelopes.java
