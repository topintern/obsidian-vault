---
kind: "coding-problem"
title: "Strange Coins (Day 104)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 104 Solutions/StrangeCoins.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Strange Coins (Day 104)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Problem

The source has reference code without a separate problem statement. Establish its inputs, expected outputs, and constraints before practising.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · StrangeCoins.java
> ```java
> import java.util.Scanner;
>
> class StrangeCoins{
> 	public static double probabilityOfHeads(double[] prob, int target) {
>         double[] dp = new double[target + 1];
>         dp[0] = 1.0;
>         for (int i = 0; i < prob.length; ++i)
>             for (int k = Math.min(i + 1, target); k >= 0; --k)
>                 dp[k] = (k > 0 ? dp[k - 1] : 0) * prob[i] + dp[k] * (1 - prob[i]);
>         return dp[target];
>     }
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		int n=sc.nextInt();
> 		double prob[]=new double[n];
> 		for(int i=0;i<n;i++)
> 			prob[i]=sc.nextDouble();
> 		int target=sc.nextInt();
> 		
> 		System.out.println(probabilityOfHeads(prob,target));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20104%20Solutions/StrangeCoins.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 104 Solutions/StrangeCoins.java
