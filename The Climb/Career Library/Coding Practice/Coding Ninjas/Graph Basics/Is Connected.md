---
kind: "coding-problem"
title: "Is Connected"
collection: "Coding Ninjas"
topic: "Graph Basics"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/4.Graphs-1/is connected q.txt","CODING RESOURCES/coding ninjas/4.Graphs-1/is connected s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Is Connected

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Given an undirected graph G(V,E), check if the graph G is connected graph or not.
V is the number of vertices present in graph G and vertices are numbered from 0 to V-1.
E is the number of edges present in graph G.

### Input Format

Line 1: Two Integers V and E (separated by space)
Next 'E' lines, each have two space-separated integers, 'a' and 'b', denoting that there exists an edge between Vertex 'a' and Vertex 'b'.

### Output Format

"true" or "false"

### Constraints

2 <= V <= 1000
1 <= E <= 1000

### Sample Input 1

```text
4 4
0 1
0 3
1 2
2 3
```

### Sample Output 1

```text
true
```

### Sample Input 2

```text
4 3
0 1
1 3 
0 3
```

### Sample Output 2

```text
false 
Sample Output 2 Explanation
The graph is not connected, even though vertices 0,1 and 3 are connected to each other but there isn’t any path from vertices 0,1,3 to vertex 2. 
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · is connected s.txt
> ```java
> import java.util.Scanner;
>
> public class Solution {
> 	
> 	public static void DFS(int[][] edges, int sv, boolean[] visited) {
> 		visited[sv] = true;
> 		for(int i = 0; i < edges.length; i++) {
> 			if(edges[sv][i] == 1 && !visited[i]) {
> 				DFS(edges, i, visited);
> 				visited[i] = true;
> 			}
> 		}
> 	}
> 	
> 	public static boolean isConnected(int[][] edges) {
> 		boolean[] visited = new boolean[edges.length];
> 		
> 		DFS(edges, 0, visited);
> 		
> 		for(int i = 0; i < visited.length; i++) {
> 			if(!visited[i]) {
> 				return false;
> 			}
> 		}
> 		
> 		return true;
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
> 		System.out.println(isConnected(edges));
> 	}
>
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/4.Graphs-1/is%20connected%20q.txt) · CODING RESOURCES/coding ninjas/4.Graphs-1/is connected q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/4.Graphs-1/is%20connected%20s.txt) · CODING RESOURCES/coding ninjas/4.Graphs-1/is connected s.txt
