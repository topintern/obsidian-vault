---
kind: "coding-problem"
title: "Adjacent Bit Counts"
collection: "Coding Ninjas"
topic: "Dynamic Programming I"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-1/adjacent bit q.txt","CODING RESOURCES/coding ninjas/Dp-1/adjacent bit s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Adjacent Bit Counts

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

For a string of n bits x1,x2,x3,...,Xn the adjacent bit count of the string (AdjBC(x)) is given by
X1*X2 + X2*X3 + X3*X4 + ... + Xn-1 * Xn
which counts the number of times a 1 bit is adjacent to another 1 bit. For example:
AdjBC(011101101) = 3
AdjBC(111101101) = 4
AdjBC(010101010) = 0
Write a program which takes as input integers n and k and returns the number of bit strings x of n bits (out of 2n) that satisfy AdjBC(x) = k. For example, for 5 bit strings, there are 6 ways of getting AdjBC(x) = 2:
11100, 01110, 00111, 10111, 11101, 11011

### Input

The first line of input contains a single integer P, (1 = P = 1000), which is the number of data sets that follow. Each data set is a single line that contains the data set number, followed by a space, followed by a decimal integer giving the number (n) of bits in the bit strings, followed by a single space, followed by a decimal integer (k) giving the desired adjacent bit count. The number of bits (n) will not be greater than 100.

### Output

For each data set there is one line of output. It contains the data set number followed by a single space, followed by the number of n-bit strings with adjacent bit count equal to k. As answer can be very large print your answer modulo 10^9+7.

### Sample Input

```text
10
1 5 2
2 20 8
3 30 17
4 40 24
5 50 37
6 60 52
7 70 59
8 80 73
9 90 84
10 100 90
```

### Sample Output

```text
1 6
2 63426
3 1861225
4 168212501
5 44874764
6 160916
7 22937308
8 99167
9 15476
10 23076518
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · adjacent bit s.txt
> ```cpp
> #include <iostream>
> #include <cstdio>
> #define ll long long
> #define mod 1000000007
> using namespace std;
> ll dp[101][101][2];
> int main()
> {
>     int t, n, k, i, j;
>     dp[1][0][0]=1;
>     dp[1][0][1]=1;
>     for(i=2;i<=100;i++)
>     {
>         dp[i][i-1][0]=0;
>         dp[i][i-1][1]=1;
>         dp[i][0][0]=dp[i-1][0][0]+dp[i-1][0][1];
>         dp[i][0][1]=dp[i-1][0][0];
>         if(dp[i][0][0]>=mod)dp[i][0][0]-=mod;
>     }
>     for(i=2;i<=100;i++)//for each n
>     {
>         for(j=1;j<i;j++)//for each k
>         {
>             dp[i][j][0]=dp[i-1][j][0]+dp[i-1][j][1];
>             dp[i][j][1]=dp[i-1][j][0]+dp[i-1][j-1][1];
>             if(dp[i][j][0]>=mod)dp[i][j][0]-=mod;
>             if(dp[i][j][1]>=mod)dp[i][j][1]-=mod;
>         }
>     }
>     cin>>t;
>     while(t--)
>     {
>         cin>>i>>n>>k;
>         if(n==0&&k==0)
>             cout<<i<<" 1"<<endl;
>         else
>         {
>             ll ans=dp[n][k][0]+dp[n][k][1];
>             if(ans>=mod)ans-=mod;
>             cout<<i<<" "<<ans<<endl;
>         }
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/adjacent%20bit%20q.txt) · CODING RESOURCES/coding ninjas/Dp-1/adjacent bit q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/adjacent%20bit%20s.txt) · CODING RESOURCES/coding ninjas/Dp-1/adjacent bit s.txt
