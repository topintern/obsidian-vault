---
kind: "coding-problem"
title: "Maximum Sum Rectangle"
collection: "Coding Ninjas"
topic: "Dynamic Programming I"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-1/max rectangle q.txt","CODING RESOURCES/coding ninjas/Dp-1/max rectangle s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Maximum Sum Rectangle

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Given a 2D array, find the maximum sum rectangle in it. In other words find maximum sum over all rectangles in the matrix.

### Input

First line contains 2 numbers n and m denoting number of rows and number of columns. Next n lines contain m space separated integers denoting elements of matrix nxm.

### Output

Output a single integer, maximum sum rectangle.

### Constraints

1<=n,m<=100

### Sample Input

```text
4 5
1 2 -1 -4 -20
-8 -3 4 2 1
3 8 10 1 3
-4 -1 1 7 -6
```

### Sample Output

```text
29
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · max rectangle s.txt
> ```cpp
> #include <bits/stdc++.h>
>
> #define mod 1000000007
> #define inf 1000000000000LL
> #define root2 1.41421
> #define root3 1.73205
> #define pi 3.14159
> #define MAX 100001
> #define cntbit __builtin_popcountll
> #define ll long long int
> #define PII pair<int, int>
> #define f first
> #define s second
> #define mk make_pair
> #define PLL pair<ll, ll>
> #define gc getchar
> #define pb push_back
> using namespace std;
> ll M[101][101];
> ll kadane(vector<ll> v)
> {
>     int n=v.size();
>     int i, j;
>     ll ret=0, me=-inf, csum=0;
>     for(i=0;i<n;i++)
>     {
>         csum+=v[i];
>         if(csum<0)csum=0;
>         ret = max(ret, csum);
>         me=max(me, v[i]);
>     }
>     if(me<0)return me;
>     else return ret;
> }
> int main()
> {
>     ll mxsum=-inf, sum, i, j, k, n, m;
>     cin>>n>>m;
>     for(i=0;i<n;i++)
>     for(j=0;j<m;j++)
>         cin>>M[i][j];
>     for(int l=0;l<m;l++)
>     {
>         vector<ll> v(n, 0);
>         for(int r=l;r<m;r++)
>         {
>             for(i=0;i<n;i++)
>                 v[i]+=M[i][r];
>             mxsum=max(kadane(v), mxsum);
>         }
>     }
>     cout<<mxsum<<endl;
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/max%20rectangle%20q.txt) · CODING RESOURCES/coding ninjas/Dp-1/max rectangle q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/max%20rectangle%20s.txt) · CODING RESOURCES/coding ninjas/Dp-1/max rectangle s.txt
