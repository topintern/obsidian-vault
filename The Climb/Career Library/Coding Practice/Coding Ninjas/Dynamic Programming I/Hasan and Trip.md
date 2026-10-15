---
kind: "coding-problem"
title: "Hasan and Trip"
collection: "Coding Ninjas"
topic: "Dynamic Programming I"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-1/hasan trip q.txt","CODING RESOURCES/coding ninjas/Dp-1/hasan trip s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Hasan and Trip

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Hasan has finally finished his final exams and he decided to go in a trip among cities in Syria.
There are N cities in Syria and they are numbered from 1 to N, each city has coordinates on plane, i-th city is in (Xi, Yi).
Hasan is in first city and he wants to visit some cities by his car in the trip but the final destination should be N-th city and the sequence of cities he will visit should be increasing in index (i.e. if he is in city i he can move to city j if and only if i < j ).
Visiting i-th city will increase Hasan's happiness by Fi units (including first and last cities), also Hasan doesn't like traveling too much, so his happiness will decrease by total distance traveled by him.
Help Hasan by choosing a sequence of cities to visit which maximizes his happiness.

### Input format

First line contain integer N.
Next N lines contains three integers each, i-th line contains coordinates of i-th city Xi, Yi and Fi.

### Output format

Output one number rounded to 6 digits after floating point, the maximum possible happiness Hasan can get. Note: If answer is 2 print 2.000000

### Constraints

1 <= N <= 3,000
0 <= Xi, Yi, Fi <= 100,000

### Sample Input

```text
3
0 0 1
3 1 1
6 0 9
```

### Sample Output

```text
4.675445
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · hasan trip s.txt
> ```cpp
> #include <bits/stdc++.h>
>
> #define mod 1000000007
> #define inf 1000000000000
> #define root2 1.41421
> #define root3 1.73205
> #define pi 3.14159
> #define MAX 100001
> #define ll long long int
> #define PII pair<int, int>
> #define f first
> #define s second
> #define ss(n) scanf("%lld", &n)
> #define ssf(n) scanf("%lf", &n)
> #define mk make_pair
> #define PDD pair<double , double>
> #define gc getchar
> #define pb push_back
> using namespace std;
> double dp[3001], F[3001];
> PDD d[3001];
> ll n;
> double fun(PDD d1, PDD d2)
> {
>     return sqrt((d2.f-d1.f)*(d2.f-d1.f)+(d2.s-d1.s)*(d2.s-d1.s));
> }
>
> int main()
> {
>     ll i, j;
>     double x, y;
>     cin>>n;
>     for(i=0;i<n;i++)
>     {
>         cin>>x>>y;
>         d[i]=mk(x, y);
>         cin>>F[i];
>     }
>     dp[0]=F[0];
>     for(i=1;i<n;i++)
>     {
>         dp[i]=-inf;
>         for(j=0;j<i;j++)
>         {
>             x=fun(d[i], d[j]);//Find distance between i and j
>             dp[i]=max(dp[i], dp[j]-x);//Maximize over all possible differences
>         }
>         dp[i]+=F[i];
>     }
>     cout<<fixed;
>     cout<<setprecision(6)<<dp[n-1]<<endl;
>     return 0;
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/hasan%20trip%20q.txt) · CODING RESOURCES/coding ninjas/Dp-1/hasan trip q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/hasan%20trip%20s.txt) · CODING RESOURCES/coding ninjas/Dp-1/hasan trip s.txt
