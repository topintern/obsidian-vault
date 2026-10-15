---
kind: "coding-problem"
title: "Square Brackets"
collection: "Coding Ninjas"
topic: "Dynamic Programming II"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-2/square bracket q.txt","CODING RESOURCES/coding ninjas/Dp-2/square bracket s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Square Brackets

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

You are given:
a positive integer n,
an integer k, 1<=k<=n,
an increasing sequence of k integers 0 < s1 < s2 < ... < sk <= 2n.
What is the number of proper bracket expressions of length 2n with opening brackets appearing in positions s1, s2,...,sk?

### Illustration

Several proper bracket expressions:
`[[]][[[]][]]`
`[[[][]]][][[]]`
An improper bracket expression:
`[[[][]]][]][[]]`
There is exactly one proper expression of length 8 with opening brackets in positions 2, 5 and 7.

### Task

Write a program which for each data set from a sequence of several data sets:
1. reads integers n, k and an increasing sequence of k integers from input,
2. computes the number of proper bracket expressions of length 2n with opening brackets appearing at positions s1,s2,...,sk,
3. writes the result to output.

### Input

The first line of the input file contains one integer d, 1 <= d <= 10, which is the number of data sets. The data sets follow. Each data set occupies two lines of the input file. The first line contains two integers n and k separated by single space, 1 <= n <= 19, 1 <= k <= n. The second line contains an increasing sequence of k integers from the interval [1;2n] separated by single spaces.

### Output

The i-th line of output should contain one integer - the number of proper bracket expressions of length 2n with opening brackets appearing at positions s1, s2,...,sk.

### Sample Input

```text
5 
1 1 
1 
1 1 
2 
2 1 
1 
3 1 
2 
4 2 
5 7 
```

### Sample Output

```text
1 
0 
2 
3 
2 
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · square bracket s.txt
> ```cpp
> #include <iostream>
> #include <cstdio>
> #include <cstring>
> using namespace std;
> int n, A[41];
> long long memo[21][21];
> long long int solve(int op, int cl, int cur, int k)
> {
>     if(memo[op][cur]!=-1)
>         return memo[op][cur];
>     if(op>n||(op==n&&k!=0))
>     {
>         if(A[cur]==1)
>         k--;
>         return 0;
>     }
>     if(op==n)
>     {
>         if(A[cur]==1)
>         k--;
>         return 1;
>     }
>     if(A[cur]==1)
>         k--;
>     if(op-cl==0||A[cur]==1)//cur must be opening
>     {
>         return memo[op][cur]=solve(op+1, cl, cur+1, k);
>     }
>     else if(op-cl>0)
>     {
>         return memo[op][cur]=solve(op+1, cl, cur+1, k)+solve(op, cl+1, cur+1, k);
>     }
>     else return memo[op][cur]=0;
> }
> int main()
> {
>     int d, i, x, k, p;
>     scanf("%d", &d);
>     while(d--)
>     {
>         scanf("%d %d", &n, &k);
>         for(i=0;i<=2*n;i++)
>             A[i]=0;
>         memset(memo, -1, sizeof memo);
>         p=0;
>         for(i=0;i<k;i++)
>         {
>             scanf("%d", &x);
>             if(A[x]!=1)
>                 p++;
>             A[x]=1;
>         }
>         if(A[2*n]==1)
>             printf("0\n");
>         else
>             printf("%lld\n", solve(0, 0, 1, p));
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/square%20bracket%20q.txt) · CODING RESOURCES/coding ninjas/Dp-2/square bracket q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/square%20bracket%20s.txt) · CODING RESOURCES/coding ninjas/Dp-2/square bracket s.txt
