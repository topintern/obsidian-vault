---
kind: "coding-problem"
title: "Rust Murderer (Day 50)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 50 Solutions/RustMurderer.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Rust Murderer (Day 50)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Detective Rust is investigating a homicide and he wants to chase down the murderer. 
The murderer knows he would definitely get caught if he takes the main roads for fleeing, 
so he uses the village roads (or side lanes) for running away from the crime scene.

Rust knows that the murderer will take village roads and he wants to chase him down. 
He is observing the city map, but it doesn't show the village roads (or side lanes) 
on it and shows only the main roads.

The map of the city is a graph consisting N nodes (labeled 1 to N) where a specific 
given node S represents the current position of Rust and the rest of the nodes denote 
other places in the city, and an edge between two nodes is a main road between two 
places in the city. It can be suitably assumed that an edge that doesn't exist/isn't 
shown on the map is a village road (side lane).
That means, there is a village road between two nodes a and b iff(if and only if) 
there is no city road between them.

In this problem, distance is calculated as number of village roads (side lanes)
between any two places in the city.

Rust wants to calculate the shortest distance from his position (Node S) to all 
the other places in the city if he travels only using the village roads (side lanes).

Note: The graph/map of the city is ensured to be a sparse graph.



### Input Format

------------
 - First line has two integers N, denoting the number of cities in the map
and M, denoting the number of roads in the map.
 - The next M lines each consist of two space-separated integers x and y denoting a main 
road between city x and city y. 
 - The last line has an integer S, denoting the current position of Rust. 

Note
----
No nodes will have a road to itself.
There will not be multiple edges between any pair of nodes i.e. 
there is at most one undirected edge between them.
It is guranteed that there will be a path between any pair of nodes using the side lanes.


### Output Format

-------------
Print a single line consisting of N-1 space separated integers, 
denoting the shortest distances of the remaining N-1 places from Rust's position 
(that is all distances, except the source node to itself) using the village roads/side lanes 
in ascending order based on vertex number. 


### Sample Input: 

4 3
1 2
2 3
1 4
1

### Sample Output

3 1 2


### Explanation:
		

Graph shown like below
 S
(1)-------(4)
 |
 |
(2)-------(3)

