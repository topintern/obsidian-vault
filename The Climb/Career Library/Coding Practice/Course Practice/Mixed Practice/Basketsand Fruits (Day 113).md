---
kind: "coding-problem"
title: "Basketsand Fruits (Day 113)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 113 Solutions/BasketsandFruits.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Basketsand Fruits (Day 113)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a bunch of baskets in a row, each basket contains few fruits in it.
You can select K number of baskets, one after other.
The selection of basket is either from beginning or from the end the row.

Return the maximum number of fruits you have after K baskets collected.

Input Format:
-------------
Line-1 -> Two integers N and K, N is no of baskets and K is the basket count you can pick.
Line-2 -> N space separated integers fruits[], fruits in each basket.

Output Format:
--------------
Print an integer, Maximum num of fruits you can collect.


Sample Input-1:
---------------
7 3
1 2 3 4 5 6 1

Sample Output-1:
----------------
12


Sample Input-2:
---------------
5 3
2 2 2 2 2

Sample Output-2:
----------------
6

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · BasketsandFruits.java
> ```java
> /*
> Given a bunch of baskets in a row, each basket contains few fruits in it.
> You can select K number of baskets, one after other.
> The selection of basket is either from beginning or from the end the row.
>
> Return the maximum number of fruits you have after K baskets collected.
>
> Input Format:
> -------------
> Line-1 -> Two integers N and K, N is no of baskets and K is the basket count you can pick.
> Line-2 -> N space separated integers fruits[], fruits in each basket.
>
> Output Format:
> --------------
> Print an integer, Maximum num of fruits you can collect.
>
>
> Sample Input-1:
> ---------------
> 7 3
> 1 2 3 4 5 6 1
>
> Sample Output-1:
> ----------------
> 12
>
>
> Sample Input-2:
> ---------------
> 5 3
> 2 2 2 2 2
>
> Sample Output-2:
> ----------------
> 6
>
> */
> import java.util.*;
>
> class BasketsandFruits {
>     public int maxFruits(int[] basket, int k) {
>         int n = basket.length, lSum = 0;
>         for(int i = 0; i < k; ++i){
>             lSum += basket[i];
>         }
>         int max = lSum;
>         for(int rSum = 0, i = 0; i < k; ++i){
>             rSum += basket[n-1-i];
>             lSum -= basket[k-1-i];
>             max = Math.max(max,lSum+rSum);
>         }
>         return max;
>     }
> 	public static void main(String args[])
> 	{
> 		Scanner sc = new Scanner(System.in);
> 		int N=sc.nextInt();
> 		int K=sc.nextInt();
> 		int[] basket=new int[N];
> 		for(int i=0;i<N;i++)
> 				basket[i]=sc.nextInt();
> 		System.out.println(new BasketsandFruits().maxFruits(basket, K));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20113%20Solutions/BasketsandFruits.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 113 Solutions/BasketsandFruits.java
