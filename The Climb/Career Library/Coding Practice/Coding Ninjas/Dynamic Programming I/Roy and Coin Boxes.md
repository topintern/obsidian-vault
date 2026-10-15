---
kind: "coding-problem"
title: "Roy and Coin Boxes"
collection: "Coding Ninjas"
topic: "Dynamic Programming I"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-1/roy coin box q.txt","CODING RESOURCES/coding ninjas/Dp-1/roy coin box s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Roy and Coin Boxes

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Roy has N coin boxes numbered from 1 to N.
Every day he selects two indices [L,R] and adds 1 coin to each coin box starting from L to R (both inclusive).
He does this for M number of days.

After M days, Roy has a query: How many coin boxes have atleast X coins.
He has Q such queries.

### Input

First line contains N - number of coin boxes.
Second line contains M - number of days. Each of the next M lines consists of two space separated integers L and R. Followed by integer Q - number of queries.
Each of next Q lines contain a single integer X.a

### Output

For each query output the result in a new line.

### Constraints

1 = N = 1000000

1 = M = 1000000

1 = L = R = N

1 = Q = 1000000

1 = X = N

### Sample Input

```text
7
4
1 3
2 5
1 2
5 6
4
1
7
4
2
```

### Sample Output

```text
6
0
0
4
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · roy coin box s.txt
> ```cpp
> #include <iostream>
> #include <cstdio>
> using namespace std;
> long int  days[1000001];
> long int strt[1000001], en[1000001], ans[1000001];
> int main()
> {
>     ios_base::sync_with_stdio(false);
>     cin.tie(0);
>     long int n, m, x, q, l, r, i, c=0;
>     cin>>n>>m;
>     for(i=0;i<m;i++)
>     {
>         cin>>l>>r;
>     	strt[l]++;//noting the times the starting box was kth box
>     	en[r]++;//noting the times the ending box was kth box
>     }
>     for(i=1;i<=n;i++)
>     {
>     	c+=strt[i];
>     	days[i]=c;//number of coins in a box is same as number of days the coin was put in the box
>     	c-=en[i];
>     }
>     //now calculate how many boxes have exact i coins
>     for(i=1;i<=n;i++)
>     ans[days[i]]++;
>     /*now calculate how many boxes have atleast i coins which is same as
>     number of boxes having atleast i+1 coins + number of boxes having exact i coins
>     Note: box with atleast max coins is same as box with exact k coins
>     In other words we can take max as n and start iterating from n-1*/
>     for(i=n-1;i>0;i--)
>     {
>     	ans[i]=ans[i]+ans[i+1];
>     }
>     cin>>q;
>     while(q--)
>     {
>     	c=0;
>     	cin>>x;
>     	cout<<ans[x]<<endl;
>     }
>     return 0;
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/roy%20coin%20box%20q.txt) · CODING RESOURCES/coding ninjas/Dp-1/roy coin box q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/roy%20coin%20box%20s.txt) · CODING RESOURCES/coding ninjas/Dp-1/roy coin box s.txt
