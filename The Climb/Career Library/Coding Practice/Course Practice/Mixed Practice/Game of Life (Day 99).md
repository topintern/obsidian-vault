---
kind: "coding-problem"
title: "Game of Life (Day 99)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 99 Solutions/Game of Life - LeetCode.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 99 Solutions/GameofLife.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Game of Life (Day 99)

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

> [!example]- Reference 1 · GameofLife.java
> ```java
> import java.util.Scanner;
>
> public class GameofLife
> {
> 	public static void gameOfLife(int[][] board) {
> 		if (board == null || board.length == 0) return;
> 		int m = board.length, n = board[0].length;
>
> 		for (int i = 0; i < m; i++) {
> 			for (int j = 0; j < n; j++) {
> 				int lives = liveNeighbors(board, m, n, i, j);
>
> 				// In the beginning, every 2nd bit is 0;
> 				// So we only need to care about when will the 2nd bit become 1.
> 				if (board[i][j] == 1 && lives >= 2 && lives <= 3) {  
> 					board[i][j] = 3; // Make the 2nd bit 1: 01 ---> 11
> 				}
> 				if (board[i][j] == 0 && lives == 3) {
> 					board[i][j] = 2; // Make the 2nd bit 1: 00 ---> 10
> 				}
> 			}
> 		}
>
> 		for (int i = 0; i < m; i++) {
> 			for (int j = 0; j < n; j++) {
> 				board[i][j] >>= 1;  // Get the 2nd state.
> 			}
> 		}
> 	}
>
> 	public static int liveNeighbors(int[][] board, int m, int n, int i, int j) {
> 		int lives = 0;
> 		for (int x = Math.max(i - 1, 0); x <= Math.min(i + 1, m - 1); x++) {
> 			for (int y = Math.max(j - 1, 0); y <= Math.min(j + 1, n - 1); y++) {
> 				lives += board[x][y] & 1;
> 			}
> 		}
> 		lives -= board[i][j] & 1;
> 		return lives;
> 	}
>
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		int r=sc.nextInt();
> 		int c=sc.nextInt();
> 		int board[][]=new int[r][c];
> 		for(int i=0;i<r;i++)
> 			for(int j=0;j<c;j++)
> 				board[i][j]=sc.nextInt();
> 		gameOfLife(board);
> 		for(int i=0;i<r;i++){
> 			for(int j=0;j<c;j++){
> 				System.out.print(board[i][j]+" ");
> 			}
> 			System.out.println();
> 		}
> 				
> 	}
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/Game of Life - Leet Code-c6f1e767.pdf|Game of Life - Leet Code-c6f1e767.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/Game of Life - Leet Code-c6f1e767.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2099%20Solutions/Game%20of%20Life%20-%20LeetCode.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 99 Solutions/Game of Life - LeetCode.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2099%20Solutions/GameofLife.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 99 Solutions/GameofLife.java
