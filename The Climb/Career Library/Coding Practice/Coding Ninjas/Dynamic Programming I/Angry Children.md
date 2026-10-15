---
kind: "coding-problem"
title: "Angry Children"
collection: "Coding Ninjas"
topic: "Dynamic Programming I"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-1/angry child q.txt","CODING RESOURCES/coding ninjas/Dp-1/angry child s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Angry Children

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Bill Gates is on one of his philanthropic journeys to a village in Utopia. He has N packets of candies and would like to distribute one packet to each of the K children in the village (each packet may contain different number of candies). To avoid a fight between the children, he would like to pick K out of N packets such that the unfairness is minimized.
Suppose the K packets have (x1, x2, x3,....xk) candies in them, where xi denotes the number of candies in the ith packet, then we define unfairness as
unfairness=0;
for(i=0;i<n;i++)
for(j=0;j<n;j++)
    unfairness+=abs(xi-xj)
abs(x) denotes absolute value of x.

### Input Format

The first line contains an integer N.
The second line contains an integer K.
N lines follow each integer containing the candy in the ith packet.

### Output Format

A single integer which will be minimum unfairness.

### Constraints

2<=N<=10^5

2<=K<=N

0<= number of candies in each packet <=10^9

### Sample Input

```text
7
3
10
100
300
200
1000
20
30
```

### Sample Output

```text
40
```

### Explanation

Bill Gates will choose packets having 10, 20 and 30 candies.So unfairness will be |10-20| + |20-30| + |10-30| = 40. We can verify that it will be minimum in this way.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · angry child s.txt
> ```cpp
> #include <bits/stdc++.h>
> #define ll long long
> using namespace std;
>
> ll A[100001];
> void solve(ll n, ll k) {
>     sort(A, A+n);
>     vector<ll> sum(n+1, 0);
>     ll c=0, ans=-1, z;
>     int i;
>     sum[0]=0;
>     for(i=0;i<n;i++)
>         sum[i+1]=sum[i]+A[i];
>     for(i=0;i<k;i++)
>         c+=A[i]*(2*i+1);
>     for(i=0;i+k<=n;i++)
>     {
>         //k numbers starting from i;
>         z=c-k*(sum[k+i]-sum[i]);
>         //cout<<z<<" "<<c<<" "<<sum[k+i]-sum[i]<<endl;
>         if(ans==-1)
>             ans=z;
>         else
>             ans=min(z, ans);
>         //change c for next iteration
>         if(i+k<=n)
>         c=c-2*(sum[k+i]-sum[i+1])-A[i]+(2*k-1)*A[i+k];
>     }
>     cout<<ans;
> }
> int main() {
>     ll N, K;
>      cin >> N >> K;
>     for(int i = 0; i < N; i++) {
>         cin >> A[i];
>     }
>     solve(N, K);
>     return 0;
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/angry%20child%20q.txt) · CODING RESOURCES/coding ninjas/Dp-1/angry child q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/angry%20child%20s.txt) · CODING RESOURCES/coding ninjas/Dp-1/angry child s.txt
