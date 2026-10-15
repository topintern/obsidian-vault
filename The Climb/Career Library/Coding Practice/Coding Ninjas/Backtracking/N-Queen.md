---
kind: "coding-problem"
title: "N-Queen"
collection: "Coding Ninjas"
topic: "Backtracking"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/2.backtrack/backtack s.txt","CODING RESOURCES/coding ninjas/2.backtrack/backtrack q.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# N-Queen

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

You are given N, and for a given N x N chessboard, find a way to place N queens such that no queen can attack any other queen on the chess board. A queen can be killed when it lies in the same row, or same column, or the same diagonal of any of the other queens. You have to print all such configurations.

### Input Format

Line 1 : Integer N

### Output Format

One Line for every board configuration. 
Every line will have N*N board elements printed row wise and are separated by space
Note : Don't print anything if there isn't any valid configuration.

### Constraints

1<=N<=10

### Sample Input 1

```text
4
```

### Sample Output 1

```text
0 1 0 0 0 0 0 1 1 0 0 0 0 0 1 0 
0 0 1 0 1 0 0 0 0 0 0 1 0 1 0 0 
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · backtack s.txt
> ```cpp
> #include<vector>
> class RectangularVectors
> {
> public:
> 	static std::vector<std::vector<int>> RectangularIntVector(int size1, int size2)
> 	{
> 		std::vector<std::vector<int>> newVector(size1);
> 		for (int vector1 = 0; vector1 < size1; vector1++)
> 		{
> 			newVector[vector1] = std::vector<int>(size2);
> 		}
>
> 		return newVector;
> 	}
> };
> bool isBoardSafe(std::vector<std::vector<int>> &board, int row, int col)
> {
> 		
> 		int n = board.size();
> 		for (int i = row - 1, j = col - 1 ; i >= 0 && j >= 0; i--,j--)
> 		{
> 			if (board[i][j] == 1)
> 			{
> 				return false;
> 			}
> 		}
> 		for (int i = row + 1, j = col + 1 ; i < n && j < n ; i++,j++)
> 		{
> 			if (board[i][j] == 1)
> 			{
> 				return false;
> 			}
> 		}
>
> 		for (int i = row - 1, j = col + 1 ; i >= 0 && j < n; i--,j++)
> 		{
> 			if (board[i][j] == 1)
> 			{
> 				return false;
> 			}
> 		}
>
> 		for (int i = row + 1, j = col - 1 ; i < n && j >= 0; i++,j--)
> 		{
> 			if (board[i][j] == 1)
> 			{
> 				return false;
> 			}
> 		}
>
> 		for (int i = row - 1; i >= 0; i--)
> 		{
> 			if (board[i][col] == 1)
> 			{
> 				return false;
> 			}
> 		}
>
> 		for (int i = row + 1; i < n; i++)
> 		{
> 			if (board[i][col] == 1)
> 			{
> 				return false;
> 			}
> 		}
>
> 		return true;
>
> }
>
> void placeQueen(std::vector<std::vector<int>> &board, int row, int n)
> {
> 		if (row == n)
> 		{
> 				for (int i = 0; i < n; i++)
> 				{
> 					for (int j = 0; j < n; j++)
> 					{
> 						std::cout << board[i][j] << " ";
> 					}
> 				}
> 				std::cout <<std::endl;
> 		}
> 		for (int j = 0; j < n; j++)
> 		{
> 			if (isBoardSafe(board,row, j))
> 			{
> 				board[row][j] = 1;
> 				placeQueen(board, row + 1, n);
> 				board[row][j] = 0;
> 			}
> 		}
> }
>
> void placeNQueens(int n){
>
> 	std::vector<std::vector<int>> board = RectangularVectors::RectangularIntVector(n, n);
> 			placeQueen(board, 0, n);
>
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/2.backtrack/backtack%20s.txt) · CODING RESOURCES/coding ninjas/2.backtrack/backtack s.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/2.backtrack/backtrack%20q.txt) · CODING RESOURCES/coding ninjas/2.backtrack/backtrack q.txt
