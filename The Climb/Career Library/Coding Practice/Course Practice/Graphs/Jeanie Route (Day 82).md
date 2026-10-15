---
kind: "coding-problem"
title: "Jeanie Route (Day 82)"
collection: "Course Practice"
topic: "Graphs"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 82 Solutions/JeanieRoute.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Jeanie Route (Day 82)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Input Format:
    - Line-1 contains two space-separated integers, C  and L, 
      the number of cities and the number of letters respectively.
    - Line-2 contains L space-separated integers 
      describing the delivery city for each letter.
    - Next C-1 lines contains 3 space-separated integers ui,vi,di
      di is the distance of the bidirectional road between cities ui and vi.

Output Format:
    - Print the minimum distance must travel to deliver all L letters.
    
    

### Sample Input

6 3
1 5 6
1 3 4
2 3 3
3 4 2
2 5 3
2 6 2


### Sample Output

14
*********Testcases************
case =1
input =5 3
1 3 4
1 2 1
2 3 2
2 4 2
3 5 3
output =6

case =2
input =6 3
3 4 6
1 2 5
1 3 4
1 4 6
2 5 3
2 6 2
output =21

case =3
input =6 3
1 2 5
1 3 4
1 4 6
2 5 3
2 6 2
1 2 4
output =7

case =4
input =6 3
1 5 6
1 3 4
2 3 3
3 4 2
2 5 3
2 6 2
output =14

case =5
input =5 3
1 3 5
1 2 2
2 3 3
2 4 4
1 5 5
output =10

case =6
input =20 5
5 11 12 16 15
17 4 3
11 12 5
14 2 1
16 14 4
7 8 4
13 5 5
17 15 2
5 3 5
8 6 1
18 10 4
18 1 3
16 1 2
9 2 5
11 6 1
4 9 4
7 20 2
13 19 3
19 12 3
10 20 2
output =54

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · JeanieRoute.txt
> ```java
> /*
> Input Format:
>     - Line-1 contains two space-separated integers, C  and L, 
>       the number of cities and the number of letters respectively.
>     - Line-2 contains L space-separated integers 
>       describing the delivery city for each letter.
>     - Next C-1 lines contains 3 space-separated integers ui,vi,di
>       di is the distance of the bidirectional road between cities ui and vi.
>
> Output Format:
>     - Print the minimum distance must travel to deliver all L letters.
>     
>     
> Sample Input:
> 6 3
> 1 5 6
> 1 3 4
> 2 3 3
> 3 4 2
> 2 5 3
> 2 6 2
>
> Sample Output:
> 14
>
>
> **********Testcases************
> case =1
> input =5 3
> 1 3 4
> 1 2 1
> 2 3 2
> 2 4 2
> 3 5 3
> output =6
>
> case =2
> input =6 3
> 3 4 6
> 1 2 5
> 1 3 4
> 1 4 6
> 2 5 3
> 2 6 2
> output =21
>
> case =3
> input =6 3
> 1 2 5
> 1 3 4
> 1 4 6
> 2 5 3
> 2 6 2
> 1 2 4
> output =7
>
> case =4
> input =6 3
> 1 5 6
> 1 3 4
> 2 3 3
> 3 4 2
> 2 5 3
> 2 6 2
> output =14
>
> case =5
> input =5 3
> 1 3 5
> 1 2 2
> 2 3 3
> 2 4 4
> 1 5 5
> output =10
>
> case =6
> input =20 5
> 5 11 12 16 15
> 17 4 3
> 11 12 5
> 14 2 1
> 16 14 4
> 7 8 4
> 13 5 5
> 17 15 2
> 5 3 5
> 8 6 1
> 18 10 4
> 18 1 3
> 16 1 2
> 9 2 5
> 11 6 1
> 4 9 4
> 7 20 2
> 13 19 3
> 19 12 3
> 10 20 2
> output =54
>
>
> */
> import java.io.*;
> import java.util.*;
> import java.text.*;
> import java.math.*;
> import java.util.regex.*;
>
> class EdgeJ implements Comparable<EdgeJ> {
> 	
> 	int end;
> 	int weight;
> 	
> 	EdgeJ(int end, int weight) {
> 		this.end = end;
> 		this.weight = weight;
> 	}
> 	
> 	public int compareTo(EdgeJ o) {
> 		
> 		return Integer.compare(this.weight, o.weight);
> 	}
> 	
> }
> public class JeanieRoute {
> 	static int max = 0;
> 	static int dfsMax(int start, int t, ArrayList<ArrayList<EdgeJ>> al, boolean[] l) {
> 		int currentMax = 0;
> 		
> 		int ix = -1;
> 		if(l[start]) {
> 			ix = start;
> 		}
> 		
> 		for(EdgeJ e : al.get(start)) {
> 			int v = e.end;
> 			
> 			if(v != t) {
> 				v = dfsMax(v, start, al, l);
> 				
> 				if(v != -1) {
> 					int current = max + e.weight;
> 					
> 					if(current > currentMax) {
> 						currentMax = current;
> 						ix = v;
> 					}
> 				}
> 			}
> 		}
> 		max = currentMax;
> 		return ix;
> 	}
> 	
> 	static int dfsSum(int start, int t, ArrayList<ArrayList<EdgeJ>> al, boolean[] l) {
> 		
> 		int sum = 0;
> 		
> 		for(EdgeJ e : al.get(start)) {
> 			int v = e.end;
> 			
> 			if(v != t) {
> 				sum = sum + dfsSum(v, start, al, l);
> 				if(l[v]) {
> 					l[start] = true;
> 					sum = sum + 2 * e.weight;
> 				}
> 			}
> 		}
> 		return sum;
> 	}
> 	public static void main(String [] args) {
> 		Scanner sc = new Scanner(System.in);
> 		
> 		int N = sc.nextInt();
> 		int K = sc.nextInt();
> 		
> 		boolean[] letter = new boolean[N];
> 		
> 		int startingP = 0;
> 		
> 		for(int i = 0; i < K; i++) {
> 			startingP = sc.nextInt() - 1;
> 			letter[startingP] = true;
> 		}
> 		
> 		ArrayList<ArrayList<EdgeJ>> adj = new ArrayList<ArrayList<EdgeJ>>();
> 		
> 		for(int i = 0; i < N; i++) {
> 			adj.add(new ArrayList<EdgeJ>());
> 		}
> 		
> 		for(int i = 0; i < N - 1; i++) {
> 			int x = sc.nextInt() - 1;
> 			int y = sc.nextInt() - 1;
> 			int z = sc.nextInt();
> 			
> 			adj.get(x).add(new EdgeJ(y, z));
> 			adj.get(y).add(new EdgeJ(x, z));
> 		}
> 		
> 		dfsMax(dfsMax(startingP, -1, adj, letter), -1, adj, letter);
> 		int temp2 = dfsSum(startingP, -1, adj, letter.clone());
> 		System.out.println(temp2 - max);
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2082%20Solutions/JeanieRoute.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 82 Solutions/JeanieRoute.txt
