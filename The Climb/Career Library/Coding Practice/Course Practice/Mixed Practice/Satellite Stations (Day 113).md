---
kind: "coding-problem"
title: "Satellite Stations (Day 113)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 113 Solutions/SatelliteStations.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Satellite Stations (Day 113)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given N satellite stations, numbered 1 to N.
These satellites are connected to send signals from one to other.
To send a signal from satellite 's' to satellite 'd', it takes an amount of time 't'.

You are given a list of travel times as directed edges times[i] = (s, d, t).

Your task to find the time taken to recieve signal from a satellite station K, to all N-1 satellite stations 
If it is impossible, return -1 .

Input Format:
-------------
Line-1 -> Three integers, N number of satellite stations, K is the satellite to send signal
          and T is the number of edges.
Next T lines -> Three space separated integers, 's' is the source, 'd' is the destination, 
			't' is the time taken recieve signal from 's' to 'd'.

Output Format:
--------------
Print an integer as your result.


Sample Input-1:
---------------
4 2 3
2 1 1
2 3 1
3 4 1

Sample Output-1:
----------------
2


Sample Input-2:
---------------
5 2 4
2 1 1
2 3 2
3 4 3
5 1 4

Sample Output-2:
----------------
-1

Sample Input-3:
---------------
5 2 4
2 1 1
2 3 2
3 4 3
1 5 6

Sample Output-3:
----------------
7

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SatelliteStations.java
> ```java
> /*
> Given N satellite stations, numbered 1 to N.
> These satellites are connected to send signals from one to other.
> To send a signal from satellite 's' to satellite 'd', it takes an amount of time 't'.
>
> You are given a list of travel times as directed edges times[i] = (s, d, t).
>
> Your task to find the time taken to recieve signal from a satellite station K, to all N-1 satellite stations 
> If it is impossible, return -1 .
>
> Input Format:
> -------------
> Line-1 -> Three integers, N number of satellite stations, K is the satellite to send signal
>           and T is the number of edges.
> Next T lines -> Three space separated integers, 's' is the source, 'd' is the destination, 
> 			't' is the time taken recieve signal from 's' to 'd'.
>
> Output Format:
> --------------
> Print an integer as your result.
>
>
> Sample Input-1:
> ---------------
> 4 2 3
> 2 1 1
> 2 3 1
> 3 4 1
>
> Sample Output-1:
> ----------------
> 2
>
>
> Sample Input-2:
> ---------------
> 5 2 4
> 2 1 1
> 2 3 2
> 3 4 3
> 5 1 4
>
> Sample Output-2:
> ----------------
> -1
>
> Sample Input-3:
> ---------------
> 5 2 4
> 2 1 1
> 2 3 2
> 3 4 3
> 1 5 6
>
> Sample Output-3:
> ----------------
> 7
>
> */
>
> import java.util.*;
>
> class SatelliteStations {
>     public static int travelTime(int[][] times, int N, int K) {
>         Map<Integer, Map<Integer,Integer>> map = new HashMap<>();
>         for(int[] time : times){
>             map.putIfAbsent(time[0], new HashMap<>());
>             map.get(time[0]).put(time[1], time[2]);
>         }
>         
>         //distance, node into pq
>         Queue<int[]> pq = new PriorityQueue<>((a,b) -> (a[0] - b[0]));
>         
>         pq.add(new int[]{0, K});
>         
>         boolean[] visited = new boolean[N+1];
>         int res = 0;
>         
>         while(!pq.isEmpty()){
>             int[] cur = pq.remove();
>             int curNode = cur[1];
>             int curDist = cur[0];
>             if(visited[curNode]) continue;
>             visited[curNode] = true;
>             res = curDist;
>             N--;
>             if(map.containsKey(curNode)){
>                 for(int next : map.get(curNode).keySet()){
>                     pq.add(new int[]{curDist + map.get(curNode).get(next), next});
>                 }
>             }
>         }
>         return N == 0 ? res : -1;
>             
>     }
> 	
> 	public static void main(String args[])
> 	{
> 		Scanner sc = new Scanner(System.in);
> 		int N=sc.nextInt();
> 		int K=sc.nextInt();
> 		int T=sc.nextInt();
> 		int[][] times=new int[T][3];
> 		for(int i=0;i<T;i++)
> 			for(int j=0;j<3;j++)
> 				times[i][j]=sc.nextInt();
> 		System.out.println(travelTime(times, N, K));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20113%20Solutions/SatelliteStations.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 113 Solutions/SatelliteStations.java
