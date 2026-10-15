---
kind: "coding-problem"
title: "Corner Rectangles (Day 44)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 44 Solutions/CornerRectangles.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Corner Rectangles (Day 44)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a grid where each entry is only 0 or 1, find the number of corner rectangles.

A corner rectangle is 4 distinct 1s on the grid that form an axis-aligned rectangle.
 Note that only the corners need to have the value 1. Also, all four 1s used must be distinct.
 
 If you are not able to form a rectangle print -1,
 If you are not able to form a matrix print -2.

Example 1:
	Input:	4 5
				1 0 0 1 0
				0 0 1 0 1
				0 0 0 1 0
				1 0 1 0 1
	Output: 1
	Explanation: There is only one corner rectangle, with corners grid[1][2], grid[1][4], grid[3][2], grid[3][4].
 

Example 2:
	Input:3 3
	1 1 1
	1 1 1
	1 1 1
	Output: 9
	Explanation: There are four 2x2 rectangles, four 2x3 and 3x2 rectangles, and one 3x3 rectangle.
 

Example 3:
	Input: 1 4
	Output: -1
	Explanation: Rectangles must have four distinct corners.
 
 
 ==========TestCases=============
 case =1
input =3 4
1 0 1 0
1 1 1 1
0 1 1 1
output =4

case =2
input =4 6
1 0 1 1 1 1
1 0 1 1 0 1
0 1 0 1 1 1
1 1 1 1 0 1
output =25

case =3
input =5 5
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
1 1 1 1 1
output =100

case =4
input =5 6
1 1 0 1 0 1
1 1 0 1 1 0
1 1 0 1 1 1
1 0 1 0 0 0
0 1 1 1 1 0
output =22

case =5
input =3 3
1 0 0 
0 1 0
0 0 1
output =0

case =6
input =3 2
1 1
0 1
1 1
output =1

case =7
input =4 4
1 0 0 1
0 1 1 0
0 1 1 0
1 0 0 1
output =2

case =8
input =7 9
1 1 1 0 1 1 0 1 1
1 1 0 1 1 0 1 0 1
1 0 1 1 0 1 0 1 0
0 1 1 1 1 0 1 0 1
1 0 1 1 1 1 0 1 1
1 1 0 1 1 0 1 0 1
1 1 1 0 1 1 0 1 1
output =165

case =9
input =6 7
1 1 1 0 1 1 0
1 1 0 1 1 0 1
1 0 1 1 0 1 0
0 1 1 1 1 0 1
1 0 1 1 1 1 0
1 1 0 1 1 0 1
output =58

case =10
input =5 6
1 1 1 1 0 0
1 1 1 0 0 1
1 1 0 0 1 1
1 0 0 1 1 1
0 0 1 1 1 1
output =18

case =11
input =3 1
output =-1

case =12
input =4 0
output =-2

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · CornerRectangles.java
> ```java
> /*
>  * 
> Given a grid where each entry is only 0 or 1, find the number of corner rectangles.
>
> A corner rectangle is 4 distinct 1s on the grid that form an axis-aligned rectangle.
>  Note that only the corners need to have the value 1. Also, all four 1s used must be distinct.
>  
>  If you are not able to form a rectangle print -1,
>  If you are not able to form a matrix print -2.
>
> Example 1:
> 	Input:	4 5
> 				1 0 0 1 0
> 				0 0 1 0 1
> 				0 0 0 1 0
> 				1 0 1 0 1
> 	Output: 1
> 	Explanation: There is only one corner rectangle, with corners grid[1][2], grid[1][4], grid[3][2], grid[3][4].
>  
>
> Example 2:
> 	Input:3 3
> 	1 1 1
> 	1 1 1
> 	1 1 1
> 	Output: 9
> 	Explanation: There are four 2x2 rectangles, four 2x3 and 3x2 rectangles, and one 3x3 rectangle.
>  
>
> Example 3:
> 	Input: 1 4
> 	Output: -1
> 	Explanation: Rectangles must have four distinct corners.
>  
>  
>  ==========TestCases=============
>  case =1
> input =3 4
> 1 0 1 0
> 1 1 1 1
> 0 1 1 1
> output =4
>
> case =2
> input =4 6
> 1 0 1 1 1 1
> 1 0 1 1 0 1
> 0 1 0 1 1 1
> 1 1 1 1 0 1
> output =25
>
> case =3
> input =5 5
> 1 1 1 1 1
> 1 1 1 1 1
> 1 1 1 1 1
> 1 1 1 1 1
> 1 1 1 1 1
> output =100
>
> case =4
> input =5 6
> 1 1 0 1 0 1
> 1 1 0 1 1 0
> 1 1 0 1 1 1
> 1 0 1 0 0 0
> 0 1 1 1 1 0
> output =22
>
> case =5
> input =3 3
> 1 0 0 
> 0 1 0
> 0 0 1
> output =0
>
> case =6
> input =3 2
> 1 1
> 0 1
> 1 1
> output =1
>
> case =7
> input =4 4
> 1 0 0 1
> 0 1 1 0
> 0 1 1 0
> 1 0 0 1
> output =2
>
> case =8
> input =7 9
> 1 1 1 0 1 1 0 1 1
> 1 1 0 1 1 0 1 0 1
> 1 0 1 1 0 1 0 1 0
> 0 1 1 1 1 0 1 0 1
> 1 0 1 1 1 1 0 1 1
> 1 1 0 1 1 0 1 0 1
> 1 1 1 0 1 1 0 1 1
> output =165
>
> case =9
> input =6 7
> 1 1 1 0 1 1 0
> 1 1 0 1 1 0 1
> 1 0 1 1 0 1 0
> 0 1 1 1 1 0 1
> 1 0 1 1 1 1 0
> 1 1 0 1 1 0 1
> output =58
>
> case =10
> input =5 6
> 1 1 1 1 0 0
> 1 1 1 0 0 1
> 1 1 0 0 1 1
> 1 0 0 1 1 1
> 0 0 1 1 1 1
> output =18
>
> case =11
> input =3 1
> output =-1
>
> case =12
> input =4 0
> output =-2
>  
>
>  */
>
> import java.util.Scanner;
>
> public class CornerRectangles {
>
> 	 public static int countCornerRectangles(int[][] grid) {
> 	        int ans = 0;
> 	        for (int i = 0; i < grid.length - 1; i++) {
> 	            for (int j = i + 1; j < grid.length; j++) {
> 	                int counter = 0;
> 	                for (int k = 0; k < grid[0].length; k++) {
> 	                    if (grid[i][k] == 1 && grid[j][k] == 1) counter++;
> 	                }
> 	                if (counter > 0) ans += counter * (counter - 1) / 2;
> 	            }
> 	        }
> 	        return ans;
> 	    }
> 	 
> 	  public static void main(String args[] ) {
> 			 Scanner scan = new Scanner(System.in);
> 				int R=scan.nextInt();
> 				int C=scan.nextInt();      
>
> 				int[][] grid=new int[R][C];
> 			       for(int i=0; i<R; i++)
> 			       {
> 			           for(int j=0; j<C; j++)
> 			           {
> 			        	   grid[i][j] = scan.nextInt();
> 			           }
> 			       }
> 			       System.out.println(countCornerRectangles(grid));
> 		}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2044%20Solutions/CornerRectangles.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 44 Solutions/CornerRectangles.java
