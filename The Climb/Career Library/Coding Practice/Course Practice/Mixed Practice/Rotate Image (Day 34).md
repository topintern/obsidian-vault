---
kind: "coding-problem"
title: "Rotate Image (Day 34)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 34 Solutions/RotateImage.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Rotate Image (Day 34)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Venkat is playing with Integer Matrices, 
He is transforming the matix content as described in the examples
	
Example-1:

    Input = 3
            7 8 9
    		4 5 6
    		1 2 3
    		
    Output= `[[1, 4, 7], [2, 5, 8], [3, 6, 9]]`
Example-2:

    Input=  4
            2 3 4 5
    		6 7 10 9
    		5 4 3 2
    		9 8 7 4
    			 
    Output= `[[9, 5, 6, 2], [8, 4, 7, 3], [7, 3, 10, 4], [4, 2, 9, 5]]`
Note:
You may assume given matrix is a square matrix.
You have to modify the input 2D matrix without using additional matrix.

```text
=====TestCases=========
case =1
input =4
1 2 3 4
5 6 7 8
9 10 11 12
13 14 15 16
output =`[[13, 9, 5, 1], [14, 10, 6, 2], [15, 11, 7, 3], [16, 12, 8, 4]]`
case =2
input =5
8 4 6 7 3
0 3 21 4 5
6 3 2 7 4
9 6 7 5 4
74 5 3 8 2
output =`[[74, 9, 6, 0, 8], [5, 6, 3, 3, 4], [3, 7, 2, 21, 6], [8, 5, 7, 4, 7], [2, 4, 4, 5, 3]]`
case =3
input =3
8 4 2
7 6 9
3 8 5
output =`[[3, 7, 8], [8, 6, 4], [5, 9, 2]]`
case =4
input =2
23 43
54 56
output =`[[54, 23], [56, 43]]`
case =5
input =1
5
output =`[[5]]`
case =6
input =6
1 1 1 1 1 1
2 2 2 2 2 2
3 3 3 3 3 3
4 4 4 4 4 4
5 5 5 5 5 5
6 6 6 6 6 6
output =`[[6, 5, 4, 3, 2, 1], [6, 5, 4, 3, 2, 1], [6, 5, 4, 3, 2, 1], [6, 5, 4, 3, 2, 1], [6, 5, 4, 3, 2, 1], [6, 5, 4, 3, 2, 1]]`
```


## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · RotateImage.java
> ```java
> /*
> Venkat is playing with Integer Matrices, 
> He is transforming the matix content as described in the examples
> 	
> Example-1:
>
>     Input = 3
>             7 8 9
>     		4 5 6
>     		1 2 3
>     		
>     Output= [[1, 4, 7], [2, 5, 8], [3, 6, 9]]
>     			   
>
> Example-2:
>
>     Input=  4
>             2 3 4 5
>     		6 7 10 9
>     		5 4 3 2
>     		9 8 7 4
>     			 
>     Output= [[9, 5, 6, 2], [8, 4, 7, 3], [7, 3, 10, 4], [4, 2, 9, 5]]
>
> Note:
> You may assume given matrix is a square matrix.
> You have to modify the input 2D matrix without using additional matrix.
>
> =====TestCases=========
> case =1
> input =4
> 1 2 3 4
> 5 6 7 8
> 9 10 11 12
> 13 14 15 16
> output =[[13, 9, 5, 1], [14, 10, 6, 2], [15, 11, 7, 3], [16, 12, 8, 4]]
>
> case =2
> input =5
> 8 4 6 7 3
> 0 3 21 4 5
> 6 3 2 7 4
> 9 6 7 5 4
> 74 5 3 8 2
> output =[[74, 9, 6, 0, 8], [5, 6, 3, 3, 4], [3, 7, 2, 21, 6], [8, 5, 7, 4, 7], [2, 4, 4, 5, 3]]
>
> case =3
> input =3
> 8 4 2
> 7 6 9
> 3 8 5
> output =[[3, 7, 8], [8, 6, 4], [5, 9, 2]]
>
> case =4
> input =2
> 23 43
> 54 56
> output =[[54, 23], [56, 43]]
>
> case =5
> input =1
> 5
> output =[[5]]
>
> case =6
> input =6
> 1 1 1 1 1 1
> 2 2 2 2 2 2
> 3 3 3 3 3 3
> 4 4 4 4 4 4
> 5 5 5 5 5 5
> 6 6 6 6 6 6
> output =[[6, 5, 4, 3, 2, 1], [6, 5, 4, 3, 2, 1], [6, 5, 4, 3, 2, 1], [6, 5, 4, 3, 2, 1], [6, 5, 4, 3, 2, 1], [6, 5, 4, 3, 2, 1]]
>
> */
>
>
> import java.util.Scanner;
> import java.util.Arrays;
>
> class RotateImage {
>   public static void rotate(int[][] matrix) {
>     int n = matrix.length;
>     for (int i = 0; i < (n + 1) / 2; i ++) {
>       for (int j = 0; j < n / 2; j++) {
>         int temp = matrix[n - 1 - j][i];
>         matrix[n - 1 - j][i] = matrix[n - 1 - i][n - j - 1];
>         matrix[n - 1 - i][n - j - 1] = matrix[j][n - 1 -i];
>         matrix[j][n - 1 - i] = matrix[i][j];
>         matrix[i][j] = temp;
>       }
>     }
>   }
>   public static void main(String args[])
>   {
> 	  Scanner sc=new Scanner(System.in);
> 	  int n=sc.nextInt();
> 	  int[][] arr=new int[n][n];
> 	  for(int i=0;i<n;i++)
> 		  for(int j=0;j<n;j++)
> 			  arr[i][j]=sc.nextInt();
> 	  rotate(arr);
> 	  System.out.println(Arrays.deepToString( arr ) );
>   }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2034%20Solutions/RotateImage.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 34 Solutions/RotateImage.java
