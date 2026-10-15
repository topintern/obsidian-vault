---
kind: "coding-problem"
title: "Max Area Of Seq Of Plots (Day 14)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 14 Solutions/MaxAreaOfSeqOfPlots.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Max Area Of Seq Of Plots (Day 14)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Problem: write a program to find Maximum area for given sequence of plots.
In a layout of plots, all plots are having equal width, which is 10 meters, but these
plots varies in length For a given sequence of plots lengths, you need find what is maximum
rectangle area you can make ?

	 ----------
 	 |	  |
---------|        |	
|	 | 	  |----------
| 30*10	 | 40*10  |  25*10  |
|        |        |	    |---------
|	 |        |	    |  20*10 |
-------------------------------------
 

### Sample Input

4
30 40 25 20 


### Sample Output

800


### Explanation

	 Max Area is 4*10*20 = 800 sq meters

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MaxAreaOfSeqOfPlots.java
> ```java
> /*
> Problem: write a program to find Maximum area for given sequence of plots.
> In a layout of plots, all plots are having equal width, which is 10 meters, but these
> plots varies in length For a given sequence of plots lengths, you need find what is maximum
> rectangle area you can make ?
>
> 	 ----------
>  	 |	  |
> ---------|        |	
> |	 | 	  |----------
> | 30*10	 | 40*10  |  25*10  |
> |        |        |	    |---------
> |	 |        |	    |  20*10 |
> -------------------------------------
>  
> Sample Input:
> 4
> 30 40 25 20 
>
> Sample Output:
> 800
>
> Explanation:
> 	 Max Area is 4*10*20 = 800 sq meters
>
>  */
>
> import java.util.Scanner;
> import java.util.Stack;
>
> public class MaxAreaOfSeqOfPlots {
> 	
> 	
> 	public static void main(String args[]) {
> 		
> 		Scanner sc = new Scanner(System.in);
> 		
> 		int totalNumOfPlots = sc.nextInt();
> 		int[] a = new int[totalNumOfPlots];
> 		
> 		for(int i=0;i<totalNumOfPlots;i++)
> 			a[i] = sc.nextInt()*10;//multiplying length with width of the plot 
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

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2014%20Solutions/MaxAreaOfSeqOfPlots.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 14 Solutions/MaxAreaOfSeqOfPlots.java
