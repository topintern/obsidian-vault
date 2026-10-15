---
kind: "coding-problem"
title: "BFS Traversal"
collection: "Coding Ninjas"
topic: "Graph Basics"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/4.Graphs-1/bfs q.txt","CODING RESOURCES/coding ninjas/4.Graphs-1/bfs s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# BFS Traversal

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Given an undirected and connected graph G(V, E), print its BFS traversal.
Here you need to consider that you need to print BFS path starting from vertex 0 only.
V is the number of vertices present in graph G and vertices are numbered from 0 to V-1.
E is the number of edges present in graph G.
Note : 1. Take graph input in the adjacency matrix.
2. Handle for Disconnected Graphs as well

### Input Format

Line 1: Two Integers V and E (separated by space)
Next 'E' lines, each have two space-separated integers, 'a' and 'b', denoting that there exists an edge between Vertex 'a' and Vertex 'b'.

### Output Format

BFS Traversal (separated by space)

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
0 1 3 2
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · bfs s.txt
> ```cpp
> #include <queue>
> #include <iostream>
> #include <unordered_map>
> using namespace std;
>
> void printBFS(int** edges, int n, int sv, bool* visited) {
> 	queue<int> pendingVertices;
> 	pendingVertices.push(sv);        
> 	visited[sv] = true;
> 	while (!pendingVertices.empty()) {
> 		int currentVertex = pendingVertices.front();
> 		pendingVertices.pop();
> 		cout << currentVertex << " " ;
> 		for (int i = 0; i < n; i++) {
> 			if (i == currentVertex) {
> 				continue;
> 			}
> 			if (edges[currentVertex][i] == 1 && !visited[i]) {
> 				pendingVertices.push(i);
> 				visited[i] = true;
> 			}
> 		}
> 	}
> }
>
> void BFS(int** edges, int n) {
> 	bool * visited = new bool[n];
> 	for (int i = 0; i < n; i++) {
> 		visited[i] = false;
> 	}
>
> 	for(int i = 0; i < n; i++) {
> 		if(!visited[i]) {
> 			printBFS(edges, n, i, visited);
> 		}
> 	}
> 	delete [] visited;
> }
>
> int main() {
> 	int n;
> 	int e;
> 	cin >> n >> e;
> 	int** edges = new int*[n];
> 	for (int i = 0; i < n; i++) {
> 		edges[i] = new int[n];
> 		for (int j = 0; j < n; j++) {
> 			edges[i][j] = 0;
> 		}
> 	}
>
> 	for (int i = 0; i < e; i++) {
> 		int f, s;
> 		cin >> f >> s;
> 		edges[f][s] = 1;
> 		edges[s][f] = 1;
> 	}
>
>  	BFS(edges, n);
>
> 	for (int i = 0; i < n; i++) {
> 		delete [] edges[i];
> 	}
> 	delete [] edges;
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/4.Graphs-1/bfs%20q.txt) · CODING RESOURCES/coding ninjas/4.Graphs-1/bfs q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/4.Graphs-1/bfs%20s.txt) · CODING RESOURCES/coding ninjas/4.Graphs-1/bfs s.txt
