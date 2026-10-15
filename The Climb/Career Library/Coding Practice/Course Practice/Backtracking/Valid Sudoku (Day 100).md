---
kind: "coding-problem"
title: "Valid Sudoku (Day 100)"
collection: "Course Practice"
topic: "Backtracking"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 100 Solutions/Valid Sudoku - LeetCode.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 100 Solutions/ValidSudoku.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Valid Sudoku (Day 100)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Sample-1:
53..7....
6..195...
.98....6.
8...6...3
4..8.3..2
7...2...6
.6....28.
...419..5
....8..79
true

Sample-2:
83..7....
6..195...
.98....1.
8...6...3
4..8.3..1
7...2...6
.6....28.
...419..5
....8..79
false

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ValidSudoku.java
> ```java
> /*
> Sample-1:
> 53..7....
> 6..195...
> .98....6.
> 8...6...3
> 4..8.3..2
> 7...2...6
> .6....28.
> ...419..5
> ....8..79
> true
>
> Sample-2:
> 83..7....
> 6..195...
> .98....1.
> 8...6...3
> 4..8.3..1
> 7...2...6
> .6....28.
> ...419..5
> ....8..79
> false
>
> */
>
> import java.util.*;
>
> class ValidSudoku {
>    public static boolean isValidSudoku(char[][] board) {
>     for(int i = 0; i<9; i++){
>         HashSet<Character> rows = new HashSet<Character>();
>         HashSet<Character> columns = new HashSet<Character>();
>         HashSet<Character> cube = new HashSet<Character>();
>         for (int j = 0; j < 9;j++){
>             if(board[i][j]!='.' && !rows.add(board[i][j]))
>                 return false;
>             if(board[j][i]!='.' && !columns.add(board[j][i]))
>                 return false;
>             int RowIndex = 3*(i/3);
>             int ColIndex = 3*(i%3);
>             if(board[RowIndex + j/3][ColIndex + j%3]!='.' && !cube.add(board[RowIndex + j/3][ColIndex + j%3]))
>                 return false;
>         }
>     }
>     return true;
> 	}
> 	
> 	public static void main(String args[])
> 	{
> 		char board[][]=new char[9][9];
> 		Scanner sc=new Scanner(System.in);
> 		for(int i=0;i<9;i++)
> 			board[i]=sc.next().toCharArray();
> 		
> 		System.out.println(isValidSudoku(board));
> 	}
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/Valid Sudoku - Leet Code-ed60653f.pdf|Valid Sudoku - Leet Code-ed60653f.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/Valid Sudoku - Leet Code-ed60653f.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20100%20Solutions/Valid%20Sudoku%20-%20LeetCode.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 100 Solutions/Valid Sudoku - LeetCode.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20100%20Solutions/ValidSudoku.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 100 Solutions/ValidSudoku.java
