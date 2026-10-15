---
kind: "coding-problem"
title: "The Asian Games (Day 48)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 48 Solutions/TheAsianGames.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# The Asian Games (Day 48)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

The Asian Games
-------------------------
The member of  Olympic Council of Asia (OCA) is planning to select people for the Asian Games. 
They want to choose two from different states. You will be given a list of pairs of athlete id's. 
Each pair is made of athletes from the same state. Determine how many pairs of athletes from 
different states they can choose from.
For example, we have the following data on 2 pairs of athletes, and 4 athletes total, numbered  
0 through 3.
ID State ID
1  2
2  3
athletes by state are [0] and [1,2,3]. There are 3 pairs to choose from:[0,1],[0,2] and [0,3].

Input Format:
-----------------
The first line contains two integers n and p, the number of athletes and the number of pairs.
Each of the p next lines contains 2 space-separated integers denoting athlete ID's of two who 
share the same state.


### Output Format

-------------
An integer that denotes the number of ways to choose a pair of athletes from different states.

Sample Input 1:
--------------
5 3
0 1
2 3
0 4

Sample Output 1:
---------------
6


### Explanation

Persons numbered [0,1,4] belong to one state, and those numbered [2,3] belong to another. 
The member has 6 ways of choosing a pair [0,2],[0,3],[1,2],[1,3],[4,2],[4,3]

Sample Input 2:
---------------
4 1
0 2

Sample Output 2:
----------------
5


### Explanation

Persons numbered [0,2] belong to one state. but persons 1 & 3 don't share states with anyone else.
The member has 5 ways of choosing a pair [0,1],[0,3],[2,1],[2,3],[1,3].



Algorithm:

We apply Depth First Search to calculate how many different connected components are present in the graph 
where the vertices are represented by the people and the people from the same state form one connected component. 
After we get how many connected components are present, say M, 
we just need to calculate the number of ways of selecting two persons from two different connected component. 
Let us assume that component i contains Mi people. 
So, for the number of ways selecting two persons from different components, 
we subtract the number of ways of selecting two persons from the same component 
from the total numbers of ways of selecting two persons 
i.e.
Ways = N choose 2 - (∑(Mi Choose 2) for i = 1 to M)


------------------------------------------------------

case = 1
input =6 4
0 1
2 3
4 5
0 2
output =8

case = 2
input =8 6
0 1
2 3
4 5
6 7
0 7
6 3
output =12

case = 3
input =10 5
0 1
2 5
1 4
5 6
4 7
output =36

