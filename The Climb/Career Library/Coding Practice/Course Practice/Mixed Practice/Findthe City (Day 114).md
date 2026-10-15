---
kind: "coding-problem"
title: "Findthe City (Day 114)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 114 Solutions/FindtheCity.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Findthe City (Day 114)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Amith decided go on a holiday trip. 
Given a map of N holiday spots numbered 0,1,2,.. N-1, map shows the connecting routes
between the holiday sopts, the routes are bidirectional, and
the connecting routes are indicates as routes[i] = [from , to , distance ]. 
He can travel only a certian distance D.

Your task is to find the holiday spot H with the smallest number of holiday spots
that are reachable from H and whose distance is at most D, 

If there are multiple holiday spots, return H with the greatest number.


Input Format:
-------------
Line-1 -> Three integers, N number of holiday spots, R is the number of connecting routes
          and D is the distance can travel.
Next R lines -> Three space separated integers, from , to and distance.

Output Format:
--------------
Print an integer, holiday spot.


Sample Input-1:
---------------
4 4 4
0 1 3
1 2 1
1 3 4
2 3 1

Sample Output-1:
----------------
3



### Explanation

------------
Distance can travel= 4,

From			Reachable sopts
-------------------------------------
Holiday-spot 0 -> [Holiday-spot 1, Holiday-spot 2] 
Holiday-spot 1 -> [Holiday-spot 0, Holiday-spot 2, Holiday-spot 3] 
Holiday-spot 2 -> [Holiday-spot 0, Holiday-spot 1, Holiday-spot 3] 
Holiday-spot 3 -> [Holiday-spot 1, Holiday-spot 2] 

Holiday-spots 0 and 3 have 2 reachable Holiday-spots at a distance = 4, 
but we have to return Holiday-spot 3 since it has the greatest number.


Sample Input-2:
---------------
5 6 2
0 1 2
0 4 8
1 2 3
1 4 2
2 3 1
3 4 1

Sample Output-2:
----------------
0


### Explanation

------------
Distance can travel= 2,

From			Reachable sopts
-------------------------------------
Holiday-spot 0 -> [Holiday-spot 1] 
Holiday-spot 1 -> [Holiday-spot 0, Holiday-spot 4] 
Holiday-spot 2 -> [Holiday-spot 3, Holiday-spot 4] 
Holiday-spot 3 -> [Holiday-spot 2, Holiday-spot 4]
Holiday-spot 4 -> [Holiday-spot 1, Holiday-spot 2, Holiday-spot 3]

Holiday-spots 0 has 1 reachable Holiday-spot at a distance = 2,

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · FindtheCity.java
> ```java
> /*
> Amith decided go on a holiday trip. 
> Given a map of N holiday spots numbered 0,1,2,.. N-1, map shows the connecting routes
> between the holiday sopts, the routes are bidirectional, and
> the connecting routes are indicates as routes[i] = [from , to , distance ]. 
> He can travel only a certian distance D.
>
> Your task is to find the holiday spot H with the smallest number of holiday spots
> that are reachable from H and whose distance is at most D, 
>
> If there are multiple holiday spots, return H with the greatest number.
>
>
> Input Format:
> -------------
> Line-1 -> Three integers, N number of holiday spots, R is the number of connecting routes
>           and D is the distance can travel.
> Next R lines -> Three space separated integers, from , to and distance.
>
> Output Format:
> --------------
> Print an integer, holiday spot.
>
>
> Sample Input-1:
> ---------------
> 4 4 4
> 0 1 3
> 1 2 1
> 1 3 4
> 2 3 1
>
> Sample Output-1:
> ----------------
> 3
>
>
> Explanation:
> ------------
> Distance can travel= 4,
>
> From			Reachable sopts
> -------------------------------------
> Holiday-spot 0 -> [Holiday-spot 1, Holiday-spot 2] 
> Holiday-spot 1 -> [Holiday-spot 0, Holiday-spot 2, Holiday-spot 3] 
> Holiday-spot 2 -> [Holiday-spot 0, Holiday-spot 1, Holiday-spot 3] 
> Holiday-spot 3 -> [Holiday-spot 1, Holiday-spot 2] 
>
> Holiday-spots 0 and 3 have 2 reachable Holiday-spots at a distance = 4, 
> but we have to return Holiday-spot 3 since it has the greatest number.
>
>
> Sample Input-2:
> ---------------
> 5 6 2
> 0 1 2
> 0 4 8
> 1 2 3
> 1 4 2
> 2 3 1
> 3 4 1
>
> Sample Output-2:
> ----------------
> 0
>
> Explanation:
> ------------
> Distance can travel= 2,
>
> From			Reachable sopts
> -------------------------------------
> Holiday-spot 0 -> [Holiday-spot 1] 
> Holiday-spot 1 -> [Holiday-spot 0, Holiday-spot 4] 
> Holiday-spot 2 -> [Holiday-spot 3, Holiday-spot 4] 
> Holiday-spot 3 -> [Holiday-spot 2, Holiday-spot 4]
> Holiday-spot 4 -> [Holiday-spot 1, Holiday-spot 2, Holiday-spot 3]
>
> Holiday-spots 0 has 1 reachable Holiday-spot at a distance = 2, 
>
>
> */
>
> import java.util.*;
>
> class FindtheCity{
> 	public int findTheCity(int n, int[][] routes, int distance) {
>         int[][] dis = new int[n][n];
>         int res = 0, smallest = n;
>         for (int[] row : dis)
>             Arrays.fill(row, 10001);
>         for (int[] e : routes)
>             dis[e[0]][e[1]] = dis[e[1]][e[0]] = e[2];
>         for (int i = 0; i < n; ++i)
>             dis[i][i] = 0;
>         for (int k = 0; k < n; ++k)
>             for (int i = 0; i < n; ++i)
>                 for (int j = 0; j < n; ++j)
>                     dis[i][j] = Math.min(dis[i][j], dis[i][k] + dis[k][j]);
>         for (int i = 0; i < n; i++) {
>             int count = 0;
>             for (int j = 0; j < n; ++j)
>                 if (dis[i][j] <= distance)
>                     ++count;
>             if (count <= smallest) {
>                 res = i;
>                 smallest = count;
>             }
>         }
>         return res;
>     }
> 	
> 	public static void main(String args[])
> 	{
> 		Scanner sc = new Scanner(System.in);
> 		int N=sc.nextInt();
> 		int R=sc.nextInt();
> 		int D=sc.nextInt();
> 		int[][] routes=new int[R][3];
> 		for(int i=0;i<R;i++)
> 			for(int j=0;j<3;j++)
> 				routes[i][j]=sc.nextInt();
> 		System.out.println(new FindtheCity().findTheCity(N,routes,D));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20114%20Solutions/FindtheCity.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 114 Solutions/FindtheCity.java
