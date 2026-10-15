---
kind: "coding-problem"
title: "Surface Area (Day 61)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 61 Solutions/SurfaceArea.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Surface Area (Day 61)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Madison, is a little girl who is fond of toys. 
Her friend Mason works in a toy manufacturing factory . 
Mason has a 2D board A of size H*W with H rows and W columns. 
The board is divided into cells of size 1*1 with each cell indicated by it's coordinate (i, j). 
The cell (i,j) has an integer Aij written on it.
To create the toy Mason stacks  number of cubes of size 1*1*1 on the cell (i, j).

Given the description of the board showing the values of Aij and 
that the price of the toy is equal to the 3d surface area find the price of the toy.

NOTE: ******For description look in Testcases document.******

Input Format:
	- The first line contains two space-separated integers H and W the height and the width of the board respectively.
	- The next H lines contains W space separated integers. The jth integer in ith line denotes Aij.

Output Format:
	- Print the required answer, i.e the price of the toy, in one line.

Sample Input-1
1 1
1
Sample Output-1
6
Explanation-1
For diagram look at Testcases Doc.
So, The surface area of 1*1*1 cube is 6.

Sample Input-2
3 3
1 3 4
2 2 3
1 2 4
Sample Output-2
60

Explanation-2
For diagram look at Testcases Doc.

========= Testcases Program-1 =========
case =1
input =4 4
4 4 4 4
4 4 4 4
4 4 4 4
4 4 4 4
output =96

case =2
input =4 4
1 2 3 4
1 2 3 4
1 2 3 4
1 2 3 4
output =84

case =3
input =5 4
87 8 93 2
97 32 48 95
37 26 48 7
9 84 57 43
98 34 50 9
output =2236

case =4
input =	4 3
2 3 4
7 3 4
9 4 6
2 3 1
output =114

case =5
input =3 3
1 3 4
2 2 3
1 2 4
output =60

case =6
input =1 1
1
output =6

case =7
input =1 10
91 80 7 41 36 11 48 57 40 43
output =1276

case =8
input =10 1
51
32
28
49
28
21
98
56
99
77
output =1482

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SurfaceArea.java
> ```java
> /*
> Madison, is a little girl who is fond of toys. 
> Her friend Mason works in a toy manufacturing factory . 
> Mason has a 2D board A of size H*W with H rows and W columns. 
> The board is divided into cells of size 1*1 with each cell indicated by it's coordinate (i, j). 
> The cell (i,j) has an integer Aij written on it.
> To create the toy Mason stacks  number of cubes of size 1*1*1 on the cell (i, j).
>
> Given the description of the board showing the values of Aij and 
> that the price of the toy is equal to the 3d surface area find the price of the toy.
>
> NOTE: ******For description look in Testcases document.******
>
> Input Format:
> 	- The first line contains two space-separated integers H and W the height and the width of the board respectively.
> 	- The next H lines contains W space separated integers. The jth integer in ith line denotes Aij.
>
> Output Format:
> 	- Print the required answer, i.e the price of the toy, in one line.
>
> Sample Input-1
> 1 1
> 1
> Sample Output-1
> 6
> Explanation-1
> For diagram look at Testcases Doc.
> So, The surface area of 1*1*1 cube is 6.
>
> Sample Input-2
> 3 3
> 1 3 4
> 2 2 3
> 1 2 4
> Sample Output-2
> 60
>
> Explanation-2
> For diagram look at Testcases Doc.
>
> ========= Testcases Program-1 =========
> case =1
> input =4 4
> 4 4 4 4
> 4 4 4 4
> 4 4 4 4
> 4 4 4 4
> output =96
>
> case =2
> input =4 4
> 1 2 3 4
> 1 2 3 4
> 1 2 3 4
> 1 2 3 4
> output =84
>
> case =3
> input =5 4
> 87 8 93 2
> 97 32 48 95
> 37 26 48 7
> 9 84 57 43
> 98 34 50 9
> output =2236
>
> case =4
> input =	4 3
> 2 3 4
> 7 3 4
> 9 4 6
> 2 3 1
> output =114
>
> case =5
> input =3 3
> 1 3 4
> 2 2 3
> 1 2 4
> output =60
>
> case =6
> input =1 1
> 1
> output =6
>
> case =7
> input =1 10
> 91 80 7 41 36 11 48 57 40 43
> output =1276
>
> case =8
> input =10 1
> 51
> 32
> 28
> 49
> 28
> 21
> 98
> 56
> 99
> 77
> output =1482
>
>
> */
> import java.util.*;
> import java.math.*;
>
> public class SurfaceArea {
>
>     static int surfaceArea(int[][] A) {
>         int s = 0;
>         for (int i=0; i<A.length; i++) {
>             for (int j=0; j<A[0].length; j++) {
>                 s += A[i][j] * 4 + 2;
>                 if (i > 0) {
>                     int intersectI = A[i][j] > A[i-1][j] ? A[i-1][j] : A[i][j];
>                     s -= intersectI * 2;
>                 }
>                 
>                 if (j > 0) {
>                     int intersectJ = A[i][j] > A[i][j-1] ? A[i][j-1] : A[i][j];
>                     s -= intersectJ * 2;                    
>                 }
>             }
>         }
>         return s;
>     }
>
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         int H = in.nextInt();
>         int W = in.nextInt();
>         int[][] A = new int[H][W];
>         for(int A_i = 0; A_i < H; A_i++){
>             for(int A_j = 0; A_j < W; A_j++){
>                 A[A_i][A_j] = in.nextInt();
>             }
>         }
>         int result = surfaceArea(A);
>         System.out.println(result);
>         in.close();
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2061%20Solutions/SurfaceArea.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 61 Solutions/SurfaceArea.java
