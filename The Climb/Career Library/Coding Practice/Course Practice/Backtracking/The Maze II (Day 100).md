---
kind: "coding-problem"
title: "The Maze II (Day 100)"
collection: "Course Practice"
topic: "Backtracking"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 100 Solutions/MazeII.java","CODING RESOURCES/ELITE FS COMPLETE/Day 100 Solutions/The Maze II - LeetCode.pdf"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# The Maze II (Day 100)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Problem

Read the original PDF below. Its mathematical notation was not reliably preserved by text extraction.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MazeII.java
> ```java
> import java.util.*;
>
> public class MazeII {
>     class Point {
>         int x,y,l;
>         public Point(int _x, int _y, int _l) {x=_x;y=_y;l=_l;}
>     }
>     public int shortestDistance(int[][] maze, int[] start, int[] destination) {
>         int m=maze.length, n=maze[0].length;
>         int[][] length=new int[m][n]; // record length
>         for (int i=0;i<m*n;i++) length[i/n][i%n]=Integer.MAX_VALUE;
>         int[][] dir=new int[][] {{-1,0},{0,1},{1,0},{0,-1}};
>         PriorityQueue<Point> list=new PriorityQueue<>((o1,o2)->o1.l-o2.l); // using priority queue
>         list.offer(new Point(start[0], start[1], 0));
>         while (!list.isEmpty()) {
>             Point p=list.poll();
>             if (length[p.x][p.y]<=p.l) continue; // if we have already found a route shorter
>             length[p.x][p.y]=p.l;
>             for (int i=0;i<4;i++) {
>                 int xx=p.x, yy=p.y, l=p.l;
>                 while (xx>=0 && xx<m && yy>=0 && yy<n && maze[xx][yy]==0) {
>                     xx+=dir[i][0];
>                     yy+=dir[i][1];
>                     l++;
>                 }
>                 xx-=dir[i][0];
>                 yy-=dir[i][1];
>                 l--;
>                 list.offer(new Point(xx, yy, l));
>             }
>         }
>         return length[destination[0]][destination[1]]==Integer.MAX_VALUE?-1:length[destination[0]][destination[1]];
>     }
> 	
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		MazeII m=new MazeII();
> 		int n=sc.nextInt();
> 		int start[]=new int[2];
> 		int destination[]=new int[2];
> 		int maze[][]=new int[n][n];
> 		for(int i=0;i<n;i++)
> 			for(int j=0;j<n;j++)
> 				maze[i][j]=sc.nextInt();
> 		start[0]=sc.nextInt();
> 		start[1]=sc.nextInt();
> 		destination[0]=sc.nextInt();
> 		destination[1]=sc.nextInt();
> 		int distance=m.shortestDistance(maze,start,destination);
> 	
> 		if(distance > 0)
> 			System.out.println(distance);
> 		else
> 			System.out.println("-1");
> 	}
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/The Maze II - Leet Code-7067ae24.pdf|The Maze II - Leet Code-7067ae24.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/The Maze II - Leet Code-7067ae24.pdf#height=420]]

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20100%20Solutions/MazeII.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 100 Solutions/MazeII.java
- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20100%20Solutions/The%20Maze%20II%20-%20LeetCode.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 100 Solutions/The Maze II - LeetCode.pdf
