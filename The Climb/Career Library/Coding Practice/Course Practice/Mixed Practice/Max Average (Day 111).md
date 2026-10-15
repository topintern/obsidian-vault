---
kind: "coding-problem"
title: "Max Average (Day 111)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 111 Solutions/MaxAverage.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Max Average (Day 111)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a list of positive integers, You need to make K adjacent groups.
And calculate the average A of each group and add averages A's of all groups to S.
You need to find out that the value of S to be maximum.

Note: you must use every integer in A, 
      and that averages are not necessarily integers.

Input Format:
-------------
Line-1 -> Two integers N and K, number of array elements and number of groups
Line-2 -> N space separated integers, elements of the array.

Output Format:
--------------
Print a double value as your result.



Sample Input-1:
---------------
5 3
6 2 3 1 6

Sample Output-1:
----------------
14.0


### Explanation

------------
The best choice is to split A into [6], [2, 3, 1], [6]. The
answer is 96 + (2 + 3 + 1) / 3 + 6 = 14.
We could have also split A into [6, 2], [3], [1, 9], for
example.
That partition would lead to a total of 4 + 3 + 5 = 12, which is
not max.

Sample Input-1:
---------------
7 3
7 3 8 2 3 4 5

Sample Output-1:
----------------
16.5

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MaxAverage.txt
> ```java
> /*
> Given a list of positive integers, You need to make K adjacent groups.
> And calculate the average A of each group and add averages A's of all groups to S.
> You need to find out that the value of S to be maximum.
>
> Note: you must use every integer in A, 
>       and that averages are not necessarily integers.
>
> Input Format:
> -------------
> Line-1 -> Two integers N and K, number of array elements and number of groups
> Line-2 -> N space separated integers, elements of the array.
>
> Output Format:
> --------------
> Print a double value as your result.
>
>
>
> Sample Input-1:
> ---------------
> 5 3
> 6 2 3 1 6
>
> Sample Output-1:
> ----------------
> 14.0
>
> Explanation:
> ------------
> The best choice is to split A into [6], [2, 3, 1], [6]. The
> answer is 96 + (2 + 3 + 1) / 3 + 6 = 14.
> We could have also split A into [6, 2], [3], [1, 9], for
> example.
> That partition would lead to a total of 4 + 3 + 5 = 12, which is
> not max.
>
> Sample Input-1:
> ---------------
> 7 3
> 7 3 8 2 3 4 5
>
> Sample Output-1:
> ----------------
> 16.5
>
> */
> import java.util.*;
>
> class MaxAverage {
> 	public double largestSumOfAverages(int[] A, int K) {
>         int N = A.length;
>         double[][] memo = new double[N+1][N+1];
>         double cur = 0;
>         for (int i = 0; i < N; ++i) {
>             cur += A[i];
>             memo[i + 1][1] = cur / (i + 1);
>         }
>         return search(N, K, A, memo);
>     }
>
>     public double search(int n, int k, int[] A, double[][] memo) {
>         if (memo[n][k] > 0) return memo[n][k];
>         if (n < k) return 0;
>         double cur = 0;
>         for (int i = n - 1; i > 0; --i) {
>             cur += A[i];
>             memo[n][k] = Math.max(memo[n][k], search(i, k - 1, A, memo) + cur / (n - i));
>         }
>         return memo[n][k];
>     }
> 	
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		int N=sc.nextInt();
> 		int K=sc.nextInt();
> 		int arr[]=new int[N];
> 		for(int i=0;i<N;i++)
> 				arr[i]=sc.nextInt();
> 		System.out.println(new MaxAverage().largestSumOfAverages(arr,K));
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20111%20Solutions/MaxAverage.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 111 Solutions/MaxAverage.txt
