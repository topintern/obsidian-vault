---
kind: "coding-problem"
title: "Cheapest Flights Within KStops (Day 52)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 52 Solutions/CheapestFlightsWithinKStops.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Cheapest Flights Within KStops (Day 52)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

There are n cities connected by m flights. 
Each fight starts from city u and arrives at v with a price w.

Now given all the cities and flights, 
together with starting city src and the destination dst, 
your task is to find the cheapest price from src to dst with up to k stops. 
If there is no such route, output -1.

Note:

The number of nodes n will be in range [1, 100], with nodes labeled from 0 to n - 1.
The size of flights will be in range [0, n * (n - 1) / 2].
The format of each flight will be (src, dst, price).
The price of each flight will be in the range [1, 10000].
k is in the range of [0, n - 1].
There will not be any duplicated flights or self cycles.


Sample Input 1: 
3 3
0 1 100
1 2 100
0 2 500
0 2 1

Sample Output 1: 
200


### Explanation: 

The graph looks like this:
	       0
	  100 / \ 500
	     /	 \
	    1-----2
	      100
The cheapest price from city 0 to city 2 with at most 1 stop costs 200.

Sample Input 2: 
3 3
0 1 100
1 2 100
0 2 500
0 2 0

Sample Output 2: 
500


### Explanation: 

The graph looks like this:
	       0
	  100 / \ 500
	     /	 \
	    1-----2
	      100

The cheapest price from city 0 to city 2 with at most 0 stop costs 500.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · CheapestFlightsWithinKStops.txt
> ```java
> /*
>  * 
> There are n cities connected by m flights. 
> Each fight starts from city u and arrives at v with a price w.
>
> Now given all the cities and flights, 
> together with starting city src and the destination dst, 
> your task is to find the cheapest price from src to dst with up to k stops. 
> If there is no such route, output -1.
>
> Note:
>
> The number of nodes n will be in range [1, 100], with nodes labeled from 0 to n - 1.
> The size of flights will be in range [0, n * (n - 1) / 2].
> The format of each flight will be (src, dst, price).
> The price of each flight will be in the range [1, 10000].
> k is in the range of [0, n - 1].
> There will not be any duplicated flights or self cycles.
>
>
> Sample Input 1: 
> 3 3
> 0 1 100
> 1 2 100
> 0 2 500
> 0 2 1
>
> Sample Output 1: 
> 200
>
> Explanation: 
> The graph looks like this:
> 	       0
> 	  100 / \ 500
> 	     /	 \
> 	    1-----2
> 	      100
> The cheapest price from city 0 to city 2 with at most 1 stop costs 200.
>
> Sample Input 2: 
> 3 3
> 0 1 100
> 1 2 100
> 0 2 500
> 0 2 0
>
> Sample Output 2: 
> 500
>
> Explanation: 
> The graph looks like this:
> 	       0
> 	  100 / \ 500
> 	     /	 \
> 	    1-----2
> 	      100
>
> The cheapest price from city 0 to city 2 with at most 0 stop costs 500.
>
>  * 
>  * 
>  */
> import java.util.Arrays;
> import java.util.LinkedList;
> import java.util.Queue;
> import java.util.Scanner;
>
> public class CheapestFlightsWithinKStops {
>
> 	public static int findCheapestPrice(int n, int[][] adj, int src, int dst, int K) {
> 		if (src == dst) {
> 			return 0;
> 		}
> 		int[] dist = new int[n];
> 		Arrays.fill(dist, Integer.MAX_VALUE);
> 		Queue<Integer> queue = new LinkedList<>();
> 		queue.add(src);
> 		dist[src] = 0;
> 		int layOffs = 0;
> 		while (!queue.isEmpty() && layOffs <= K) {
> 			layOffs++;
> 			int size = queue.size();
> 			int[] distClone = Arrays.copyOf(dist, dist.length);
>
> 			for (int i = 0; i < size; i++) {
> 				int vertex = queue.poll();
> 				for (int j = 0; j < adj[vertex].length; j++) {
> 					if (adj[vertex][j] != 0) {
> 						if (dist[vertex] + adj[vertex][j] < distClone[j]) {
> 							distClone[j] = dist[vertex] + adj[vertex][j];
> 							queue.add(j);
> 						}
> 					}
> 				}
> 			}
> 			dist = distClone;
> 		}
> 		return dist[dst] == Integer.MAX_VALUE ? -1 : dist[dst];
> 	}
>
> 	public static void main(String args[]) {
>
> 		Scanner sc = new Scanner(System.in);
> 		int numOfCities = sc.nextInt();
> 		int numOfFlights = sc.nextInt();
>
> 		int[][] adj = new int[numOfCities][numOfCities];
> 		int u, v, price;
> 		for (int i = 0; i < numOfFlights; i++) {
> 			u = sc.nextInt();
> 			v = sc.nextInt();
> 			price = sc.nextInt();
> 			adj[u][v] = price;
> 		}
> 		int src = sc.nextInt();
> 		int dst = sc.nextInt();
> 		int K = sc.nextInt();
>
> 		System.out.println(findCheapestPrice(numOfCities, adj, src, dst, K));
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2052%20Solutions/CheapestFlightsWithinKStops.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 52 Solutions/CheapestFlightsWithinKStops.txt
