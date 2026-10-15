---
kind: "coding-problem"
title: "Word Search (Day 37)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 37 Solutions/WordSearch.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Word Search (Day 37)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

Example:

input:3
4
A B C E
S F C S
A D E E
ABCCED

output:
Given word = "ABCCED", return true.

input:3
4
A B C E
S F C S
A D E E
ABCB

output:
Given word = "ABCB", return false.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · WordSearch.txt
> ```java
> /*
>  * 
>  Given a 2D board and a word, find if the word exists in the grid.
>
> The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.
>
> Example:
>
> input:3
> 4
> A B C E
> S F C S
> A D E E
> ABCCED
>
> output:
> Given word = "ABCCED", return true.
>
> input:3
> 4
> A B C E
> S F C S
> A D E E
> ABCB
>
> output:
> Given word = "ABCB", return false.
>
>
>
>  */
>
> package Elite2020;
>
> import java.util.Scanner;
>
> public class WordSearch {
>
> 	public static boolean exist(char[][] board, String word) {
> 	    for(int i = 0; i < board.length; i++)
> 	        for(int j = 0; j < board[0].length; j++){
> 	            if(exist(board, i, j, word, 0))
> 	                return true;
> 	        }
> 	    return false;
> 	}
> 	
> 	private static boolean exist(char[][] board, int i, int j, String word, int ind){
> 	    if(ind == word.length()) return true;
> 	    if(i > board.length-1 || i <0 || j<0 || j >board[0].length-1 || board[i][j]!=word.charAt(ind))
> 	        return false;
> 	    board[i][j]='*';
> 	    boolean result =    exist(board, i-1, j, word, ind+1) ||
> 	                        exist(board, i, j-1, word, ind+1) ||
> 	                        exist(board, i, j+1, word, ind+1) ||
> 	                        exist(board, i+1, j, word, ind+1);
> 	    board[i][j] = word.charAt(ind);
> 	    return result;
> 	}
> 	
> 	public static void main(String args[] ) {
> 		 Scanner scan = new Scanner(System.in);
> 			int R=scan.nextInt();
> 			 int C=scan.nextInt();      
> 			
> 			char[][] field=new char[R][C];
> 		       for(int i=0; i<R; i++)
> 		       {
> 		           for(int j=0; j<C; j++)
> 		           {
> 		        	   field[i][j] = scan.next().charAt(0);
> 		           }
> 		       }
> 		       String word=scan.next();
> 		       System.out.println(exist(field,word));
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2037%20Solutions/WordSearch.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 37 Solutions/WordSearch.txt
