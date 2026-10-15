---
kind: "coding-problem"
title: "Permutation Swaps"
collection: "Coding Ninjas"
topic: "Advanced Graphs"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/5.Adv graphs/permutation swaps q.txt","CODING RESOURCES/coding ninjas/5.Adv graphs/permutation swaps s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Permutation Swaps

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Kevin has a permutation P of N integers 1, 2, ..., N, but he doesn't like it. Kevin wants to get a permutation Q.

Also he believes that there are M good pairs of integers (ai , bi). Kevin can perform following operation with his permutation:

Swap Px and Py only if (x, y) is a good pair.
Help him and tell if Kevin can obtain permutation Q using such operations.

### Input format

The first line of input will contain an integer T, denoting the number of test cases.

Each test case starts with two space-separated integers N and M. The next line contains N space-separated integers Pi. The next line contains N space-separated integers Qi. Each of the next M lines contains two space-separated integers ai and bi.

### Output format

For every test case output "YES" (without quotes) if Kevin can obtain permutation Q and "NO" otherwise.

### Constraints

1 = T = 10
2 = N = 100000
1 = M = 100000
1 = Pi, Qi = N. Pi and Qi are all distinct.
1 = ai < bi = N

### SAMPLE INPUT

```text
2
4 1
1 3 2 4
1 4 2 3
3 4
4 1
1 3 2 4
1 4 2 3
2 4
```

### SAMPLE OUTPUT

```text
NO 
YES
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · permutation swaps s.txt
> ```java
> import java.io.*;
> import java.util.*;
> class solution
> {
>     static int[] dad = new int[100005];
>     static int find(int x)
>     {
>
>         if(x == dad[x] )
>         {
>             return dad[x];
>         }
>         return ( dad[x] =find(dad[x]));
>     }
>
>     public static void main(String[] args)
>     {
>
>
>         Scanner sc = new Scanner(System.in);
>         int t = sc.nextInt();
>         while (t-- > 0)
>         {
>
>             int n = sc.nextInt();
>             int m = sc.nextInt();
>             for(int i=0;i<=n;i++) dad[i] =i;
>             int[] p = new int[n + 1];
>             for (int i = 1; i <= n; i++)
>             {
>                 int val= sc.nextInt();
>                 p[val] = i;
>             }
>
>             int[] q = new int[n + 1];
>             for (int i = 1; i <= n; i++)
>             {
>                 int val = sc.nextInt();
>                 q[val] = i;
>             }
>
>             while (m-- > 0)
>             {
>
>                 int a = sc.nextInt();
>                 int b = sc.nextInt();
>                 a = find(a);
>                 b=  find(b);
>                 if(a == b)
>                 {
>                     continue;
>                 }
>                 else
>                 {
>                     dad[a] =b;
>                 }
>             }
>
>             boolean flag = true;
>
>             for (int i = 1; i <= n; i++)
>             {
>                 if(find(p[i]) ==find(q[i]))
>                 {
>                     continue;
>                 }
>                 else
>                 {
>                     flag = false;
>                 }
>
>
>             }
>             System.out.println(flag == true ? "YES" : "NO");
>
>         }
>     }
>
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/5.Adv%20graphs/permutation%20swaps%20q.txt) · CODING RESOURCES/coding ninjas/5.Adv graphs/permutation swaps q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/5.Adv%20graphs/permutation%20swaps%20s.txt) · CODING RESOURCES/coding ninjas/5.Adv graphs/permutation swaps s.txt
