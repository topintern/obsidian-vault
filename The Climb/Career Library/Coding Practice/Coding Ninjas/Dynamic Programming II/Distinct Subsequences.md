---
kind: "coding-problem"
title: "Distinct Subsequences"
collection: "Coding Ninjas"
topic: "Dynamic Programming II"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-2/distinct subsequences q.txt","CODING RESOURCES/coding ninjas/Dp-2/distinct subsequences s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Distinct Subsequences

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Given a string, count the number of distinct subsequences of it ( including empty subsequence ). For the uninformed, A subsequence of a string is a new string which is formed from the original string by deleting some of the characters without disturbing the relative positions of the remaining characters.
For example, "AGH" is a subsequence of "ABCDEFGH" while "AHG" is not.

### Input

First line of input contains an integer T which is equal to the number of test cases. You are required to process all test cases. Each of next T lines contains a string s.

### Output

Output consists of T lines. Ith line in the output corresponds to the number of distinct subsequences of ith input string. Since, this number could be very large, you need to output ans%1000000007 where ans is the number of distinct subsequences. 
Constraints and Limits
T = 100, length(S) = 100000

All input strings shall contain only uppercase letters.

### Sample Input

```text
3
AAA
ABCDEFG
CODECRAFT
```

### Sample Output

```text
4
128
496
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · distinct subsequences s.txt
> ```cpp
> #include <iostream>
> #include <cstdio>
> #include <string>
> #include <cstring>
> #include <algorithm>
> #define mod 1000000007
> #define MAX 100005
> using namespace std;
> long long int sum[MAX], dp[MAX];
> int main()
> {
>     int t, i, n, last[26];
>     string S;
>     scanf("%d", &t);
>     while(t--)
>     {
>         cin>>S;
>         n=S.size();
>         memset(last, -1, sizeof last);
>         dp[0]=1;
>         sum[0]=1;
>         dp[1]=1;
>         sum[1]=2;
>         last[S[0]-65]=1;
>         for(i=2;i<=n;i++)
>         {
>             dp[i]=sum[i-1];
>             if(last[S[i-1]-65]!=-1)
>                 dp[i]-=sum[last[S[i-1]-65]-1];
>             sum[i]=(sum[i-1]+dp[i])%mod;
>             if(sum[i]<0)
>             sum[i]+=mod;
>             last[S[i-1]-65]=i;
>         }
>         /*for(i=0;i<=n;i++)
>             printf("%lld ", dp[i]);
>         printf("\n");
>         for(i=0;i<=n;i++)
>             printf("%lld ", sum[i]);*/
>         printf("%lld\n", sum[n]);
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/distinct%20subsequences%20q.txt) · CODING RESOURCES/coding ninjas/Dp-2/distinct subsequences q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/distinct%20subsequences%20s.txt) · CODING RESOURCES/coding ninjas/Dp-2/distinct subsequences s.txt
