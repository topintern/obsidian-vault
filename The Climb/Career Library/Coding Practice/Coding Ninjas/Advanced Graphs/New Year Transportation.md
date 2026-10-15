---
kind: "coding-problem"
title: "New Year Transportation"
collection: "Coding Ninjas"
topic: "Advanced Graphs"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/5.Adv graphs/new yr transport q.txt","CODING RESOURCES/coding ninjas/5.Adv graphs/new yr transport s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# New Year Transportation

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

New Year Transportation
New Year is coming in Line World! In this world, there are n cells numbered by integers from 1 to n, as a 1?×?n board. People live in cells. However, it was hard to move between distinct cells, because of the difficulty of escaping the cell. People wanted to meet people who live in other cells.

 So, user tncks0121 has made a transportation system to move between these cells, to celebrate the New Year. First, he thought of n?-?1 positive integers a1,?a2,?...,?an?-?1. For every integer i where 1?=?i?=?n?-?1 the condition 1?=?ai?=?n?-?i holds. Next, he made n?-?1 portals, numbered by integers from 1 to n?-?1. The i-th (1?=?i?=?n?-?1) portal connects cell i and cell (i?+?ai), and one can travel from cell i to cell (i?+?ai) using the i-th portal. Unfortunately, one cannot use the portal backwards, which means one cannot move from cell (i?+?ai) to cell i using the i-th portal. It is easy to see that because of condition 1?=?ai?=?n?-?i one can't leave the Line World using portals.

Currently, I am standing at cell 1, and I want to go to cell t. However, I don't know whether it is possible to go there. Please determine whether I can go to cell t by only using the construted transportation system.

### Input

The first line contains two space-separated integers n (3?=?n?=?3?×?104) and t (2?=?t?=?n) — the number of cells, and the index of the cell which I want to go to.

The second line contains n?-?1 space-separated integers a1,?a2,?...,?an?-?1 (1?=?ai?=?n?-?i). It is guaranteed, that using the given transportation system, one cannot leave the Line World.

### Output

If I can go to cell t using the transportation system, print "YES". Otherwise, print "NO".

### Sample input 1

```text
8 4
1 2 1 2 1 2 1
```

### Sample output 1

```text
YES
```

### Sample input 2

```text
8 5 1 2 1 2 1 1 1
```

### Sample output 2

```text
NO
```

### Note

In the first sample, the visited cells are: 1,?2,?4; so we can successfully visit the cell 4.

In the second sample, the possible cells to visit are: 1,?2,?4,?6,?7,?8; so we can't visit the cell 5, which we want to visit.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · new yr transport s.txt
> ```java
> import java.util.Scanner;
>
> public class solution {
>
> 	public static void main(String[] args) {
> 		// TODO Auto-generated method stub
> 		Scanner sc = new Scanner(System.in);
> 		int cn = sc.nextInt();
> 		int des = sc.nextInt();
> 		
> 		int[] cell = new int[cn-1];
> 		for(int i=0;i<cn-1;i++){
> 			 cell[i] = sc.nextInt();
> 			}
> 		int sum = 0;
> 		while(sum<des-1){
> 			sum +=cell[sum];
> 		}
> 		if(sum==des-1)
> 			System.out.println("YES");
> 		else
> 			System.out.println("NO");
> 		}
> 	}
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/5.Adv%20graphs/new%20yr%20transport%20q.txt) · CODING RESOURCES/coding ninjas/5.Adv graphs/new yr transport q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/5.Adv%20graphs/new%20yr%20transport%20s.txt) · CODING RESOURCES/coding ninjas/5.Adv graphs/new yr transport s.txt
