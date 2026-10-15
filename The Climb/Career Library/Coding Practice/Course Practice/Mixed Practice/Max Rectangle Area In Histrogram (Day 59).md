---
kind: "coding-problem"
title: "Max Rectangle Area In Histrogram (Day 59)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 59 Solutions/MaxRectangleAreaInHistrogram.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Max Rectangle Area In Histrogram (Day 59)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Largest rectangle under histogram: 
A histogram is a polygon composed of a sequence of rectangles aligned at a common base line.
For simplicity, assume that the rectangles have equal widths but may have different heights. 
For	example, the figure on the left shows a histogram that consists of rectangles 
with the heights 3, 2, 5, 6, 1, 4, 4, measuredin units where 1 is the width of the rectangles.

Here our problem is:given an array with heights of rectangles (assuming	width is 1),
we need to find the largest rectangle.
In below diagram, each line(|) indicates one small rectangle.

         |						 		   |
      |  |					          |==|
      |  |     |  |				      |==|    |  |
|     |  |     |  |				|     |==|    |  |
|  |  |  |     |  |			    |  |  |==|     |  |
|  |  |  |  |  |  |				|  |  |==|  |  |  |
3  2  5  6  1  4  4				3  2  5  6  1  4  4

### Sample Input

	7
	3 2 5 6 1 4 4

### Sample Output

	10

Explanation: Here using 5 and 6 rectangles. we can make maximum rectangle choosing height "5" from each rectangle.
so, 5*2 = 10. 


========= Testcases Program-3 =========
case =1
input =6
2 3 4 6 7 4
output =16

case =2
input =3
5 1 6
output =6

case =3
input =9
6 7 4 1 1 6 8 3 4
output =12

case =4
input =7
3 2 5 6 1 4 4
output =10

case =5
input =10
7 3 8 5 6 3 4 9 2 8
output =24

case =6
input =12
20 12 20 5 10 20 8 15 12 14 11 9
output =64

case =7
input =15
20 12 20 5 10 20 8 15 12 14 11 9 16 13 18
output =88

case =8
input =20
80 55 31 76 44 68 95 69 96 13 74 36 17 19 18 37 16 81 86 98
output =279

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MaxRectangleAreaInHistrogram.java
> ```java
> /*
> Largest rectangle under histogram: 
> A histogram is a polygon composed of a sequence of rectangles aligned at a common base line.
> For simplicity, assume that the rectangles have equal widths but may have different heights. 
> For	example, the figure on the left shows a histogram that consists of rectangles 
> with the heights 3, 2, 5, 6, 1, 4, 4, measuredin units where 1 is the width of the rectangles.
>
> Here our problem is:given an array with heights of rectangles (assuming	width is 1),
> we need to find the largest rectangle.
> In below diagram, each line(|) indicates one small rectangle.
>
>          |						 		   |
>       |  |					          |==|
>       |  |     |  |				      |==|    |  |
> |     |  |     |  |				|     |==|    |  |
> |  |  |  |     |  |			    |  |  |==|     |  |
> |  |  |  |  |  |  |				|  |  |==|  |  |  |
> 3  2  5  6  1  4  4				3  2  5  6  1  4  4
> Sample Input:
> 	7
> 	3 2 5 6 1 4 4
> Sample Output:
> 	10
>
> Explanation: Here using 5 and 6 rectangles. we can make maximum rectangle choosing height "5" from each rectangle.
> so, 5*2 = 10. 
>
>
> ========= Testcases Program-3 =========
> case =1
> input =6
> 2 3 4 6 7 4
> output =16
>
> case =2
> input =3
> 5 1 6
> output =6
>
> case =3
> input =9
> 6 7 4 1 1 6 8 3 4
> output =12
>
> case =4
> input =7
> 3 2 5 6 1 4 4
> output =10
>
> case =5
> input =10
> 7 3 8 5 6 3 4 9 2 8
> output =24
>
> case =6
> input =12
> 20 12 20 5 10 20 8 15 12 14 11 9
> output =64
>
> case =7
> input =15
> 20 12 20 5 10 20 8 15 12 14 11 9 16 13 18
> output =88
>
> case =8
> input =20
> 80 55 31 76 44 68 95 69 96 13 74 36 17 19 18 37 16 81 86 98
> output =279
>
>
>  */
>
> import java.util.Scanner;
> import java.util.Stack;
>
> public class MaxRectangleAreaInHistrogram {
> 	
> 	
> 	public static void main(String args[]) {
> 		
> 		Scanner sc = new Scanner(System.in);
> 		
> 		int totalNumOfRectangles = sc.nextInt();
> 		int[] a = new int[totalNumOfRectangles];
> 		
> 		for(int i=0;i<totalNumOfRectangles;i++)
> 			a[i] = sc.nextInt();
> 		
> 		System.out.println(MaxRectangleArea(a));
> 	}
> 	
>     public static int MaxRectangleArea(int[] A) {
>         Stack<Integer> s = new Stack<Integer>();
>         if(A == null || A.length == 0)
>             return 0;
>         // Initialize max area
>         int maxArea = 0;
>         int i = 0;
>         // run through all bars of given histogram
>         while(i < A.length) {
>         	     	
>             // If current bar is higher than the bar of the stack peek, push it to stack. 
>             if(s.empty() || A[s.peek()] <= A[i])
>                 s.push(i++);
>             else {
>                 // if current bar is lower than the stack peek, calculate area of rectangle with stack top as the smallest bar.
>                 // 'i' is 'right index' for the top and element before top in stack is 'left index'
>                 int top = s.pop();
>                 // calculate the area with A[top] stack as smallest bar and update maxArea if needed
>                 maxArea = Math.max(maxArea, A[top] * (s.empty() ? i : i - s.peek() - 1));
>             }
>         }
>         // Now pop the remaining bars from stack and calculate area with every popped bar as the smallest bar.
>         while(!s.isEmpty()) {
>             int top = s.pop();
>             maxArea = Math.max(maxArea, A[top] * (s.empty() ? i : i - s.peek() - 1));
>         }
>         return maxArea;
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2059%20Solutions/MaxRectangleAreaInHistrogram.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 59 Solutions/MaxRectangleAreaInHistrogram.java
