---
kind: "coding-problem"
title: "Longest Sequence (Day 111)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 111 Solutions/LongestSequence.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Longest Sequence (Day 111)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Gunith is interested in series and sequence problems in Maths.
Gunith is given an array A of integers, he wants to find out 
a Sequence, which is long and subsequence of given array.

Subsequence AS is the list AS[i], AS[i1], AS[i2], .... AS[ik], from the array, 
where 0 <= i< i1 < i2 < ..<ik < A.length

The sequence S has to follow this rule, S[i+1] - S[i] are all the same value 
(for 0 <= i < S.length - 1 ), and Sequence S can be formed from A

Find out the Max possible length of the Longest Sequence.

Input Format:
-------------
Line-1 -> An integer N, number of array elements
Line-2 -> N space separated integers, elements of the array.

Output Format:
--------------
Print an integer as your result.


Sample Input-1:
---------------
4
2 6 10 14

Sample Output-1:
----------------
4


Sample Input-1:
---------------
7
2 5 6 8 10 11 14

Sample Output-1:
----------------
5


### Explanation

------------
The longest possible arithmetic series is 2 5 8 11 14.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · LongestSequence.txt
> ```java
> /*
> Gunith is interested in series and sequence problems in Maths.
> Gunith is given an array A of integers, he wants to find out 
> a Sequence, which is long and subsequence of given array.
>
> Subsequence AS is the list AS[i], AS[i1], AS[i2], .... AS[ik], from the array, 
> where 0 <= i< i1 < i2 < ..<ik < A.length
>
> The sequence S has to follow this rule, S[i+1] - S[i] are all the same value 
> (for 0 <= i < S.length - 1 ), and Sequence S can be formed from A
>
> Find out the Max possible length of the Longest Sequence.
>
> Input Format:
> -------------
> Line-1 -> An integer N, number of array elements
> Line-2 -> N space separated integers, elements of the array.
>
> Output Format:
> --------------
> Print an integer as your result.
>
>
> Sample Input-1:
> ---------------
> 4
> 2 6 10 14
>
> Sample Output-1:
> ----------------
> 4
>
>
> Sample Input-1:
> ---------------
> 7
> 2 5 6 8 10 11 14
>
> Sample Output-1:
> ----------------
> 5
>
> Explanation:
> ------------
> The longest possible arithmetic series is 2 5 8 11 14.
>
> */
>
> import java.util.*;
>
> class LongestSubsequence {
> 	 public int longestSequenceLength(int[] A) {
>         int res = 2, n = A.length;
>         HashMap<Integer, Integer>[] dp = new HashMap[n];
>         for (int j = 0; j < A.length; j++) {
>             dp[j] = new HashMap<>();
>             for (int i = 0; i < j; i++) {
>                 int d = A[j] - A[i];
>                 dp[j].put(d, dp[i].getOrDefault(d, 1) + 1);
>                 res = Math.max(res, dp[j].get(d));
>             }
>         }
>         return res;
>     }
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		int N=sc.nextInt();
> 		int arr[]=new int[N];
> 		for(int i=0;i<N;i++)
> 				arr[i]=sc.nextInt();
> 		System.out.println(new LongestSubsequence().longestSequenceLength(arr));
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20111%20Solutions/LongestSequence.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 111 Solutions/LongestSequence.txt
