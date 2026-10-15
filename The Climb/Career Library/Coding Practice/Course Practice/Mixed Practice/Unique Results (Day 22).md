---
kind: "coding-problem"
title: "Unique Results (Day 22)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 22/UniqueResults.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Unique Results (Day 22)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

We have an array A of non-negative integers.

For every (contiguous) subarray B = [A[i], A[i+1], ..., A[j]] (with i <= j), 
we take the bitwise OR of all the elements in B, obtaining a result A[i] | A[i+1] | ... | A[j].

Return the number of possible results.  (
Results that occur more than once are only counted once in the final answer.)

 

Example 1:

Input: [0]
Output: 1

### Explanation: 

There is only one possible result: 0.
Example 2:

Input: [1,1,2]
Output: 3

### Explanation: 

The possible subarrays are [1], [1], [2], [1, 1], [1, 2], [1, 1, 2].
These yield the results 1, 1, 2, 1, 3, 3.
There are 3 unique values, so the answer is 3.
Example 3:

Input: [1,2,4]
Output: 6

### Explanation: 

The possible results are 1, 2, 3, 4, 6, and 7.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · UniqueResults.java
> ```java
> /*
> We have an array A of non-negative integers.
>
> For every (contiguous) subarray B = [A[i], A[i+1], ..., A[j]] (with i <= j), 
> we take the bitwise OR of all the elements in B, obtaining a result A[i] | A[i+1] | ... | A[j].
>
> Return the number of possible results.  (
> Results that occur more than once are only counted once in the final answer.)
>
>  
>
> Example 1:
>
> Input: [0]
> Output: 1
> Explanation: 
> There is only one possible result: 0.
> Example 2:
>
> Input: [1,1,2]
> Output: 3
> Explanation: 
> The possible subarrays are [1], [1], [2], [1, 1], [1, 2], [1, 1, 2].
> These yield the results 1, 1, 2, 1, 3, 3.
> There are 3 unique values, so the answer is 3.
> Example 3:
>
> Input: [1,2,4]
> Output: 6
> Explanation: 
> The possible results are 1, 2, 3, 4, 6, and 7.
> */
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.*;
>
> class UniqueResults
> {
> 	public static int subarrayBitwiseORs(int[] A) {
>         Set<Integer> ans = new HashSet();
>         Set<Integer> cur = new HashSet();
>         cur.add(0);
>         for (int x: A) {
>             Set<Integer> cur2 = new HashSet();
>             for (int y: cur)
>                 cur2.add(x | y);
>             cur2.add(x);
>             cur = cur2;
>             ans.addAll(cur);
>         }
>
>         return ans.size();
>     }
> 	   public static void main(String args[] ) throws IOException {
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		String[] numberline = str.split(" ");
> 		int[] nums = Arrays.asList(numberline).stream().mapToInt(Integer::parseInt).toArray();
> 		System.out.println(subarrayBitwiseORs(nums));   
> 	}
> }
>
> /*
> Actually, this approach can be better than that. At the kth step, say we have all the result(i, k) in some set cur. 
> Then we can find the next cur set (for k -> k+1) by using result(i, k+1) = result(i, k) | A[k+1].
>
> However, the number of unique values in this set cur is at most 32, 
> since the list result(k, k), result(k-1, k), result(k-2, k), ... is monotone increasing, 
> and any subsequent values that are different must have more 1s in it's binary representation (to a maximum of 32 ones).
>
> Algorithm
> In the kth step, we'll maintain cur: the set of results A[i] | ... | A[k] for all i.
> These results will be included in our final answer set.
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2022/UniqueResults.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 22/UniqueResults.java
