---
kind: "coding-problem"
title: "Painters Partition (Day 54)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 54 Solutions/PaintersPartition.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Painters Partition (Day 54)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

We have to paint n boards of length {A1, A2, .. An}. 
There are k painters available and each takes 1 unit time to paint 1 unit of board. 
The problem is to find the minimum time to get this job done under the constraints 
that any painter will only paint continuous sections of boards, say board {2, 3, 4} 
or only board {1} or nothing but not board {2, 4, 5}.


### Sample Input : 

10 10 10 10
2


### Sample Output : 

20


### Explanation

k = 2, A = {10, 10, 10, 10} 
Here we can divide the boards into 2
equal sized partitions, so each painter 
gets 20 units of board and the total
time taken is 20. 


### Sample Input 

10 20 30 40
2


### Sample Output : 

60


### Explanation

k = 2, A = {10, 20, 30, 40}
Here we can divide first 3 boards for
one painter and the last board for 
second painter.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · PaintersPartition.java
> ```java
> /*
> We have to paint n boards of length {A1, A2, .. An}. 
> There are k painters available and each takes 1 unit time to paint 1 unit of board. 
> The problem is to find the minimum time to get this job done under the constraints 
> that any painter will only paint continuous sections of boards, say board {2, 3, 4} 
> or only board {1} or nothing but not board {2, 4, 5}.
>
> Sample Input : 
> 10 10 10 10
> 2
>
> Sample Output : 
> 20
>
> Explanation:
> k = 2, A = {10, 10, 10, 10} 
> Here we can divide the boards into 2
> equal sized partitions, so each painter 
> gets 20 units of board and the total
> time taken is 20. 
>
> Sample Input :
> 10 20 30 40
> 2
>
> Sample Output : 
> 60
>
> Explanation:
> k = 2, A = {10, 20, 30, 40}
> Here we can divide first 3 boards for
> one painter and the last board for 
> second painter.
>
>  * 
>  */
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class PaintersPartition {
>
> 	// function to calculate sum between two indices 
> 	// in array 
> 	static int sum(int arr[], int from, int to) 
> 	{ 
> 		int total = 0; 
> 		for (int i = from; i <= to; i++) 
> 			total += arr[i]; 
> 		return total; 
> 	} 
>
> 	// for n boards and k partitions 
> 	static int partition(int arr[], int n, int k) 
> 	{ 
> 		// base cases	 
> 		if (k == 1) // one partition 
> 			return sum(arr, 0, n - 1);	 
> 		if (n == 1) // one board 
> 			return arr[0]; 
>
> 		int best = Integer.MAX_VALUE; 
>
> 		// find minimum of all possible maximum 
> 		// k-1 partitions to the left of arr[i], 
> 		// with i elements, put k-1 th divider 
> 		// between arr[i-1] & arr[i] to get k-th 
> 		// partition 
> 		for (int i = 1; i <= n; i++) 
> 			best = Math.min(best, Math.max(partition(arr, i, k - 1), 
> 									sum(arr, i, n - 1))); 
>
> 		return best; 
> 	} 
>
> 	public static void main(String args[]) throws IOException {
>
> 		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 		String str = br.readLine();
> 		String[] boards = str.split(" ");
> 		int[] A = Arrays.asList(boards).stream().mapToInt(Integer::parseInt).toArray();
>
> 		String painters = br.readLine();
> 		int k = Integer.parseInt(painters);
> 		System.out.println(partition(A, A.length, k));
>
> 	}
>
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2054%20Solutions/PaintersPartition.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 54 Solutions/PaintersPartition.java
