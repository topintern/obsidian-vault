---
kind: "coding-problem"
title: "Jon Snow and his favourite number"
collection: "Coding Ninjas"
topic: "Dynamic Programming I"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-1/jon snow no q.txt","CODING RESOURCES/coding ninjas/Dp-1/jon snow no s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Jon Snow and his favourite number

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Jon Snow now has to fight with White Walkers. He has n rangers, each of which has his own strength. Also Jon Snow has his favourite number x. Each ranger can fight with a white walker only if the strength of the white walker equals his strength. He however thinks that his rangers are weak and need to improve. Jon now thinks that if he takes the bitwise XOR of strengths of some of rangers with his favourite number x, he might get soldiers of high strength. So, he decided to do the following operation k times:
Arrange all the rangers in a straight line in the order of increasing strengths.
Take the bitwise XOR of the strength of each alternate ranger with x and update it's strength.
Suppose, Jon has 5 rangers with strengths [9,?7,?11,?15,?5] and he performs the operation 1 time with x?=?2. He first arranges them in the order of their strengths, [5,?7,?9,?11,?15]. Then he does the following:
The strength of first ranger is updated to 5 xor 2, i.e. 7.
The strength of second ranger remains the same, i.e. 7.
The strength of third ranger is updated to 9 xor 2, i.e. 11.
The strength of fourth ranger remains the same, i.e. 11.
The strength of fifth ranger is updated to 15 xor 2, i.e. 13.
The new strengths of the 5 rangers are [7,?7,?11,?11,?13]
Now, Jon wants to know the maximum and minimum strength of the rangers after performing the above operations k times. He wants your help for this task. Can you help him?

### Input

First line consists of three integers n, k, x (1?=?n?=?10^5, 0?=?k?=?10^5, 0?=?x?=?10^3) — number of rangers Jon has, the number of times Jon will carry out the operation and Jon's favourite number respectively.

Second line consists of n integers representing the strengths of the rangers a1,?a2,?...,?an (0?=?ai?=?10^3).

### Output

Output two integers, the maximum and the minimum strength of the rangers after performing the operation k times.

### Sample Input

```text
5 1 2
9 7 11 15 5
```

### Sample Output

```text
13 7
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · jon snow no s.txt
> ```cpp
> //http://codeforces.com/problemset/problem/768/C
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
>
> using namespace std;
> int freq[2][1024];
> int main()
> {
>     int n, x, k, i, j, a, ma=0;
>     cin>>n>>k>>x;
>     for(i=0;i<n;i++){
>         cin>>a;
>         ma=max(ma, a);
>         ma=max(ma, a^x);
>         freq[0][a]++;
>         freq[1][a]++;
>     }
>     ma=min(ma*2, 1023);
>     for(i=0;i<k;i++)
>     {
>         int c=0;
>         for(j=0;j<=ma;j++)
>         {
>             if(freq[0][j]==0)continue;
>             if(c%2==0)
>             {
>                 int p=(freq[0][j]+1)/2;
>                 freq[1][(j^x)]+=p;
>                 freq[1][j]-=p;
>             }
>             else
>             {
>                 int p=freq[0][j]/2;
>                 freq[1][(j^x)]+=p;
>                 freq[1][j]-=p;
>             }
>             c+=freq[0][j];
>         }
>         for(j=0;j<=ma;j++)
>         {
>             freq[0][j]=freq[1][j];
>         }
>     }
>     for(i=ma;i>=0;i--)
>         if(freq[0][i]>0)break;
>     cout<<i<<" ";
>
>     for(i=0;i<=ma;i++)
>         if(freq[0][i]>0)break;
>     cout<<i;
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/jon%20snow%20no%20q.txt) · CODING RESOURCES/coding ninjas/Dp-1/jon snow no q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/jon%20snow%20no%20s.txt) · CODING RESOURCES/coding ninjas/Dp-1/jon snow no s.txt
