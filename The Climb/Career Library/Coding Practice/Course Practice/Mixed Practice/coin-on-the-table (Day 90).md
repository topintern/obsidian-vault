---
kind: "coding-problem"
title: "coin-on-the-table (Day 90)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 90 Solutions/coin-on-the-table-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 90 Solutions/CoinOnTheTable.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# coin-on-the-table (Day 90)

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

> [!example]- Reference 1 · CoinOnTheTable.java
> ```java
> import java.util.Scanner;
>
> public class CoinOnTheTable {
>
>     public static void main(String[] args) {
>         Scanner cin = new Scanner(System.in);
>
>         int n = cin.nextInt();
>         int m = cin.nextInt();
>         int K = cin.nextInt();
>         int x = 0, y = 0;
>         char a[][] = new char[n][];
>         for (int i=0; i<n; i++) {
>             a[i] = cin.next().toCharArray();
>             for (int j=0; j<m; j++)
>                 if (a[i][j] == '*') {
>                     x = i;
>                     y = j;
>                 }
>         }
>
>
>         int f[][][] = new int[K + 1][n][m];
>         int ans = 1 << 29;
>         for (int k=0; k<=K; k++)
>             for (int i=0; i<n; i++)
>                 for (int j=0; j<m; j++) 
>                     if (k == 0) f[k][i][j] = i == 0 && j == 0 ? 0 : 1 << 29;
>                     else {
>                         int res = 1 << 29;
>                         if (i > 0)     res = Math.min(res, f[k - 1][i - 1][j] + (a[i - 1][j] == 'D' ? 0 : 1));
>                         if (i < n - 1) res = Math.min(res, f[k - 1][i + 1][j] + (a[i + 1][j] == 'U' ? 0 : 1));
>                         if (j > 0)     res = Math.min(res, f[k - 1][i][j - 1] + (a[i][j - 1] == 'R' ? 0 : 1));
>                         if (j < m - 1) res = Math.min(res, f[k - 1][i][j + 1] + (a[i][j + 1] == 'L' ? 0 : 1));
>
>                         f[k][i][j] = res;
>                     }
>
>         for (int k=0; k<=K; k++)
>             ans = Math.min(ans, f[k][x][y]);
>
>         if (ans < (1 << 29)) System.out.println(ans);
>         else System.out.println(-1);
>
>         cin.close();
>     }
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/coin-on-the-table-English-542445e3.pdf|coin-on-the-table-English-542445e3.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/coin-on-the-table-English-542445e3.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2090%20Solutions/coin-on-the-table-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 90 Solutions/coin-on-the-table-English.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2090%20Solutions/CoinOnTheTable.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 90 Solutions/CoinOnTheTable.java
