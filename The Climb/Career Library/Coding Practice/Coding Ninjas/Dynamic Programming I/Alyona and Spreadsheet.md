---
kind: "coding-problem"
title: "Alyona and Spreadsheet"
collection: "Coding Ninjas"
topic: "Dynamic Programming I"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-1/alonya spread q.txt","CODING RESOURCES/coding ninjas/Dp-1/alonya spread s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Alyona and Spreadsheet

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

During the lesson small girl Alyona works with one famous spreadsheet computer program and learns how to edit tables.
Now she has a table filled with integers. The table consists of n rows and m columns. By ai,?j we will denote the integer located at the i-th row and the j-th column. We say that the table is sorted in non-decreasing order in the column j if ai,?j?=?ai?+?1,?j for all i from 1 to n?-?1.
Teacher gave Alyona k tasks. For each of the tasks two integers l and r are given and Alyona has to answer the following question: if one keeps the rows from l to r inclusive and deletes all others, will the table be sorted in non-decreasing order in at least one column? Formally, does there exist such j that ai,?j?=?ai?+?1,?j for all i from l to r?-?1 inclusive.
Alyona is too small to deal with this task and asks you to help!

### Input

The first line of the input contains two positive integers n and m (1?=?n·m?=?100?000) — the number of rows and the number of columns in the table respectively. Note that your are given a constraint that bound the product of these two integers, i.e. the number of elements in the table.

Each of the following n lines contains m integers. The j-th integers in the i of these lines stands for ai,?j (1?=?ai,?j?=?109).

The next line of the input contains an integer k (1?=?k?=?100?000) — the number of task that teacher gave to Alyona.

The i-th of the next k lines contains two integers li and ri (1?=?li?=?ri?=?n).

### Output

Print "Yes" to the i-th line of the output if the table consisting of rows from li to ri inclusive is sorted in non-decreasing order in at least one column. Otherwise, print "No".

### Sample Input

```text
5 4
1 2 3 5
3 1 3 2
4 5 2 3
5 5 3 2
4 4 3 4
6
1 1
2 5
4 5
3 5
1 3
1 5
```

### Sample Output

```text
Yes
No
Yes
Yes
Yes
No
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · alonya spread s.txt
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
>
> vector<vector<int> > A, B;
> int n, m;
> int main()
> {
>     cin>>n>>m;
>     vector<int> dp(n);
>     int i, j;
>     for(i=0;i<n;i++)
>     {
>         vector<int>v(m), v2(m, 0);
>         for(j=0;j<m;j++)cin>>v[j];
>         A.pb(v);
>         B.pb(v2);
>     }
>     for(i=0;i<m;i++)
>     {
>         B[0][i]=0;
>         for(j=1;j<n;j++)
>         {
>             if(A[j][i]>=A[j-1][i])
>                 B[j][i]=B[j-1][i];
>             else
>                 B[j][i]=j;
>         }
>     }
>     for(i=0;i<n;i++)
>     {
>         dp[i]=i;
>         for(j=0;j<m;j++)
>             dp[i]=min(dp[i], B[i][j]);
>         //cout<<i<<" "<<dp[i]<<endl;
>     }
>     int q, l, r;
>     cin>>q;
>     while(q--)
>     {
>         cin>>l>>r;
>         l--;r--;
>         if(dp[r]<=l)
>             cout<<"Yes\n";
>         else
>             cout<<"No\n";
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/alonya%20spread%20q.txt) · CODING RESOURCES/coding ninjas/Dp-1/alonya spread q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/alonya%20spread%20s.txt) · CODING RESOURCES/coding ninjas/Dp-1/alonya spread s.txt
