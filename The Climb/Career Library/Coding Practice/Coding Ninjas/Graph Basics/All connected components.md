---
kind: "coding-problem"
title: "All connected components"
collection: "Coding Ninjas"
topic: "Graph Basics"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/4.Graphs-1/connected comps q.txt","CODING RESOURCES/coding ninjas/4.Graphs-1/connected comps s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# All connected components

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Given an undirected graph G(V,E), find and print all the connected components of the given graph G.
V is the number of vertices present in graph G and vertices are numbered from 0 to V-1.
E is the number of edges present in graph G.
You need to take input in main and create a function which should return all the connected components. And then print them in the main, not inside function.
Print different components in new line. And each component should be printed in increasing order (separated by space). Order of different components doesn't matter.

### Input Format

Line 1: Two Integers V and E (separated by space)
Next 'E' lines, each have two space-separated integers, 'a' and 'b', denoting that there exists an edge between Vertex 'a' and Vertex 'b'.

### Output Format

Different components in new line

### Constraints

2 <= V <= 1000
1 <= E <= 1000

### Sample Input 1

```text
4 2
0 1
2 3
```

### Sample Output 1

```text
0 1 
2 3 
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
0 1 3 
2
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · connected comps s.txt
> ```java
> import java.util.Scanner;
> import java.util.Map;
> import java.util.ArrayList;
> import java.util.Collections;
> import java.util.HashMap;
>
> class VertexOutOfRangeException extends Exception {
> 	public String toString() {
> 		return "Valid input for the vertex in specified range is expected!";
> 	}
> }
>
>
>
> public class Solution {
>
> 	public static void connectedComponents(Map<Integer, ArrayList<Integer>> adjacencyList, Map<Integer, Boolean> visited, ArrayList<Integer> smallOutput, int vertex)  {	
> 		smallOutput.add(vertex);
> 		visited.put(vertex, true);
> 		
> 		ArrayList<Integer> adjVerticies = adjacencyList.get(vertex);
> 		
> 		for(int i = 0; i < adjVerticies.size(); i++) {
> 			if(!visited.containsKey(adjVerticies.get(i))) {
> 				connectedComponents(adjacencyList, visited, smallOutput, adjVerticies.get(i));
> 			}
> 		}
> 	}
> 	
> 	public static ArrayList<ArrayList<Integer>> allConnectedComponents(Map<Integer, ArrayList<Integer>> adjacencyList) {
> 		Map<Integer, Boolean> visited = new HashMap<>();
> 		ArrayList<ArrayList<Integer>> output = new ArrayList<>();
> 		
> 		int i = 0;
> 		while(visited.size() != adjacencyList.size()) {
> 			while(i < adjacencyList.size()) {
> 				if(!visited.containsKey(i)) {
> 					ArrayList<Integer> smallOutput = new ArrayList<>();
> 					connectedComponents(adjacencyList, visited, smallOutput, i);
> 					output.add(smallOutput);
> 				}
> 				
> 				i += 1;
> 			}
> 		}
> 		
> 		return output;
> 	}
> 	
> 	
> 	public static void main(String[] args) throws VertexOutOfRangeException{
> 		Scanner s = new Scanner(System.in);
> 		int noOfVertices = s.nextInt();
> 		int noOfEdges = s.nextInt();
> 		
> 		Map<Integer, ArrayList<Integer>> adjacencyList = new HashMap<>();
> 		
> 		for(int i = 0; i < noOfVertices; i++) {
> 			adjacencyList.put(i, new ArrayList<>());
> 		}
> 		
> 		int currentEntry = 1;
> 		
> 		while(currentEntry <= noOfEdges) {
> 			int source = s.nextInt();
> 			int destination = s.nextInt();
> 			
> 			ArrayList<Integer> edgeListForDestination = adjacencyList.get(source);
> 			ArrayList<Integer> edgeListForSource = adjacencyList.get(destination);
> 			
> 			
> 			if(edgeListForDestination != null && edgeListForSource != null) {
> 				edgeListForDestination.add(destination);
> 				edgeListForSource.add(source);
> 			} else {
> 				s.close();
> 				throw new VertexOutOfRangeException();
> 			}
> 			
> 			currentEntry += 1;
> 		}
> 		
> 		ArrayList<ArrayList<Integer>> allConnectedComponents = allConnectedComponents(adjacencyList);
> 		
> 		for(int i = 0; i < allConnectedComponents.size(); i++) {
> 			ArrayList<Integer> components = allConnectedComponents.get(i);
> 			Collections.sort(components);
> 			
> 			for(int k = 0; k < components.size(); k++) {
> 				System.out.print(components.get(k) + " ");
> 			}
> 			System.out.println();
> 		}
> 		
> 		s.close();
> 	}
>
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/4.Graphs-1/connected%20comps%20q.txt) · CODING RESOURCES/coding ninjas/4.Graphs-1/connected comps q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/4.Graphs-1/connected%20comps%20s.txt) · CODING RESOURCES/coding ninjas/4.Graphs-1/connected comps s.txt
