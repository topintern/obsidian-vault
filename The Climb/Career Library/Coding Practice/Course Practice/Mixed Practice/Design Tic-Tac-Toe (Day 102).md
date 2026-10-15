---
kind: "coding-problem"
title: "Design Tic-Tac-Toe (Day 102)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 102 Solutions/Design Tic-Tac-Toe - LeetCode.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 102 Solutions/TicTacToe.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Design Tic-Tac-Toe (Day 102)

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

> [!example]- Reference 1 · TicTacToe.txt
> ```java
> import java.util.*;
>
> public class TicTacToe {
> 	private int[] rows;
> 	private int[] cols;
> 	private int diagonal;
> 	private int antiDiagonal;
>
> 	/** Initialize your data structure here. */
> 	public TicTacToe(int n) {
> 		rows = new int[n];
> 		cols = new int[n];
> 	}
>
> 	/** Player {player} makes a move at ({row}, {col}).
> 		@param row The row of the board.
> 		@param col The column of the board.
> 		@param player The player, can be either 1 or 2.
> 		@return The current winning condition, can be either:
> 				0: No one wins.
> 				1: Player 1 wins.
> 				2: Player 2 wins. */
> 	public int move(int row, int col, int player) {
> 		int toAdd = player == 1 ? 1 : -1;
> 		
> 		rows[row] += toAdd;
> 		cols[col] += toAdd;
> 		if (row == col)
> 		{
> 			diagonal += toAdd;
> 		}
> 		
> 		if (col == (cols.length - row - 1))
> 		{
> 			antiDiagonal += toAdd;
> 		}
> 		
> 		int size = rows.length;
> 		if (Math.abs(rows[row]) == size || Math.abs(cols[col]) == size || Math.abs(diagonal) == size  || Math.abs(antiDiagonal) == size)
> 		{
> 			return player;
> 		}
>     
> 		return 0;
> 	}
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		int n=sc.nextInt();
> 		TicTacToe  t=new TicTacToe(n);
> 		int winner=0;
> 		for(int i=0;i<n*n;i++)
> 		{
> 			winner=t.move(sc.nextInt(), sc.nextInt(), sc.nextInt());
> 			if(winner==1 || winner==2)
> 			break;
> 		}
> 		if(winner != 0)
> 			System.out.println("Player-"+winner);
> 		else
> 			System.out.println("Tie");
> 	}
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/Design Tic-Tac-Toe - Leet Code-7e4f3311.pdf|Design Tic-Tac-Toe - Leet Code-7e4f3311.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/Design Tic-Tac-Toe - Leet Code-7e4f3311.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20102%20Solutions/Design%20Tic-Tac-Toe%20-%20LeetCode.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 102 Solutions/Design Tic-Tac-Toe - LeetCode.pdf
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20102%20Solutions/TicTacToe.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 102 Solutions/TicTacToe.txt
