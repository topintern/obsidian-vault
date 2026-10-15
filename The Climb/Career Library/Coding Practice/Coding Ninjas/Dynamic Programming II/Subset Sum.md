---
kind: "coding-problem"
title: "Subset Sum"
collection: "Coding Ninjas"
topic: "Dynamic Programming II"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-2/subset sum q.txt","CODING RESOURCES/coding ninjas/Dp-2/subset sum s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Subset Sum

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Given a set of n integers, find if a subset of sum k can be formed from the given set. Print Yes or No.

### Input Format

First line contains a single integer n (1<=n<=1000)
Second line contains n space separated integers (1<=a[i]<=1000)
Last line contains a single positive integer k (1<=k<=1000)

### Output Format

Output Yes if there exists a subset whose sum is k, else output No.

### Sample Input

```text
3
1 2 3
4
```

### Sample Output

```text
YES
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · subset sum s.txt
> ```cpp
> #include <bits/stdc++.h>
> #define MAX 1001
> using namespace std;
> bool dp[MAX][MAX];
> //dp[i][j] is true if we can create a subset sum of j from first i elements
> int main()
> {
>     int n, i, sum;
>     cin>>n;
>     vector<int> a(n+1);
>     for(i=1;i<=n;i++)cin>>a[i];
>     cin>>sum;
>     // If sum is 0, then answer is true
>     for (int i = 0; i <= n; i++)
>         dp[i][0] = true;
>
>     // If sum is not 0 and set is empty, then answer is false
>     for (int i = 1; i <= sum; i++)
>         dp[0][i] = false;
>
>     // Fill the table in bottom up manner
>     for (int i = 1; i <= n; i++)
>     {
>         for (int j = 1; j <= sum; j++)
>         {
>             //Can we create sum by excluding current element
>             dp[i][j] = dp[i-1][j];
>             //Can we create sum by including current element
>             if(j-a[i]>=0)
>                 dp[i][j] |= dp[i-1][j-a[i]];
>        }
>     }
>     if(dp[n][sum])cout<<"Yes";
>     else cout<<"No";
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/subset%20sum%20q.txt) · CODING RESOURCES/coding ninjas/Dp-2/subset sum q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/subset%20sum%20s.txt) · CODING RESOURCES/coding ninjas/Dp-2/subset sum s.txt
