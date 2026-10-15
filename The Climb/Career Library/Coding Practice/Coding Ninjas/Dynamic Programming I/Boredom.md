---
kind: "coding-problem"
title: "Boredom"
collection: "Coding Ninjas"
topic: "Dynamic Programming I"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-1/boredom q.txt","CODING RESOURCES/coding ninjas/Dp-1/boredom s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Boredom

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Gary is bored and wants to play an interesting but tough game . So he figured out a new board game called "destroy the neighbours" . In this game there are N integers on a board. In one move, he can pick any integer x from the board and then all the integers with value x+1 or x-1 gets destroyed .This move will give him x points.
He plays the game until the board becomes empty . But as he want show this game to his friend Steven, he wants to learn techniques to maximise the points to show off . Can you help Gary in finding out the maximum points he receive grab from the game ?

### Input Format

Line 1 : Integer N 
Line 2 : A list of N integers

### Output Format

Maximum points Gary can recieve from the Game setup

### Constraints

1<=N<=10^5
1<=A[i]<=1000

### Sample Input

```text
2
1 2
```

### Sample Output

```text
2
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · boredom s.txt
> ```text
> int freq[1002],dp[1002];
> int solve(int n,vector<int>A)
> {
> 	for(int i=0;i<A.size();i++)
> 	{
> 		freq[A[i]]++; //count the frequency of each integer
> 	}
> 	dp[1]=freq[1]; //Dp[i] denotes the max points when i is the highest integer to be removed 
>     for(int i=2;i<=1000;i++)
>     {
>         dp[i]=max(dp[i-1],dp[i-2]+i*freq[i]);
>     }
>     return dp[1000];
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/boredom%20q.txt) · CODING RESOURCES/coding ninjas/Dp-1/boredom q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/boredom%20s.txt) · CODING RESOURCES/coding ninjas/Dp-1/boredom s.txt
