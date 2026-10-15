---
kind: "coding-problem"
title: "Binary Strings (Day 113)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 113 Solutions/BinaryStrings.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Binary Strings (Day 113)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Mounika is creating the binary strings using P 1's and Q 0's.
A binary string contains only 0's and 1's.
She has given a list of binary strings binStr[] to be formed.

Her task is to find, the maximum number of binary strings can be formed, 
with given P 1's and Q 0's only. She cannot use any more 1's or 0's.

Input Format:
-------------
Line-1 -> A single line of space separated binary strings, binStr[].
Line-2 -> Two integers P and Q, P number of 1's and Q number of 0's


Output Format:
--------------
Print an integer as output, maximum number of binary strings can be formed.


Sample Input-1:
---------------
10 0001 111001 1 0
3 5

Sample Output-1:
----------------
4


### Explanation

------------
She can form 4 strings by the using of 3 1's and 5 0's
strings are 10, 0001, 1, 0.


Sample Input-2:
---------------
10 1 0
1 1

Sample Output-2:
----------------
2


### Explanation

------------
She can form 2 strings by the using of 1 1's and 1 0's
strings are 1, 0.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · BinaryStrings.java
> ```java
> /*
> Mounika is creating the binary strings using P 1's and Q 0's.
> A binary string contains only 0's and 1's.
> She has given a list of binary strings binStr[] to be formed.
>
> Her task is to find, the maximum number of binary strings can be formed, 
> with given P 1's and Q 0's only. She cannot use any more 1's or 0's.
>
> Input Format:
> -------------
> Line-1 -> A single line of space separated binary strings, binStr[].
> Line-2 -> Two integers P and Q, P number of 1's and Q number of 0's
>
>
> Output Format:
> --------------
> Print an integer as output, maximum number of binary strings can be formed.
>
>
> Sample Input-1:
> ---------------
> 10 0001 111001 1 0
> 3 5
>
> Sample Output-1:
> ----------------
> 4
>
> Explanation:
> ------------
> She can form 4 strings by the using of 3 1's and 5 0's
> strings are 10, 0001, 1, 0.
>
>
> Sample Input-2:
> ---------------
> 10 1 0
> 1 1
>
> Sample Output-2:
> ----------------
> 2
>
> Explanation:
> ------------
> She can form 2 strings by the using of 1 1's and 1 0's
> strings are 1, 0.
>
> */
> import java.util.*;
>
> class BinaryStrings {
> 	public int findMaxForm(String[] strs, int m, int n) {
> 		int[][] dp = new int[m+1][n+1];
> 		for (String s : strs) {
> 			int[] count = count(s);
> 			for (int i=m;i>=count[0];i--) 
> 				for (int j=n;j>=count[1];j--) 
> 					dp[i][j] = Math.max(1 + dp[i-count[0]][j-count[1]], dp[i][j]);
> 		}
> 		return dp[m][n];
> 	}
> 		
> 	public int[] count(String str) {
> 		int[] res = new int[2];
> 		for (int i=0;i<str.length();i++)
> 			res[str.charAt(i) - '0']++;
> 		return res;
> 	}
> 	
> 	public static void main(String args[])
> 	{
> 		Scanner sc = new Scanner(System.in);
> 		String str[]=sc.nextLine().split(" ");
> 		int Q=sc.nextInt();
> 		int P=sc.nextInt();
> 		System.out.println(new BinaryStrings().findMaxForm(str, P, Q));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20113%20Solutions/BinaryStrings.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 113 Solutions/BinaryStrings.java
