---
kind: "coding-problem"
title: "Magic Square (Day 63)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 63 Solutions/MagicSquare.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Magic Square (Day 63)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

We define a magic square to be an n*n matrix of distinct positive integers from 1 to n*n 
where the sum of any row, column, or diagonal of length n is always 
equal to the same number: the magic constant.

You will be given a 3*3 matrix s of integers in the inclusive range [1-9]. 
We can convert any digit 'a' to any other digit 'b' in the range [1-9] at cost of |a-b|. 
Given s, convert it into a magic square at minimal cost. 
Print this cost on a new line.

Note: The resulting magic square must contain distinct integers in the inclusive range [1-9].

For example, we start with the following matrix s:
5 3 4
1 5 8
6 4 2
We can convert it to the following magic square:
8 3 4
1 5 9
6 7 2
This took three replacements at a cost of |5-8| + |8-9| + |4-7| =7.

Input Format:
Each of the lines contains three space-separated integers of row s[i], 1<=s[i]<=9 


### Output Format

Print an integer denoting the minimum cost of turning matrix s into a magic square.

Sample Input1:
4 9 2
3 5 7
8 1 5
Sample Output1:
1
Explanation1:
If we change the bottom right value, s[2][2], from 5 to 6 at a cost of |5-6|=1, 
s becomes a magic square at the minimum possible cost.

Sample Input2:
4 8 2
4 5 7
6 1 6
Sample Output2:
4

Explanation2:
Using 0-based indexing, if we make
-> s[0][1] at a cost of |9-8|=1 
-> s[1][0] at a cost of |3-4|=1
-> s[2][0] at a cost of |8-6|=2
then the total cost will be 1+1+2=4.


========= Testcases Program-3 =========
case =1
input =4 9 2
3 5 7
8 1 5
output =1

case =2
input =4 5 8
2 4 1
1 9 7
output =14

case =3
input =2 9 8
4 2 7
5 6 7
output =21

case =4
input =4 4 7
3 1 5
1 7 9
output =20

case =5
input =2 2 7
8 6 4
1 2 9
output =16

case =6
input =7 6 5
7 2 8
5 3 4
output =18

case =7
input =4 9 2
3 5 7
8 1 6
output =0

case =8
input =1 3 8
6 4 1
2 6 5
output =9

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MagicSquare.java
> ```java
> /*
> We define a magic square to be an n*n matrix of distinct positive integers from 1 to n*n 
> where the sum of any row, column, or diagonal of length n is always 
> equal to the same number: the magic constant.
>
> You will be given a 3*3 matrix s of integers in the inclusive range [1-9]. 
> We can convert any digit 'a' to any other digit 'b' in the range [1-9] at cost of |a-b|. 
> Given s, convert it into a magic square at minimal cost. 
> Print this cost on a new line.
>
> Note: The resulting magic square must contain distinct integers in the inclusive range [1-9].
>
> For example, we start with the following matrix s:
> 5 3 4
> 1 5 8
> 6 4 2
> We can convert it to the following magic square:
> 8 3 4
> 1 5 9
> 6 7 2
> This took three replacements at a cost of |5-8| + |8-9| + |4-7| =7.
>
> Input Format:
> Each of the lines contains three space-separated integers of row s[i], 1<=s[i]<=9 
>
> Output Format
> Print an integer denoting the minimum cost of turning matrix s into a magic square.
>
> Sample Input1:
> 4 9 2
> 3 5 7
> 8 1 5
> Sample Output1:
> 1
> Explanation1:
> If we change the bottom right value, s[2][2], from 5 to 6 at a cost of |5-6|=1, 
> s becomes a magic square at the minimum possible cost.
>
> Sample Input2:
> 4 8 2
> 4 5 7
> 6 1 6
> Sample Output2:
> 4
>
> Explanation2:
> Using 0-based indexing, if we make
> -> s[0][1] at a cost of |9-8|=1 
> -> s[1][0] at a cost of |3-4|=1
> -> s[2][0] at a cost of |8-6|=2
> then the total cost will be 1+1+2=4.
>
>
> ========= Testcases Program-3 =========
> case =1
> input =4 9 2
> 3 5 7
> 8 1 5
> output =1
>
> case =2
> input =4 5 8
> 2 4 1
> 1 9 7
> output =14
>
> case =3
> input =2 9 8
> 4 2 7
> 5 6 7
> output =21
>
> case =4
> input =4 4 7
> 3 1 5
> 1 7 9
> output =20
>
> case =5
> input =2 2 7
> 8 6 4
> 1 2 9
> output =16
>
> case =6
> input =7 6 5
> 7 2 8
> 5 3 4
> output =18
>
> case =7
> input =4 9 2
> 3 5 7
> 8 1 6
> output =0
>
> case =8
> input =1 3 8
> 6 4 1
> 2 6 5
> output =9
>
> */
>
> import java.io.*;
> import java.util.*;
> public class MagicSquare {
>     public static int diff(int[][] s1,int[][] s2){
>         int d=0;
>         for(int i=0;i<3;i++)
>             for(int j=0;j<3;j++)
>                 d+=Math.abs(s1[i][j]-s2[i][j]);
>         return d;
>     }
>     public static void main(String[] args) {
>         Scanner sc=new Scanner(System.in);
>         int s[][]=new int[3][3];
>         for(int i=0;i<3;i++)
>            for(int j=0;j<3;j++)
>            {s[i][j]=sc.nextInt();}
>         int a[][]={{2,7,6},{9,5,1},{4,3,8}};
>         int b[][]={{2,9,4},{7,5,3},{6,1,8}};
>         int c[][]={{4,3,8},{9,5,1},{2,7,6}};
>         int d[][]={{4,9,2},{3,5,7},{8,1,6}};
>         int e[][]={{6,1,8},{7,5,3},{2,9,4}};
>         int f[][]={{6,7,2},{1,5,9},{8,3,4}};
>         int g[][]={{8,1,6},{3,5,7},{4,9,2}};
>         int h[][]={{8,3,4},{1,5,9},{6,7,2}};
>         ArrayList<int[][]> val=new ArrayList<>();
>         int res=Integer.MAX_VALUE;
>         val.add(a);val.add(b);val.add(c);val.add(d);val.add(e);val.add(f);val.add(g);val.add(h);
>         for(int[][] x:val){
>             res=Math.min(res, diff(x, s));
>         }
>         System.out.println(res);
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2063%20Solutions/MagicSquare.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 63 Solutions/MagicSquare.java
