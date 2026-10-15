---
kind: "coding-problem"
title: "Walls and Gates (Day 99)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 99 Solutions/Walls and Gates - LeetCode.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 99 Solutions/WallsandGates.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Walls and Gates (Day 99)

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

> [!example]- Reference 1 · WallsandGates.java
> ```java
> import java.util.*;
>
> public class WallsandGates {
>     public static void wallsAndGates(int[][] rooms) {
>         if (rooms.length == 0 || rooms[0].length == 0) return;
>         Queue<int[]> queue = new LinkedList<>();
>         for (int i = 0; i < rooms.length; i++) {
>             for (int j = 0; j < rooms[0].length; j++) {
>                 if (rooms[i][j] == 0) queue.add(new int[]{i, j});
>             }
>         }
>         while (!queue.isEmpty()) {
>             int[] top = queue.remove();
>             int row = top[0], col = top[1];
>             if (row > 0 && rooms[row - 1][col] == -2) {			//INF replaced with -2
>                 rooms[row - 1][col] = rooms[row][col] + 1;
>                 queue.add(new int[]{row - 1, col});
>             }
>             if (row < rooms.length - 1 && rooms[row + 1][col] == -2) {
>                 rooms[row + 1][col] = rooms[row][col] + 1;
>                 queue.add(new int[]{row + 1, col});
>             }
>             if (col > 0 && rooms[row][col - 1] == -2) {
>                 rooms[row][col - 1] = rooms[row][col] + 1;
>                 queue.add(new int[]{row, col - 1});
>             }
>             if (col < rooms[0].length - 1 && rooms[row][col + 1] == -2) {
>                 rooms[row][col + 1] = rooms[row][col] + 1;
>                 queue.add(new int[]{row, col + 1});
>             }
>         }
>     }
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		int r=sc.nextInt();
> 		int c=sc.nextInt();
> 		int rooms[][]=new int[r][c];
> 		for(int i=0;i<r;i++)
> 			for(int j=0;j<c;j++)
> 				rooms[i][j]=sc.nextInt();
> 		wallsAndGates(rooms);
> 		for(int i=0;i<r;i++){
> 			for(int j=0;j<c;j++){
> 				System.out.print(rooms[i][j]+" ");
> 			}
> 			System.out.println();
> 		}		
> 	}
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/Walls and Gates - Leet Code-4637a407.pdf|Walls and Gates - Leet Code-4637a407.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/Walls and Gates - Leet Code-4637a407.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2099%20Solutions/Walls%20and%20Gates%20-%20LeetCode.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 99 Solutions/Walls and Gates - LeetCode.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2099%20Solutions/WallsandGates.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 99 Solutions/WallsandGates.java
