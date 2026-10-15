---
kind: "coding-problem"
title: "bomber-man (Day 75)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 75 Solutions/bomber-man-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 75 Solutions/Bomberman.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# bomber-man (Day 75)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Refer to Editorial For Different Input and step by step Explanation.


### Sample input :


3 3 3
...
.O.
...


### Sample output :


O.O
...
O.O




### Sample input 

6 7 3
.......
...O...
....O..
.......
OO.....
OO.....


### Sample output :


OOO.OOO
OO...OO
OOO...O
..OO.OO
...OOOO
...OOOO



### Explanation :


The initial state of the grid is:

.......
...O...
....O..
.......
OO.....
OO.....

Bomberman spends the first second doing nothing, so this is the state after 1 second:

.......
...O...
....O..
.......
OO.....
OO.....

Bomberman plants bombs in all the empty cells during his second second, so this is the state after 2 seconds:

OOOOOOO
OOOOOOO
OOOOOOO
OOOOOOO
OOOOOOO
OOOOOOO

In his third second, Bomberman sits back and watches all the bombs he planted 3 seconds ago detonate. This is the final state after  seconds:

OOO.OOO
OO...OO
OOO...O
..OO.OO
...OOOO
...OOOO

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Bomberman.java
> ```java
> /*
>
> Refer to Editorial For Different Input and step by step Explanation.
>
> Sample input :
>
> 3 3 3
> ...
> .O.
> ...
>
> Sample output :
>
> O.O
> ...
> O.O
>
>
>
> Sample input :
> 6 7 3
> .......
> ...O...
> ....O..
> .......
> OO.....
> OO.....
>
> Sample output :
>
> OOO.OOO
> OO...OO
> OOO...O
> ..OO.OO
> ...OOOO
> ...OOOO
>
>
> Explanation :
>
> The initial state of the grid is:
>
> .......
> ...O...
> ....O..
> .......
> OO.....
> OO.....
>
> Bomberman spends the first second doing nothing, so this is the state after 1 second:
>
> .......
> ...O...
> ....O..
> .......
> OO.....
> OO.....
>
> Bomberman plants bombs in all the empty cells during his second second, so this is the state after 2 seconds:
>
> OOOOOOO
> OOOOOOO
> OOOOOOO
> OOOOOOO
> OOOOOOO
> OOOOOOO
>
> In his third second, Bomberman sits back and watches all the bombs he planted 3 seconds ago detonate. This is the final state after  seconds:
>
> OOO.OOO
> OO...OO
> OOO...O
> ..OO.OO
> ...OOOO
> ...OOOO
>
>
>
> */
>
>
> import java.io.*;
> import java.util.*;
> import java.text.*;
> import java.math.*;
> import java.util.regex.*;
>
> public class Bomberman {
>
>     public static void toComplement(char[][] grid, int r, int c){
>         for(int i=0; i<r; i++){
>             for(int j=0; j<c; j++){
>                 if(grid[i][j]=='O'){
>                     if(i-1>=0 && grid[i-1][j]!='O') grid[i-1][j]='*';
>                     if(i+1<r && grid[i+1][j]!='O') grid[i+1][j]='*';
>                     if(j-1>=0 && grid[i][j-1]!='O') grid[i][j-1]='*';
>                     if(j+1<c && grid[i][j+1]!='O') grid[i][j+1]='*';
>                 }
>             }
>         }
>         for(int i=0; i<r; i++){
>             for(int j=0; j<c; j++){
>                 if(grid[i][j]=='.') grid[i][j]='O';
>                 else if(grid[i][j]=='O' || grid[i][j]=='*') grid[i][j]='.';
>             }
>         }
>     }
>     
>     public static void toFull(char[][] grid, int r, int c){
>         for(int i=0; i<r; i++){
>             for(int j=0; j<c; j++){
>                 grid[i][j]='O';
>             }
>         }
>     }
>     
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         int r = in.nextInt();
>         int c = in.nextInt();
>         int n = in.nextInt();
>         in.nextLine();
>         char[][] grid = new char[r][c];
>         for(int i=0; i<r; i++){
>             grid[i] = in.nextLine().toCharArray();
>         }
>         if(n%2 == 0) toFull(grid, r, c);
>         if(n%4 == 3) toComplement(grid, r, c);
>         if(n%4 == 1 && n!=1){
>             toComplement(grid, r, c);
>             toComplement(grid, r, c);
>         }
> 		System.out.println("----------------------------");
>         for(int i=0; i<r; i++){
>             for(int j=0; j<c; j++){
>                 System.out.print(grid[i][j]);
>             }
>             System.out.println();
>         }
>     }
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/bomber-man-English-04b01678.pdf|bomber-man-English-04b01678.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/bomber-man-English-04b01678.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2075%20Solutions/bomber-man-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 75 Solutions/bomber-man-English.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2075%20Solutions/Bomberman.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 75 Solutions/Bomberman.java
