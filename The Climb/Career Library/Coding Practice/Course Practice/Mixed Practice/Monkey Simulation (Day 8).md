---
kind: "coding-problem"
title: "Monkey Simulation (Day 8)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 8 Solutions/MonkeySimulation.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Monkey Simulation (Day 8)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

There's a tree, a mokey, and several fruits. 

Positions are represented by the cells in a 2D grid. 

Your goal is to find the minimal distance for the monkey to 
collect all the fruits and put them under the tree one by one. 

The monkey can only take at most one fruit at one time 
and can move in four directions - up, down, left and right, to the adjacent cell. 
The distance is represented by the number of moves.

Example 1:
    Input=5
             7
             2 2
             4 4
             2
             3 0
             2 5
    Output= 12
    Input Format:
        Height : 5
        Width : 7
        Tree position : [2,2]
        Monkey : [4,4]
        Number of Fruits : 2
        Fruits : [[3,0], [2,5]]

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MonkeySimulation.java
> ```java
> /*
> There's a tree, a mokey, and several fruits. 
>
> Positions are represented by the cells in a 2D grid. 
>
> Your goal is to find the minimal distance for the monkey to 
> collect all the fruits and put them under the tree one by one. 
>
> The monkey can only take at most one fruit at one time 
> and can move in four directions - up, down, left and right, to the adjacent cell. 
> The distance is represented by the number of moves.
>
> Example 1:
>     Input=5
>              7
>              2 2
>              4 4
>              2
>              3 0
>              2 5
>     Output= 12
>     Input Format:
>         Height : 5
>         Width : 7
>         Tree position : [2,2]
>         Monkey : [4,4]
>         Number of Fruits : 2
>         Fruits : [[3,0], [2,5]]
>  */
> import java.util.*;
>
> public class MonkeySimulation {
> 	public static int minDistance(int height, int width, int[] tree, int[] monkey, int[][] fruits) {
>         int tot_dist = 0, d = Integer.MIN_VALUE;
>         for (int[] fruit: fruits) {
>             tot_dist += (distance(fruit, tree) * 2);
>             d = Math.max(d, distance(fruit, tree) - distance(fruit, monkey));
>         }
>         return tot_dist - d;
>     }
>     public static int distance(int[] a, int[] b) {
>         return Math.abs(a[0] - b[0]) + Math.abs(a[1] - b[1]);
>     }
>     
>     public static void main(String args[] ) {
>
> 	    Scanner sc = new Scanner(System.in);
>
> 		int height=sc.nextInt();
> 		int width=sc.nextInt();
> 		
> 		int[] tree = new int[2];
> 		tree[0]=sc.nextInt();
> 		tree[1]=sc.nextInt();
> 		
> 		int[] monkey = new int[2];
> 		monkey[0]=sc.nextInt();
> 		monkey[1]=sc.nextInt();
> 		
> 		int n=sc.nextInt(); // no of nuts
> 		int[][] fruits=new int[n][2];
> 		for(int i=0; i<n; i++)
> 	       {
> 			  fruits[i][0]=sc.nextInt();
> 		      fruits[i][1]=sc.nextInt();	           
> 	       }
> 		System.out.println(minDistance( height, width, tree, monkey,fruits));
> 		}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%208%20Solutions/MonkeySimulation.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 8 Solutions/MonkeySimulation.java
