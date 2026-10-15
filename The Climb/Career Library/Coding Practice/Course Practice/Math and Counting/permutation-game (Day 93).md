---
kind: "coding-problem"
title: "permutation-game (Day 93)"
collection: "Course Practice"
topic: "Math and Counting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 93 Solutions/permutation-game-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 93 Solutions/PermutationGame.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# permutation-game (Day 93)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Problem

Read the original PDF below. Its mathematical notation was not reliably preserved by text extraction.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · PermutationGame.txt
> ```java
> /* Enter your code here. Read input from STDIN. Print output to STDOUT */
> import java.util.*;
>
> public class Solution {
> 	int[] cache;
> 	int n;
> 	int[] vec;
> 	boolean solve(int conf) {
> 		if (cache[conf] != -1 )
> 			return cache[conf] == 1 ? true : false;
> 		int last = -1;
> 		boolean allWin = true;
> 		boolean increase = true;
> 		for (int i=0; i<n; i++)
> 			if ((conf&(1<<i)) != 0) {
> 				if (vec[i] < last) increase = false;
> 				allWin = allWin && solve(conf - (1<<i));
> 				last = vec[i];
> 			}
> 		boolean res = !(increase || allWin);
> 		cache[conf] = res ? 1 : 0;
> 		return res;
> 	}
> 	Solution() {
> 		Scanner sc = new Scanner(System.in);
> 		int nrt = sc.nextInt();
> 		for (int t=0; t<nrt; t++) {
> 			n = sc.nextInt();
> 			vec = new int[n];
> 			for (int i=0; i<n; i++) {
> 				vec[i] = sc.nextInt();
> 			}
> 			cache = new int[1<<n];
> 			Arrays.fill(cache, -1);
> 			if (solve((1<<n) - 1)) System.out.println("Alice");
> 			else System.out.println("Bob");
> 		}
> 	}
> 	public static void main(String args[]) {
> 		new Solution();
> 	}
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/permutation-game-English-61851501.pdf|permutation-game-English-61851501.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/permutation-game-English-61851501.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2093%20Solutions/permutation-game-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 93 Solutions/permutation-game-English.pdf
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2093%20Solutions/PermutationGame.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 93 Solutions/PermutationGame.txt
