---
kind: "coding-problem"
title: "Rescue People (Day 111)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 111 Solutions/RescuePeople.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Rescue People (Day 111)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

A forest is represented as a square grid consist of 0's an 1's only.
Few people stuck in the forest, where 1's are indicate people, and 0's are indicate as trees. 
A person cannot move from the tree.

You want to save people, a person can be saved, if he/she connected to other person 
who is at the boundary of forest
If 'a' is connected to 'b' and 'b' is connected to 'c',
then you can consider that 'a' is also connected to 'c'. They can connected in 4 directions only. 
(up, right, left and down)

You need to find out the number of persons, who cannot be saved from thegiven forest grid.


Input Format:
-------------
Line-1 -> An integer N, size of the grid N*N
next N lines -> N space separated integers(0's and 1's)

Output Format:
--------------
Print an integer as your result


Sample Input-1:
---------------
5
0 0 1 1 0
1 0 0 1 0
0 0 1 0 0
0 1 1 0 1
1 0 0 1 0

Sample Output-1:
----------------
3


### Explanation

------------
In the given grid, 1's at (2,2), (3,1), (3,2) positions are not connected to the boundary
So, number of people cannot be saved are 3

Sample Input-2:
---------------
5
0 0 1 1 0
1 0 0 1 0
0 0 1 1 0
0 1 1 0 1
1 0 0 1 0

Sample Output-2:
----------------
0


### Explanation

------------
In the given grid, each 1 is either at the boundary or connceted to 1 at boundary.
So, number of people cannot be saved are '0'

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · RescuePeople.txt
> ```java
> /*
> A forest is represented as a square grid consist of 0's an 1's only.
> Few people stuck in the forest, where 1's are indicate people, and 0's are indicate as trees. 
> A person cannot move from the tree.
>
> You want to save people, a person can be saved, if he/she connected to other person 
> who is at the boundary of forest
> If 'a' is connected to 'b' and 'b' is connected to 'c',
> then you can consider that 'a' is also connected to 'c'. They can connected in 4 directions only. 
> (up, right, left and down)
>
> You need to find out the number of persons, who cannot be saved from thegiven forest grid.
>
>
> Input Format:
> -------------
> Line-1 -> An integer N, size of the grid N*N
> next N lines -> N space separated integers(0's and 1's)
>
> Output Format:
> --------------
> Print an integer as your result
>
>
> Sample Input-1:
> ---------------
> 5
> 0 0 1 1 0
> 1 0 0 1 0
> 0 0 1 0 0
> 0 1 1 0 1
> 1 0 0 1 0
>
> Sample Output-1:
> ----------------
> 3
>
> Explanation:
> ------------
> In the given grid, 1's at (2,2), (3,1), (3,2) positions are not connected to the boundary
> So, number of people cannot be saved are 3
>
> Sample Input-2:
> ---------------
> 5
> 0 0 1 1 0
> 1 0 0 1 0
> 0 0 1 1 0
> 0 1 1 0 1
> 1 0 0 1 0
>
> Sample Output-2:
> ----------------
> 0
>
> Explanation:
> ------------
> In the given grid, each 1 is either at the boundary or connceted to 1 at boundary.
> So, number of people cannot be saved are '0'
>
> */
>
> import java.util.*;
>
> class RescuePeople {
>     public int rescuePeople(int[][] A) {
>         int result = 0;
>         for(int i = 0; i < A.length; i++) {
>             for(int j = 0; j < A[i].length; j++) {
>                 if(i == 0 || j == 0 || i == A.length - 1 || j == A[i].length - 1)
>                     dfs(A, i, j);
>             }
>         }
>         
>         for(int i = 0; i < A.length; i++) {
>             for(int j = 0; j < A[i].length; j++) {
>                 if(A[i][j] == 1)
>                     result++;
>             }
>         }
>         
>         return result;
>     }
>     
>     public void dfs(int a[][], int i, int j) {
>         if(i >= 0 && i <= a.length - 1 && j >= 0 && j <= a[i].length - 1 && a[i][j] == 1) {
>             a[i][j] = 0;
>             dfs(a, i + 1, j);
>             dfs(a, i - 1, j);
>             dfs(a, i, j + 1);
>             dfs(a, i, j - 1);
>         }
>     }
> 	
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		int N=sc.nextInt();
> 		int arr[][]=new int[N][N];
> 		for(int i=0;i<N;i++)
> 			for(int j=0;j<N;j++)
> 				arr[i][j]=sc.nextInt();
> 		System.out.println(new RescuePeople().rescuePeople(arr));
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20111%20Solutions/RescuePeople.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 111 Solutions/RescuePeople.txt
