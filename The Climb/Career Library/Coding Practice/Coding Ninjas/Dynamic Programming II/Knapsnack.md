---
kind: "coding-problem"
title: "Knapsnack"
collection: "Coding Ninjas"
topic: "Dynamic Programming II"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-2/knapsack q.txt","CODING RESOURCES/coding ninjas/Dp-2/knapsack s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Knapsnack

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

A thief robbing a store and can carry a maximal weight of W into his knapsack. There are N items and ith item weigh wi and is of value vi. What is the maximum value V, that thief can take ?
Space complexity should be O(n).

### Input Format

Line 1 : N i.e. number of items
Line 2 : N Integers i.e. weights of items separated by space
Line 3 : N Integers i.e. values of items separated by space
Line 4 : Integer W i.e. maximum weight thief can carry

### Output Format

Line 1 : Maximum value V

### Constraints

1 <= N <= 10^4
1<= wi <= 100
1 <= vi <= 100

### Sample Input 1

```text
4
1 2 4 5
5 4 8 6
5
```

### Sample Output

```text
13
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · knapsack s.txt
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
> 	public static int knapsack(int[] weight,int value[],int maxWeight){
> 			int storagePrev[] = new int[maxWeight + 1];
> 		int storageCurrent[] = new int[maxWeight + 1];
> 		for(int i = 1; i < value.length+1; i++){
> 			for(int w = 1; w < maxWeight+1; w++){
> 				if(weight[i-1] > w){
>
> 					storageCurrent[w] = storagePrev[w];
> 				}
> 				else{
> 					storageCurrent[w] = Math.max(storagePrev[w - weight[i - 1]] + value[i - 1], storagePrev[w]);
> 				}
> 			}
> 			storagePrev = storageCurrent;
> 			storageCurrent = new int[maxWeight + 1];
> 		}
> 		return storagePrev[maxWeight];
> 	}
> 	
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/knapsack%20q.txt) · CODING RESOURCES/coding ninjas/Dp-2/knapsack q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/knapsack%20s.txt) · CODING RESOURCES/coding ninjas/Dp-2/knapsack s.txt
