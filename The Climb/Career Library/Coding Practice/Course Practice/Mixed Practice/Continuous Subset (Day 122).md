---
kind: "coding-problem"
title: "Continuous Subset (Day 122)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 122 solutions/ContinuousSubset.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Continuous Subset (Day 122)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a set of weights of n items weights[], and another item wieght w.
Your task is to check if the sum of weights of continuous subset is equal to 
one of the multiple of w, where subset size should be minimum 2.

For Example: Mulitpke of w means, w=3 then multiple of w are
3, 6, 9, 12, .... so on.

Print true, if such subset sum is possible.
Otherwise, print false.

Input Format:
-------------
Line-1 : Two integers n and w, number of weights and weight to match.
Line-2 : n space separated integers, weights of n items.

Output Format:
--------------
Print a boolean value.


Sample Input-1:
---------------
5 4
1 2 3 5 6

Sample Output-1:
----------------
false


Sample Input-2:
---------------
5 4
1 2 3 6 5

Sample Output-2:
----------------
true


### Explanation: 

------------
sum of  continuous subset of weights [1,2,3,6]  equals to 12, multiple of 4.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ContinuousSubset.java
> ```java
> /*
> Given a set of weights of n items weights[], and another item wieght w.
> Your task is to check if the sum of weights of continuous subset is equal to 
> one of the multiple of w, where subset size should be minimum 2.
>
> For Example: Mulitpke of w means, w=3 then multiple of w are
> 3, 6, 9, 12, .... so on.
>
> Print true, if such subset sum is possible.
> Otherwise, print false.
>
> Input Format:
> -------------
> Line-1 : Two integers n and w, number of weights and weight to match.
> Line-2 : n space separated integers, weights of n items.
>
> Output Format:
> --------------
> Print a boolean value.
>
>
> Sample Input-1:
> ---------------
> 5 4
> 1 2 3 5 6
>
> Sample Output-1:
> ----------------
> false
>
>
> Sample Input-2:
> ---------------
> 5 4
> 1 2 3 6 5
>
> Sample Output-2:
> ----------------
> true
>
> Explanation: 
> ------------
> sum of  continuous subset of weights [1,2,3,6]  equals to 12, multiple of 4.
>
> */
> import java.util.*;
>
> class ContinuousSubset {
>     public boolean checkSubarraySum(int[] weights, int k) {
>         k = k == 0 ? Integer.MAX_VALUE : (k < 0 ? -k : k); // make sure k is positive; if k is zero, we won't do mod at all
>         if ((weights.length + 2) / 2 > k) return true; // we have (length + 1 > k * 2) prefix sum but k remainder and k positions that the same remainders next to each other, then there is at least two prefix with the same remainder and the distance is larger than one
>         
>         Set<Integer> set = new HashSet<>();
>         int last = 0; // the prefix sum one element earlier
>         for (int weight : weights) {
>             int cur = (last + weight) % k; // get newest prefix sum mod k
>             if (set.contains(cur)) return true;
>             set.add(last); // add old prefix sum into HashSet
>             last = cur; // update old prefix sum
>         }
>         return false;
>     }
> 	
> 	public static void main(String[] args) {
> 		Scanner sc = new Scanner(System.in);
> 		int n=sc.nextInt();
> 		int w=sc.nextInt();
> 		int[] weights=new int[n];
> 		for(int i=0;i<n;i++)
> 			weights[i]=sc.nextInt();
> 		System.out.print(new ContinuousSubset().checkSubsetSum(weights,w));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20122%20solutions/ContinuousSubset.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 122 solutions/ContinuousSubset.java
