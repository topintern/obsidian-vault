---
kind: "coding-problem"
title: "Connected Cells (Day 87)"
collection: "Course Practice"
topic: "Graphs"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 87 Solutions/ConnectedCells.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Connected Cells (Day 87)

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

> [!example]- Reference 1 · ConnectedCells.java
> ```java
> import java.io.*;
> import java.util.*;
> import java.text.*;
> import java.math.*;
> import java.util.regex.*;
>
> public class ConnectedCells {
>     static boolean[][] visited;
>     static int[][] matrix;
>     private static void solve(int[][] m) {
>         int biggest = 0;
>         matrix = m;
>         visited = new boolean[m.length][m[0].length];
>         for (int i = 0; i < visited.length; i++) {
>             for (int j = 0; j < visited[i].length; j++) {
>                 if (!visited[i][j]) {
>                     int area = dfs(i, j);
>                     if (area > biggest) biggest = area;
>                 }
>             }
>         }
>         System.out.println(biggest);
>     }
>     private static int dfs(int i, int j) {
>         if (i < 0 || i >= visited.length || j < 0 || j >= visited[0].length) return 0;
>         if (matrix[i][j] == 0) return 0;
>         if (visited[i][j]) return 0;
>         visited[i][j] = true;
>         int[][] neighbors = {{i-1, j-1}, {i-1,j}, {i-1, j+1}, {i, j-1}, {i, j+1}, {i+1, j-1}, {i+1,j}, {i+1,j+1}};
>         int result = 1;
>         for (int n = 0; n < neighbors.length; n++) {
>             result += dfs(neighbors[n][0], neighbors[n][1]);
>         }
>         return result;
>     }
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         int m = in.nextInt();
>         int n = in.nextInt();
>         int[][] board = new int[m][n];
>         for (int i = 0; i < m; i++) {
>             for (int j = 0; j < n; j++) {
>                 board[i][j] = in.nextInt();
>             }
>         }
>         solve(board);
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2087%20Solutions/ConnectedCells.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 87 Solutions/ConnectedCells.java
