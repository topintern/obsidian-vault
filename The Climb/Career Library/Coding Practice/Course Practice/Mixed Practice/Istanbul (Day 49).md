---
kind: "coding-problem"
title: "Istanbul (Day 49)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 49 Solutions/Istanbul.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Istanbul (Day 49)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

The city of Istanbul is represented as an n*m matrix, where rows and columns start with index 1.

Istanbul has a network of road ways that always run in straight horizontal lines along a row. 
In other words, the start and end points of a road way are (r,c1) and (r,c2), 
where r represents the row number, c1 represents the starting column, 
and c2 represents the ending column of the road way.

The mayor of Istanbul is surveying the city to determine the number of locations 
where pylons can be placed. A pylon can be placed in any cell that is not occupied by a road way.

Given a map of Istanbul and its k road ways, 
find and print the number of cells where the mayor can place pylons.


### Input Format

The first line contains three space-separated integers n,m and k, 
	- the number of rows, columns and ways to be mapped.
Each of the next  lines contains three space-separated integers, r,c1 and c2, 
	- the row number and the way column start and end.


### Output Format

Print a single integer denoting the number of cells where the mayor can install pylons.

Sample Input
	4 4 3
	2 2 3
	3 1 4
	4 4 4
Sample Output
	9

Note: A road way may overlap other road ways within the same row.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Istanbul.java
> ```java
> /*
> The city of Istanbul is represented as an n*m matrix, where rows and columns start with index 1.
>
> Istanbul has a network of road ways that always run in straight horizontal lines along a row. 
> In other words, the start and end points of a road way are (r,c1) and (r,c2), 
> where r represents the row number, c1 represents the starting column, 
> and c2 represents the ending column of the road way.
>
> The mayor of Istanbul is surveying the city to determine the number of locations 
> where pylons can be placed. A pylon can be placed in any cell that is not occupied by a road way.
>
> Given a map of Istanbul and its k road ways, 
> find and print the number of cells where the mayor can place pylons.
>
> Input Format
> The first line contains three space-separated integers n,m and k, 
> 	- the number of rows, columns and ways to be mapped.
> Each of the next  lines contains three space-separated integers, r,c1 and c2, 
> 	- the row number and the way column start and end.
>
> Output Format
> Print a single integer denoting the number of cells where the mayor can install pylons.
>
> Sample Input
> 	4 4 3
> 	2 2 3
> 	3 1 4
> 	4 4 4
> Sample Output
> 	9
>
> Note: A road way may overlap other road ways within the same row.
> */
>
> import java.io.*;
> import java.util.*;
>
> public class Istanbul {
>
>     public static void main(String[] args) {
>         Scanner scan = new Scanner(System.in);
>         Map<Long, ArrayList<Point>> map = new HashMap<Long, ArrayList<Point>>();
>         long n,m,k;
>         long r, c1, c2;
>         n = scan.nextLong();
>         m = scan.nextLong();
>         k = scan.nextLong();
>         for (int i=0;i<k;i++) {
>             r = scan.nextLong();
>             c1 = scan.nextLong();
>             c2 = scan.nextLong();
>             if (map.get(r) == null) map.put(r, new ArrayList<Point>());
>             map.get(r).add(new Point(c1, true));
>             map.get(r).add(new Point(c2, false));
>         }
>         long blockedCells = 0;
>         for (long key : map.keySet()) {
>             ArrayList<Point> tracks = map.get(key);
>             Collections.sort(tracks);
>             Point prev = null;
>             int cnt = 0;
>             for (Point col : tracks) {
>                 if (col.start) {
>                     if (cnt == 0) {
>                         prev = col;
>                     } 
>                    cnt++;
>                 } else {
>                     cnt--;
>                    if (cnt == 0) {
>                        blockedCells += col.x - prev.x + 1;
>                    }
>                 }
>             }
>         }
>         
>         System.out.println(n*m-blockedCells);
>     }
> }
>
> class Point implements Comparable<Point> {
>     public long x;
>     public boolean start;
>     public Point(long x, boolean start) {
>         this.x = x;
>         this.start = start;
>     }
>     
>     public int compareTo(Point other) {
>         long diff = this.x - other.x;
>         if (diff == 0) {
>             if (this.start && !other.start) return -1;
>             if (other.start && !this.start) return 1;
>             return 0;
>         }
>         return (int)diff;
>     }
> }
>
> /*
>
> ======== Testcases Program-5 =========
> case =1
> input =4 4 3
> 2 2 3
> 3 1 4
> 4 4 4
> output =9
>
> case =2
> input =8 7 5
> 1 4 7
> 3 2 6
> 8 1 5
> 3 2 5
> 7 2 6
> output =37
>
> case =3
> input =9 9 7
> 1 6 7
> 6 2 8
> 4 4 6
> 2 5 7
> 3 7 9
> 5 2 8
> 9 2 6
> output =51
>
> case =4
> input =6 5 6
> 1 2 4
> 2 3 5
> 3 1 4
> 4 2 5
> 5 2 5
> 6 1 5
> output =7
>
> case =5
> input =8 8 6
> 2 3 4
> 3 4 5
> 4 5 6
> 5 6 7
> 6 7 8
> 7 1 8
> output =46
>
> case =6
> input =7 6 6
> 1 3 5
> 1 1 6
> 2 3 4
> 4 1 5
> 3 2 6
> 5 2 4
> output =21
>
> case =7
> input =9 9 9
> 1 4 9
> 9 2 5
> 3 3 9
> 4 1 6
> 5 3 6
> 6 2 7
> 8 5 9
> 9 1 6
> 8 2 9
> output =38
>
> case =8
> input =5 9 4
> 1 4 9
> 3 3 9
> 4 1 6
> 5 3 6
> output =22
>
> case =9
> input =10 10 5
> 1 2 8
> 3 7 10
> 6 3 9
> 8 1 8
> 9 3 10
> output =66
>
> case =10
> input =10 10 10
> 1 2 8
> 3 7 10
> 6 3 9
> 8 1 8
> 9 3 10
> 2 2 6
> 5 3 10
> 4 6 9
> 8 7 10
> 9 5 10
> output =47
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2049%20Solutions/Istanbul.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 49 Solutions/Istanbul.java
