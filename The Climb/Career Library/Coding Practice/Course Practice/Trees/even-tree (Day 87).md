---
kind: "coding-problem"
title: "even-tree (Day 87)"
collection: "Course Practice"
topic: "Trees"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 87 Solutions/even-tree-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 87 Solutions/EvenTree.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# even-tree (Day 87)

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

> [!example]- Reference 1 · EvenTree.java
> ```java
> import java.util.Scanner;
>
> public class EvenTree {
> 	static boolean[][] a;
> 	static boolean[][] v;
>
> 	public static void main(String[] args) {
> 		Scanner in = new Scanner(System.in);
> 		int n = in.nextInt();
> 		int m = in.nextInt();
> 		a = new boolean[n][n];
> 		v = new boolean[n][n];
> 		int f, t;
> 		for (int i = 0; i < m; i++) {
> 			f = in.nextInt() - 1;
> 			t = in.nextInt() - 1;
> 			a[f][t] = a[t][f] = true;
> 		}
> 		int cnt = 0;
> 		for (int i = 0; i < n; i++) {
> 			for (int j = i + 1; j < n; j++) {
> 				if (a[i][j]) {
> 					v[i][j] = v[j][i] = true;
> 					if (dfs(i) % 2 == 0 && dfs(j) % 2 == 0) {
> 						cnt++;
> 						a[i][j] = a[j][i] = false;
> 					} else {
> 						v[i][j] = v[j][i] = false;
> 					}
> 				}
> 			}
> 		}
> 		System.out.println(cnt);
> 	}
>
> 	public static int dfs(int cur) {
> 		int tot = 1;
> 		for (int i = 0; i < a.length; i++)
> 			if (a[cur][i] && !v[cur][i]) {
> 				v[cur][i] = v[i][cur] = true;
> 				tot += dfs(i);
> 				v[cur][i] = v[i][cur] = false;
> 			}
> 		return tot;
> 	}
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/even-tree-English-917895a0.pdf|even-tree-English-917895a0.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/even-tree-English-917895a0.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2087%20Solutions/even-tree-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 87 Solutions/even-tree-English.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2087%20Solutions/EvenTree.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 87 Solutions/EvenTree.java
