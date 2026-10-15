---
kind: "coding-problem"
title: "Has Path"
collection: "Coding Ninjas"
topic: "Graph Basics"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/4.Graphs-1/has path q.txt","CODING RESOURCES/coding ninjas/4.Graphs-1/has path s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Has Path

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Given an undirected graph G(V, E) and two vertices v1 and v2(as integers), check if there exists any path between them or not. Print true or false.
V is the number of vertices present in graph G and vertices are numbered from 0 to V-1.
E is the number of edges present in graph G.

### Input Format

Line 1: Two Integers V and E (separated by space)
Next E lines : Two integers a and b, denoting that there exists an edge between vertex a and vertex b (separated by space)
Line (E+2) : Two integers v1 and v2 (separated by space)

### Output Format

true or false

### Constraints

2 <= V <= 1000
1 <= E <= 1000
0 <= v1, v2 <= V-1

### Sample Input 1

```text
4 4
0 1
0 3
1 2
2 3
1 3
```

### Sample Output 1

```text
true
```

### Sample Input 2

```text
6 3
5 3
0 1
3 4
0 3
```

### Sample Output 2

```text
false
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · has path s.txt
> ```java
> import java.util.LinkedList;
> import java.util.Queue;
> import java.util.Scanner;
>
> public class Solution {
> 	
> 	public static boolean BFS(int edges[][], int sv, int ev, boolean visited[]) {
> 		if(edges[sv][ev] == 1) {
> 			return true;
> 		}
> 		
> 		Queue<Integer> queue = new LinkedList<>();
> 		visited[sv] = true;
> 		queue.add(sv);
> 		
> 		while(!queue.isEmpty()) {
> 			int front = queue.remove();
> 			
> 			for(int i = 0; i < edges.length; i++) {
> 				if(edges[front][i] == 1 && !visited[i]) {
> 					if(i == ev)
> 						return true;
> 					else {
> 						visited[i] = true;
> 						queue.add(i);
> 					}
> 				} 
> 			}
> 		}
> 		return false;
> 	}
> 	
> 	private static boolean hasPath(int[][] edges, int sv, int ev) {
> 		boolean visited[] = new boolean[edges.length];
> 		return BFS(edges, sv, ev, visited);
> 	}
> 	
> 	public static void main(String[] args) {
> 		int n;
> 		int e;
>
> 		Scanner s = new Scanner(System.in);
> 		n = s.nextInt();
> 		e = s.nextInt();
> 		int edges[][] = new int[n][n];
>
> 		for(int i = 0; i < e; i++) {
> 			int fv = s.nextInt();
> 			int sv = s.nextInt();
> 			edges[fv][sv] = 1;
> 			edges[sv][fv] = 1;
> 		}
> 		
> 		int sv = s.nextInt();
> 		int ev = s.nextInt();
> 		
> 		s.close();
> 		
> 		System.out.println(hasPath(edges, sv, ev));
> 	}
>
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/4.Graphs-1/has%20path%20q.txt) · CODING RESOURCES/coding ninjas/4.Graphs-1/has path q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/4.Graphs-1/has%20path%20s.txt) · CODING RESOURCES/coding ninjas/4.Graphs-1/has path s.txt
