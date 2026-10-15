---
kind: "coding-problem"
title: "Toggle Sequence (Day 116)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 116 Solutions/ToggleSequence.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Toggle Sequence (Day 116)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Gopal is given a list of integers.
Your task to is find out, the length of the longest subsequence that is a
toggle sequence.

Toggle Sequence means, the difference between the consecutive numbers
are alternate positive and negative.

For Example:
Given list of integers = 1 3 2 5 4 
the consecutive differences are [ 2, -1, 3, -1], 
the differences are alternate +ve and -ve.
So, complete list is a toggle sequence.

If the list of integers = 1 3 2 4 5,
the consecutive differences are [ 2, -1, 2, 1], not alternate +ve and -ve.
Not a toggle sequence.

Note: A sequence with fewer than two elements is a toggle sequence.

Input Format:
-------------
Space separated Integers, List

Output Format:
--------------
Print the length of the longest toggle sequence


Sample Input-1:
---------------
1 7 4 9 2 5

Sample Output-1:
----------------
6


### Explanation

------------
Given list of integers = 1 7 4 9 2 5
the consecutive differences are [ 6, -3, 5, -7, 3], 
the differences are alternate +ve and -ve.
So, complete list is a toggle sequence.

Sample Input-2:
---------------
1 5 4 3 7 9 10

Sample Output-2:
----------------
4


### Explanation

------------
Given list of integers = 1 5 4 3 7 9 10
the consecutive differences are [ 4, -1, -1, 4, 2, 1], 
the differences are alternate +ve and -ve.
So, there are more than one toggle sequences of length 4.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ToggleSequence.java
> ```java
> /*
> Gopal is given a list of integers.
> Your task to is find out, the length of the longest subsequence that is a
> toggle sequence.
>
> Toggle Sequence means, the difference between the consecutive numbers
> are alternate positive and negative.
>
> For Example:
> Given list of integers = 1 3 2 5 4 
> the consecutive differences are [ 2, -1, 3, -1], 
> the differences are alternate +ve and -ve.
> So, complete list is a toggle sequence.
>
> If the list of integers = 1 3 2 4 5,
> the consecutive differences are [ 2, -1, 2, 1], not alternate +ve and -ve.
> Not a toggle sequence.
>
> Note: A sequence with fewer than two elements is a toggle sequence.
>
> Input Format:
> -------------
> Space separated Integers, List
>
> Output Format:
> --------------
> Print the length of the longest toggle sequence
>
>
> Sample Input-1:
> ---------------
> 1 7 4 9 2 5
>
> Sample Output-1:
> ----------------
> 6
>
> Explanation:
> ------------
> Given list of integers = 1 7 4 9 2 5
> the consecutive differences are [ 6, -3, 5, -7, 3], 
> the differences are alternate +ve and -ve.
> So, complete list is a toggle sequence.
>
> Sample Input-2:
> ---------------
> 1 5 4 3 7 9 10
>
> Sample Output-2:
> ----------------
> 4
>
> Explanation:
> ------------
> Given list of integers = 1 5 4 3 7 9 10
> the consecutive differences are [ 4, -1, -1, 4, 2, 1], 
> the differences are alternate +ve and -ve.
> So, there are more than one toggle sequences of length 4.
>
> */
>
> import java.util.*;
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
>
> public class ToggleSequence {
>     public int toggleMaxLength(int[] nums) {
>         
>         if( nums.length == 0 ) return 0;
>         
>         int[] up = new int[nums.length];
>         int[] down = new int[nums.length];
>         
>         up[0] = 1;
>         down[0] = 1;
>         
>         for(int i = 1 ; i < nums.length; i++){
>             if( nums[i] > nums[i-1] ){
>                 up[i] = down[i-1]+1;
>                 down[i] = down[i-1];
>             }else if( nums[i] < nums[i-1]){
>                 down[i] = up[i-1]+1;
>                 up[i] = up[i-1];
>             }else{
>                 down[i] = down[i-1];
>                 up[i] = up[i-1];
>             }
>         }
>         
>         return Math.max(down[nums.length-1],up[nums.length-1]);
>     }
> 		
> 	public static void main(String args[] ) throws IOException {
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 		String str = br.readLine();
> 		String[] sarr = str.split(" ");
> 		int[] nums = Arrays.asList(sarr).stream().mapToInt(Integer::parseInt).toArray();
>
> 		System.out.println(new ToggleSequence().toggleMaxLength(nums));
> 	}
> 	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20116%20Solutions/ToggleSequence.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 116 Solutions/ToggleSequence.java
