---
kind: "coding-problem"
title: "Relation Chains (Day 121)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 121 Solutions/RelationChains.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Relation Chains (Day 121)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

There are P people in a Village, some of the people are relatives, others are not. 
Their relationship is transitive in nature. 
For example, 
if A is a direct relative of B, and B is a direct relative of C, then A is an indirect relative of C.
And we define a Relation Chain is a group of people who are direct or indirect relatives.

Given a P*P matrix R representing the relationship between people in the village. 
If R[i][j] = 1, then the i and j persons are direct relatives with each other, otherwise not. 

Your task is to findout the total number of Relation Chains among all the people.

Input Format:
-------------
Line-1 : An integer P, number of people
Next P lines : P space separated integers.

Output Format:
--------------
Print an integer, the total number of Relation Chains


Sample Input-1:
---------------
3
1 1 0
1 1 0
0 0 1

Sample Output-1:
----------------
2


### Explanation

------------
The 0-th and 1-st people are direct relatives, so they are in a relation chain.
The 2-nd person himself is in a relation chain. So return 2.


Sample Input-2:
---------------
3
1 1 0
1 1 1
0 1 1

Sample Output-2:
----------------
1


### Explanation

------------
The 0-th and 1-st people are direct relatives, 1-st and 2-nd people are direct relatives.
So, the 0-th and 2-nd people are indirect relatives.
All of them in the same relative chain. So return 1.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · RelationChains.java
> ```java
> /*
> There are P people in a Village, some of the people are relatives, others are not. 
> Their relationship is transitive in nature. 
> For example, 
> if A is a direct relative of B, and B is a direct relative of C, then A is an indirect relative of C.
> And we define a Relation Chain is a group of people who are direct or indirect relatives.
>
> Given a P*P matrix R representing the relationship between people in the village. 
> If R[i][j] = 1, then the i and j persons are direct relatives with each other, otherwise not. 
>
> Your task is to findout the total number of Relation Chains among all the people.
>
> Input Format:
> -------------
> Line-1 : An integer P, number of people
> Next P lines : P space separated integers.
>
> Output Format:
> --------------
> Print an integer, the total number of Relation Chains
>
>
> Sample Input-1:
> ---------------
> 3
> 1 1 0
> 1 1 0
> 0 0 1
>
> Sample Output-1:
> ----------------
> 2
>
> Explanation:
> ------------
> The 0-th and 1-st people are direct relatives, so they are in a relation chain.
> The 2-nd person himself is in a relation chain. So return 2.
>
>
> Sample Input-2:
> ---------------
> 3
> 1 1 0
> 1 1 1
> 0 1 1
>
> Sample Output-2:
> ----------------
> 1
>
> Explanation:
> ------------
> The 0-th and 1-st people are direct relatives, 1-st and 2-nd people are direct relatives.
> So, the 0-th and 2-nd people are indirect relatives.
> All of them in the same relative chain. So return 1.
>
> */
> import java.util.*;
>
> public class RelationChains {
>     public void dfs(int[][] R, int[] visited, int i) {
>         for (int j = 0; j < R.length; j++) {
>             if (R[i][j] == 1 && visited[j] == 0) {
>                 visited[j] = 1;
>                 dfs(R, visited, j);
>             }
>         }
>     }
>     public int findChainNum(int[][] R) {
>         int[] visited = new int[R.length];
>         int count = 0;
>         for (int i = 0; i < R.length; i++) {
>             if (visited[i] == 0) {
>                 dfs(R, visited, i);
>                 count++;
>             }
>         }
>         return count;
>     }
> 	
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		int p=sc.nextInt();
> 		int r[][]=new int[p][p];
> 		for(int i=0;i<p;i++)
> 			for(int j=0;j<p;j++)
> 				r[i][j] = sc.nextInt();
> 		System.out.println(new RelationChains().findChainNum(r));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20121%20Solutions/RelationChains.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 121 Solutions/RelationChains.java
