---
kind: "coding-problem"
title: "Sudoku"
collection: "Coding Ninjas"
topic: "Backtracking"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/2.backtrack/soduku q.txt","CODING RESOURCES/coding ninjas/2.backtrack/soduku s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Sudoku

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Given a 9*9 sudoku board, in which some entries are filled and others are 0 (0 indicates that the cell is empty), you need to find out whether the Sudoku puzzle can be solved or not i.e. return true or false.

### Input Format

9 Lines where ith line contains ith row elements separated by space

### Output Format

 true or false

### Sample Input

```text
9 0 0 0 2 0 7 5 0 
6 0 0 0 5 0 0 4 0 
0 2 0 4 0 0 0 1 0 
2 0 8 0 0 0 0 0 0 
0 7 0 5 0 9 0 6 0 
0 0 0 0 0 0 4 0 1 
0 1 0 0 0 5 0 8 0 
0 9 0 0 7 0 0 0 4 
0 8 2 0 4 0 0 0 6
```

### Sample Output

```text
true
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · soduku s.txt
> ```text
> #!/usr/bin/env python
> # coding: utf-8
>
> # In[6]:
>
>
> def presentInRow(board,row,num):
>     for j in range(9):
>         if board[row][j] == num:
>             return True
>     return False
>
> def presentInCol(board,col,num):
>     for j in range(9):
>         if board[j][col] == num:
>             return True
>     return False
>
> def presentInBox(board,row,col,num):
>     for i in range(row,row+3):
>         for j in range(col,col+3):
>             if board[i][j] == num:
>                 return True
>     return False
>
> def isPossible(board,row,col,num):
>     if(presentInRow(board,row,num)):
>         return False
>     if(presentInCol(board,col,num)):
>         return False
>     if(presentInBox(board,row-(row%3),col-(col%3),num)):
>         return False
>     return True
>
>     
> def solveSudoku(board):
>     
>     row = -1
>     col = -1
>     flag = False
>     for i in range(9):
>         for j in range(9):
>             if board[i][j] is 0:
>                 row = i
>                 col = j
>                 flag = True
>                 break
>         if flag is True:
>             break
>     if row == -1:
>         return True
>     for num in range(1,10):
>         if(isPossible(board,row,col,num)):
>             board[row][col] = num
>             if(solveSudoku(board) is True):
>                 return True
>             board[row][col] = 0
>             
>     return False
>
> board = [[ int(ele) for ele in input().split() ]for i in range(9)]
> ans = solveSudoku(board)
> if ans is True:
>     print('true')
> else:
>     print('false')
>
>
> # In[ ]:
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/2.backtrack/soduku%20q.txt) · CODING RESOURCES/coding ninjas/2.backtrack/soduku q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/2.backtrack/soduku%20s.txt) · CODING RESOURCES/coding ninjas/2.backtrack/soduku s.txt