case = 4
input =12 3
0 3
2 4
3 6
output =62

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · TheAsianGames.java
> ```java
> /*
>
> The Asian Games
> -------------------------
> The member of  Olympic Council of Asia (OCA) is planning to select people for the Asian Games. 
> They want to choose two from different states. You will be given a list of pairs of athlete id's. 
> Each pair is made of athletes from the same state. Determine how many pairs of athletes from 
> different states they can choose from.
> For example, we have the following data on 2 pairs of athletes, and 4 athletes total, numbered  
> 0 through 3.
> ID State ID
> 1  2
> 2  3
> athletes by state are [0] and [1,2,3]. There are 3 pairs to choose from:[0,1],[0,2] and [0,3].
>
> Input Format:
> -----------------
> The first line contains two integers n and p, the number of athletes and the number of pairs.
> Each of the p next lines contains 2 space-separated integers denoting athlete ID's of two who 
> share the same state.
>
> Output Format
> -------------
> An integer that denotes the number of ways to choose a pair of athletes from different states.
>
> Sample Input 1:
> --------------
> 5 3
> 0 1
> 2 3
> 0 4
>
> Sample Output 1:
> ---------------
> 6
>
> Explanation:
> Persons numbered [0,1,4] belong to one state, and those numbered [2,3] belong to another. 
> The member has 6 ways of choosing a pair [0,2],[0,3],[1,2],[1,3],[4,2],[4,3]
>
> Sample Input 2:
> ---------------
> 4 1
> 0 2
>
> Sample Output 2:
> ----------------
> 5
>
> Explanation:
> Persons numbered [0,2] belong to one state. but persons 1 & 3 don't share states with anyone else.
> The member has 5 ways of choosing a pair [0,1],[0,3],[2,1],[2,3],[1,3].
>
>
>
> Algorithm:
>
> We apply Depth First Search to calculate how many different connected components are present in the graph 
> where the vertices are represented by the people and the people from the same state form one connected component. 
> After we get how many connected components are present, say M, 
> we just need to calculate the number of ways of selecting two persons from two different connected component. 
> Let us assume that component i contains Mi people. 
> So, for the number of ways selecting two persons from different components, 
> we subtract the number of ways of selecting two persons from the same component 
> from the total numbers of ways of selecting two persons 
> i.e.
> Ways = N choose 2 - (∑(Mi Choose 2) for i = 1 to M)
>
>
> ------------------------------------------------------
>
> case = 1
> input =6 4
> 0 1
> 2 3
> 4 5
> 0 2
> output =8
>
> case = 2
> input =8 6
> 0 1
> 2 3
> 4 5
> 6 7
> 0 7
> 6 3
> output =12
>
> case = 3
> input =10 5
> 0 1
> 2 5
> 1 4
> 5 6
> 4 7
> output =36
>
> case = 4
> input =12 3
> 0 3
> 2 4
> 3 6
> output =62
>
>
> */
>
> import java.util.*;
>
> public class TheAsianGames {
> 	static List<List<Integer>> graph = new ArrayList<List<Integer>>();
> 	static boolean[] visited;
> 	static int vertices;
> 	
> 	public static void DFS(int u)
> 	{
> 	    visited[u] = true;
> 	    vertices++;
> 	    for(int adj : graph.get(u)) {
>             if (!visited[adj]) { 
>                 visited[adj] = true;
>                 DFS(adj);
>             }
>            }
> 	}
> 	
> 	
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         
>         /* write your code here */
>         int numComponents=0;
>         List<Integer> eachC =new ArrayList<Integer>();
>         
>         int n = in.nextInt();
>         int lines = in.nextInt();
>         
>         visited = new boolean[n];
>         for(int i=0;i<n;++i) {
>             visited[i] = false;
>             graph.add(new LinkedList<Integer>());
>         }
>         while(lines-->0) {
>             int a = in.nextInt();
>             int b = in.nextInt();
>             graph.get(b).add(a);
>             graph.get(a).add(b);
>         }
>         
>         //calculate numOfComponents in graph
>         //and number of nodes in each components
>         for(int i=0;i<n;i++)
>         {
>             if(!visited[i])
>             {
>                 vertices = 0;
>                 DFS(i);
>                 eachC.add(numComponents,vertices);
>                 numComponents++;
>             }
>         }
>         //this is based on the formula nC2
>         int totalWays = n*(n-1) / 2;
>         int sameWays = 0;//holds count of same state pairs
>         
>         for(int i=0;i<numComponents;i++)
>         {    
>             sameWays = sameWays + (eachC.get(i)*(eachC.get(i)-1) / 2);
>         }
>         System.out.println(totalWays - sameWays);
>         
>     }
> }
>
>
> /*
> =======Testcases=======
> case =1
> input =4 1
> 0 2
> output =5
>
> case =2
> input =5 3
> 0 1
> 2 3
> 0 4
> output =6
>
> case =3
> input =6 4
> 0 1
> 2 3
> 4 5
> 0 2
> output =8
>
> case =4
> input =8 6
> 0 1
> 2 3
> 4 5
> 6 7
> 0 7
> 6 3
> output =12
>
> case =5
> input =10 5
> 0 1
> 2 5
> 1 4
> 5 6
> 4 7
> output =36
>
> case =6
> input =12 3
> 0 3
> 2 4
> 3 6
> output =62
>
> case =7
> input =6 3
> 1 2
> 2 3
> 3 4
> output =9
>
> case =8
> input =8 3
> 0 1
> 2 3
> 4 5
> output =25
>
> case =9
> input =7 5
> 0 1
> 0 3
> 0 4
> 1 5
> 2 4
> output =6
>
> case =10
> input =6 3
> 0 1
> 1 4
> 4 5
> output =9
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2048%20Solutions/TheAsianGames.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 48 Solutions/TheAsianGames.java