Here the source node is 1 (marked S).
The distance from 1 to 2 is 3. Path: 1 -> 3 -> 4 -> 2
The distance from 1 to 3 is 1. Path: 1 -> 3
The distance from 1 to 4 is 2. Path: 1 -> 3 -> 4

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · RustMurderer.java
> ```java
> /*
> Detective Rust is investigating a homicide and he wants to chase down the murderer. 
> The murderer knows he would definitely get caught if he takes the main roads for fleeing, 
> so he uses the village roads (or side lanes) for running away from the crime scene.
>
> Rust knows that the murderer will take village roads and he wants to chase him down. 
> He is observing the city map, but it doesn't show the village roads (or side lanes) 
> on it and shows only the main roads.
>
> The map of the city is a graph consisting N nodes (labeled 1 to N) where a specific 
> given node S represents the current position of Rust and the rest of the nodes denote 
> other places in the city, and an edge between two nodes is a main road between two 
> places in the city. It can be suitably assumed that an edge that doesn't exist/isn't 
> shown on the map is a village road (side lane).
> That means, there is a village road between two nodes a and b iff(if and only if) 
> there is no city road between them.
>
> In this problem, distance is calculated as number of village roads (side lanes)
> between any two places in the city.
>
> Rust wants to calculate the shortest distance from his position (Node S) to all 
> the other places in the city if he travels only using the village roads (side lanes).
>
> Note: The graph/map of the city is ensured to be a sparse graph.
>
>
> Input Format
> ------------
>  - First line has two integers N, denoting the number of cities in the map
> and M, denoting the number of roads in the map.
>  - The next M lines each consist of two space-separated integers x and y denoting a main 
> road between city x and city y. 
>  - The last line has an integer S, denoting the current position of Rust. 
>
> Note
> ----
> No nodes will have a road to itself.
> There will not be multiple edges between any pair of nodes i.e. 
> there is at most one undirected edge between them.
> It is guranteed that there will be a path between any pair of nodes using the side lanes.
>
> Output Format
> -------------
> Print a single line consisting of N-1 space separated integers, 
> denoting the shortest distances of the remaining N-1 places from Rust's position 
> (that is all distances, except the source node to itself) using the village roads/side lanes 
> in ascending order based on vertex number. 
>
> Sample Input: 
> 4 3
> 1 2
> 2 3
> 1 4
> 1
> Sample Output:
> 3 1 2
>
> Explanation:
> 		
> Graph shown like below
>  S
> (1)-------(4)
>  |
>  |
> (2)-------(3)
>
> Here the source node is 1 (marked S).
> The distance from 1 to 2 is 3. Path: 1 -> 3 -> 4 -> 2
> The distance from 1 to 3 is 1. Path: 1 -> 3
> The distance from 1 to 4 is 2. Path: 1 -> 3 -> 4 
>
>  * 
>  */
>
> import java.util.ArrayList;
> import java.util.Scanner;
>
> public class RustMurderer {
>
> 	static ArrayList<Integer>[] roads;
> 	static private int[] distance;
> 	static private int[] state;
>
> 	public static void main(String[] args) {
>
> 		Scanner sc = new Scanner(System.in);
>
> 		int numOfCities = sc.nextInt();
> 		int numOfRoads = sc.nextInt();
>
> 		roads = new ArrayList[numOfCities];
>
> 		for (int j = 0; j < numOfCities; j++) {
> 			roads[j] = new ArrayList<Integer>();
> 		}
> 		for (int j = 0; j < numOfRoads; j++) {
>
> 			int city1 = sc.nextInt() - 1;
> 			int city2 = sc.nextInt() - 1;
>
> 			roads[city1].add(city2);
> 			roads[city2].add(city1);
> 		}
>
> 		int s = sc.nextInt() - 1;// current position of Rust
> 		int shortDistance[] = breadthFirstSearch(s);
>
> 		for (int j = 0; j < shortDistance.length; j++) {
> 			if (j == s) {// skip distance to current position of Rust
> 				continue;
> 			}
> 			System.out.print(shortDistance[j] + " ");
> 		}
>
> 	}
>
> 	static int[] breadthFirstSearch(int s) {
>
> 		java.util.LinkedList<Integer> q = new java.util.LinkedList<Integer>();
> 		distance = new int[roads.length];
> 		state = new int[roads.length];
> 		for (int i = 0; i < roads.length; i++) {
> 			state[i] = -1;
> 			distance[i] = -1;
> 		}
> 		q.add(s);
> 		state[s] = 0;
> 		distance[s] = 0;
>
> 		while (q.size() != 0) {
> 			int hold = q.removeFirst();
> 			// take the city(hold) and find the side lanes from city hold to other cities
> 			// cities.
> 			for (int i = 0; i < roads.length; i++) {
>
> 				// check whether the current city(i) is already covered or not and
> 				// check whether the road is available or not
> 				//if city is not covered and has side lane to the city then
> 				if (state[i] == -1 && !roads[hold].contains(i)) {
>
> 					q.add(i);// add the city(i) to the queue, which has village road and not covered yet.
> 					state[i] = 0;
> 					distance[i] = distance[hold] + 1;// updated the distance of current city
>
> 				}
> 			}
> 			state[hold] = 1;// mark the current city(hold) as 1
> 			for (int i = 0; i < distance.length; i++) {
> 				if (distance[i] == -1) {// need to calculate side lane to 'i'
> 					break;
> 				}
> 				if (i == distance.length - 1) {// if all village distances are calculated
> 					return distance;
> 				}
> 			}
> 		}
> 		return distance;
> 	}
> }
>
>
> /*
> ========= Testcases Program-1 =========
> case=1
> input=4 2
> 1 2
> 2 3
> 2
> output=2 2 1
>
> case=2
> input=5 3
> 1 2
> 1 5
> 3 4
> 1
> output=2 1 1 2
>
> case=3
> input=5 4
> 1 2
> 1 3
> 2 4
> 2 5
> 2
> output=3 1 2 2
>
> case=4
> input=5 4
> 1 2
> 1 3
> 2 4
> 2 5
> 3
> output=2 1 1 1
>
> case =5
> input =4 3
> 1 2
> 2 3
> 1 4
> 1
> output =3 1 2
>
> case =6
> input =6 5
> 1 2
> 2 3
> 3 4
> 4 5
> 5 6
> 2
> output =2 2 1 1 1
>
> case =7
> input =7 5
> 1 4
> 2 5
> 6 2
> 3 6
> 4 7
> 3
> output =1 1 1 1 2 1
>
> case =8
> input =8 6
> 2 6
> 3 1
> 1 4
> 5 7
> 4 8
> 7 2
> 1
> output =1 2 2 1 1 1 1
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2050%20Solutions/RustMurderer.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 50 Solutions/RustMurderer.java
