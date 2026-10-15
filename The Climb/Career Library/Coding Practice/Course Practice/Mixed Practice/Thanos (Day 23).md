---
kind: "coding-problem"
title: "Thanos (Day 23)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/ELITE DAY 23 SOLUTIONS/Thanos.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Thanos (Day 23)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Algorithm(DFS):
In this problem you are given an undirected graph with weighted vertices. 
Store the pair of weight of the vertex and its position in a vector V or a List Zakos. 
Then create adjacency representation for all edges. 
Sort the vector V or List Zakos ,in non-decreasing order, so that we get vertex with minimum weights.
Now for each connected component run DFS and simultaneously add the minimum weight vertex to final answer. 

Sample Input 1:

5 2
2 5 3 4 8
1 4
4 5

Sample Output 1:

10


### Explanation:


Here the best decision is to pay the first Zakos (2)
(he will spread the news to fourth character, and the fourth one will spread it to fifth).
 Also Thanos has to pay the second(5) and the third Zakos(3), so they know the news and spread it in their territory.
 the minimum amount of gold Thanos has to spend in order to find all infinity stones is 10(2+5+3).

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Thanos.java
> ```java
> /*
>  * 
> Algorithm(DFS):
> In this problem you are given an undirected graph with weighted vertices. 
> Store the pair of weight of the vertex and its position in a vector V or a List Zakos. 
> Then create adjacency representation for all edges. 
> Sort the vector V or List Zakos ,in non-decreasing order, so that we get vertex with minimum weights.
> Now for each connected component run DFS and simultaneously add the minimum weight vertex to final answer. 
>
> Sample Input 1:
>
> 5 2
> 2 5 3 4 8
> 1 4
> 4 5
>
> Sample Output 1:
>
> 10
>
> Explanation:
>
> Here the best decision is to pay the first Zakos (2)
> (he will spread the news to fourth character, and the fourth one will spread it to fifth).
>  Also Thanos has to pay the second(5) and the third Zakos(3), so they know the news and spread it in their territory.
>  the minimum amount of gold Thanos has to spend in order to find all infinity stones is 10(2+5+3).
>  
>  * 
>  * 
>  */
> import java.util.ArrayList;
> import java.util.Collections;
> import java.util.Iterator;
> import java.util.LinkedList;
> import java.util.List;
> import java.util.Scanner;
>
> class Pair implements Comparable<Pair> 
> {
> 	private int index,value;
> 	Pair(int index,int value){
> 		this.index = index;
> 		this.value = value;
> 	}
> 	int getIndex() {
> 		return this.index;
> 	}
> 	int getValue() {
> 		return this.value;
> 	}
> 	// Used to sort values in ascending order
>     public int compareTo(Pair p) 
>     { 
>         return this.value - p.value; 
>     } 
>
> }
> public class vaThanos {
>
> 	private boolean visited[];
> 	private int V;
> 	// Array of lists for Adjacency List Representation 
> 	private LinkedList<Integer> adj[]; 
>
> 		
> 		// Constructor 
> 		Thanos(int v) 
> 		{ 
> 			V = v; 
> 			adj = new LinkedList[v]; 
> 			for (int i=0; i<v; ++i) 
> 				adj[i] = new LinkedList(); 
> 		} 
> 		
> 		//Function to add an edge into the graph 
> 		void addEdge(int v, int w) 
> 		{ 
> 			adj[v].add(w); // Add w to v's list. 
> 			adj[w].add(v); // Add w to v's list. 
>
>  
> 		} 
> 	
> 		// A function used by DFS 
> 		void dfs(int v,boolean visited[]) 
> 		{ 
> 			// Mark the current node as visited and print it 
> 			visited[v] = true; 
> 			
> 			// Recur for all the vertices adjacent to this vertex 
> 			Iterator<Integer> i = adj[v].listIterator(); 
> 			while (i.hasNext()) 
> 			{ 
> 				int n = i.next(); 
> 				if (!visited[n]) 
> 					dfs(n, visited); 
> 			} 
> 		} 
> 	
> 	
> 	public static void main(String args[]) {
> 		
> 		Scanner sc = new Scanner(System.in);
> 		int numOfZakos = sc.nextInt();
> 		int numOfFriendShips = sc.nextInt();
> 		List Zakos = new ArrayList<Pair>();
> 		
> 		for(int i = 0 ; i < numOfZakos ; i++){
> 			Pair p = new Pair(i,sc.nextInt());
> 	        Zakos.add(p);
> 	    }
> 		
> 		Collections.sort(Zakos);
> 		
> 		Thanos g = new Thanos(numOfZakos); 
>
> 		for(int i=0;i<numOfFriendShips;i++) {
> 			g.addEdge(sc.nextInt()-1,sc.nextInt()-1); 
> 		}
> 		
> 		int minAmountOfGold = 0;
> 		
> 		// Mark all the vertices as not visited(set as false by default in java) 
> 		boolean visited[] = new boolean[numOfZakos]; 
> 		
> 	    for(int i = 0 ; i < numOfZakos ; ++i){
> 	    	Pair curr = (Pair) Zakos.get(i);
> 	        if(!visited[curr.getIndex()]){
> 	        	minAmountOfGold += curr.getValue();
> 	            g.dfs(curr.getIndex(),visited);
> 	        }
> 	    }
> 	    
> 	    System.out.println(minAmountOfGold);
> 					
> 		
> 	}
> 	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/ELITE%20DAY%2023%20SOLUTIONS/Thanos.java) · CODING RESOURCES/ELITE FS COMPLETE/ELITE DAY 23 SOLUTIONS/Thanos.java
