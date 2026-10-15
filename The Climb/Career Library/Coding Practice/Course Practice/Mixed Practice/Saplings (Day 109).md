---
kind: "coding-problem"
title: "Saplings (Day 109)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 109 Solutions/Saplings.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Saplings (Day 109)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

As a part of Harithaharam, Minister KTR planted few saplings on a flat surface. 
KTR wants to plant more number of saplings,
In order to do that, he wants to find the minimum area covered by any 4 saplings.

You are given positions of saplings as (x,y) co-ordinates.

NOTE: Please make sure that, the 4 saplings should form a rectangle.
otherwise return 0.

Input Format:
----------------
Line-1: An integer N, number of saplings.
Next N lines: two space seperated integers, (x,y).

Output Format:
------------------
Print minimun area as result.


Sample Input-1:
--------------------
5
1 1
1 3
3 1
3 3
2 2

Sample Output-1:
---------------------
4


Sample Input-2:
--------------------
6
1 1
1 3
3 1
3 3
4 1
4 3

Sample Output-2:
---------------------
2

Note: All positions are different.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Saplings.txt
> ```java
> /*
>
> As a part of Harithaharam, Minister KTR planted few saplings on a flat surface. 
> KTR wants to plant more number of saplings,
> In order to do that, he wants to find the minimum area covered by any 4 saplings.
>
> You are given positions of saplings as (x,y) co-ordinates.
>
> NOTE: Please make sure that, the 4 saplings should form a rectangle.
> otherwise return 0.
>
> Input Format:
> ----------------
> Line-1: An integer N, number of saplings.
> Next N lines: two space seperated integers, (x,y).
>
> Output Format:
> ------------------
> Print minimun area as result.
>
>
> Sample Input-1:
> --------------------
> 5
> 1 1
> 1 3
> 3 1
> 3 3
> 2 2
>
> Sample Output-1:
> ---------------------
> 4
>
>
> Sample Input-2:
> --------------------
> 6
> 1 1
> 1 3
> 3 1
> 3 3
> 4 1
> 4 3
>
> Sample Output-2:
> ---------------------
> 2
>
> Note: All positions are different.
>
> */
>
> import java.util.*;
>
> class Saplings {
>     public static int minArea(int[][] points) {
>         Set<Integer> pointSet = new HashSet();
>         for (int[] point: points)
>             pointSet.add(40001 * point[0] + point[1]);
>
>         int ans = Integer.MAX_VALUE;
>         for (int i = 0; i < points.length; ++i)
>             for (int j = i+1; j < points.length; ++j) {
>                 if (points[i][0] != points[j][0] && points[i][1] != points[j][1]) {
>                     if (pointSet.contains(40001 * points[i][0] + points[j][1]) &&
>                             pointSet.contains(40001 * points[j][0] + points[i][1])) {
>                         ans = Math.min(ans, Math.abs(points[j][0] - points[i][0]) *
>                                             Math.abs(points[j][1] - points[i][1]));
>                     }
>                 }
>             }
>
>         return ans < Integer.MAX_VALUE ? ans : 0;
>     }
> 	
> 	public static void main(String args[])
> 	{
> 		Scanner sc = new Scanner(System.in);
> 		int n=sc.nextInt();
> 		int points[][]=new int[n][2];
> 		for(int i=0;i<n;i++){
> 			points[i][0]=sc.nextInt();
> 			points[i][1]=sc.nextInt();
> 		}
> 		System.out.println(minArea(points));
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20109%20Solutions/Saplings.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 109 Solutions/Saplings.txt
