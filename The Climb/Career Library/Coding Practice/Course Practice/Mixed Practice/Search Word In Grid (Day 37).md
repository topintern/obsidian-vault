---
kind: "coding-problem"
title: "Search Word In Grid (Day 37)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 37 Solutions/SearchWordInGrid.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Search Word In Grid (Day 37)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Search a Word in a 2D Grid of characters
Given a 2D grid of characters and a word, find all occurrences of given word in grid. A word can be matched in all 8 directions at any point. Word is said be found in a direction if all characters match in this direction (not in zig-zag form).

The 8 directions are, Horizontally Left, Horizontally Right, Vertically Up and 4 Diagonal directions.

Input:4
4
T E X T
T E T T
E X I T
T E L L
LIE

Output: 3 3

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SearchWordInGrid.txt
> ```java
> /*
>  * 
>  Search a Word in a 2D Grid of characters
> Given a 2D grid of characters and a word, find all occurrences of given word in grid. A word can be matched in all 8 directions at any point. Word is said be found in a direction if all characters match in this direction (not in zig-zag form).
>
> The 8 directions are, Horizontally Left, Horizontally Right, Vertically Up and 4 Diagonal directions.
>
> Input:4
> 4
> T E X T
> T E T T
> E X I T
> T E L L
> LIE
>
> Output: 3 3
>         
>         
>         
>
>  */
>
> package Elite2020;
> import java.io.*; 
> import java.util.*; 
> public class SearchWordInGrid {
> 	
> 	// Java program to search a word in a 2D grid 
>
> 	
> 	  
> 	    // Rows and columns in given grid 
> 	    static int R, C; 
> 	  
> 	    // For searching in all 8 direction  
> 	    static int[] x = { -1, -1, -1, 0, 0, 1, 1, 1 };  
> 	    static int[] y = { -1, 0, 1, -1, 1, -1, 0, 1 };  
> 	  
> 	    // This function searches in all 8-direction from point  
> 	    // (row, col) in grid[][]  
> 	    static boolean search2D(char[][] grid, int row, 
> 	                            int col, String word) 
> 	    { 
> 	            // If first character of word doesn't match with  
> 	            // given starting point in grid.  
> 	            if (grid[row][col] != word.charAt(0)) 
> 	                return false; 
> 	  
> 	            int len = word.length(); 
> 	              
> 	            // Search word in all 8 directions 
> 	            // starting from (row,col) 
> 	            for (int dir = 0; dir < 8; dir++) 
> 	            { 
> 	                // Initialize starting point 
> 	                // for current direction  
> 	                int k, rd = row + x[dir], cd = col + y[dir]; 
> 	  
> 	                // First character is already checked,  
> 	                //  match remaining characters 
> 	                for (k = 1; k < len; k++) 
> 	                { 
> 	                    // If out of bound break  
> 	                    if (rd >= R || rd < 0 || cd >= C || cd < 0) 
> 	                        break; 
> 	  
> 	                    // If not matched, break  
> 	                    if (grid[rd][cd] != word.charAt(k)) 
> 	                        break; 
> 	  
> 	                    // Moving in particular direction  
> 	                    rd += x[dir]; 
> 	                    cd += y[dir]; 
> 	                }  
> 	  
> 	                // If all character matched, then value of must  
> 	                // be equal to length of word 
> 	                if (k == len) 
> 	                    return true;  
> 	            } 
> 	        return false; 
> 	    } 
> 	  
> 	    // Searches given word in a given 
> 	    // matrix in all 8 directions 
> 	    static void patternSearch(char[][] grid, String word) 
> 	    { 
> 	            // Consider every point as starting  
> 	            // point and search given word  
> 	            for (int row = 0; row < R; row++)  
> 	            { 
> 	                for (int col = 0; col < C; col++)  
> 	                { 
> 	                    if (search2D(grid, row, col, word)) 
> 	                        System.out.println(row+" "+col); 
> 	                } 
> 	            } 
> 	    } 
> 	  
> 	    public static void main(String args[] ) {
> 			 Scanner scan = new Scanner(System.in);
> 				 R=scan.nextInt();
> 				 C=scan.nextInt();      
> 				
> 				char[][] field=new char[R][C];
> 			       for(int i=0; i<R; i++)
> 			       {
> 			           for(int j=0; j<C; j++)
> 			           {
> 			        	   field[i][j] = scan.next().charAt(0);
> 			           }
> 			       }
> 			       String word=scan.next();
> 			       patternSearch(field,word);
> 		}
> 	  
>
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2037%20Solutions/SearchWordInGrid.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 37 Solutions/SearchWordInGrid.txt
