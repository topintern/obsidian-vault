---
kind: "coding-problem"
title: "Shortest Subsequence"
collection: "Coding Ninjas"
topic: "Dynamic Programming II"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-2/shortest subsequence q.txt","CODING RESOURCES/coding ninjas/Dp-2/shortest subsequence s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Shortest Subsequence

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Gary has two string S and V. Now Gary wants to know the length shortest subsequence in S such that it is not a subsequence in V.
Note: input data will be such so there will always be a solution.

### Input Format

Line 1 : String S of length N (1 <= N <= 1000)
Line 2 : String V of length M (1 <= M <= 1000)

### Output Format

Length of shortest subsequence in S such that it is not a subsequence in V

### Sample Input

```text
babab
babba
```

### Sample Output

```text
3
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · shortest subsequence s.txt
> ```text
> #define INF 1e9
>
> int solve(string S,string V){
> 	
> 	/*
> 		We establish the relationship between the sub problems and the problem at hand. 
> 		Let dp(i, j) be the length of the shortest subsequence that is in S[1..i] 
> 		that is not in V[1..j]. Here we have the following relationship:
> 		dp(i, j) =
> 		1. If letter S[i] is nowhere to be found in V[1..j], then dp(i,j) = 1.
> 		2. Otherwise, we have two case:
> 		    2.1. S[i] is in the shortest subsequence. We find k, the most immediate index in V[1..j] 
> 		    where V[k] == S[i]. Then dp(i, j) = 1 + dp(i-1, k-1).
> 		    2.2 S[i] is not in the shortest subsequence. Then dp(i, j) = dp(i-1, j).
> 		    We pick whichever is lower.
>
> 	*/
> 	
> 	int n = S.size(), m = V.size() ,i, j, prev;
> 	int dp[n+1][m+1] , next[n+1][m+1];
> 	
> 	for(i = 0; i < n; i++){
> 		prev = -1;
> 		for(j = 0;j < m; j++){
> 			if(S[i] == V[j])
> 				prev = j;
> 			next[i+1][j+1] = prev;
> 		}
> 	}
> 	
> 	for(i = 1; i <= n; i++)
> 		dp[i][0] = 1;
> 	
> 	for(i = 0; i <= m; i++){
> 		dp[0][i] = INF;
> 	}
> 	
> 	for(i = 1; i <= n; i++){
> 		for(j = 1; j <= m; j++){
> 			if(next[i][j] == -1)
> 				dp[i][j] = 1;
> 			else{
> 				dp[i][j] = min(dp[i-1][j],1 + dp[i-1][next[i][j]]);
> 			}
> 		}
> 	}
>
> 	return dp[n][m];
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/shortest%20subsequence%20q.txt) · CODING RESOURCES/coding ninjas/Dp-2/shortest subsequence q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/shortest%20subsequence%20s.txt) · CODING RESOURCES/coding ninjas/Dp-2/shortest subsequence s.txt
