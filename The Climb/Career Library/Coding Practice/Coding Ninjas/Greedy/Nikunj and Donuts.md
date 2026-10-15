---
kind: "coding-problem"
title: "Nikunj and Donuts"
collection: "Coding Ninjas"
topic: "Greedy"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/3.greedy/donuts q.txt","CODING RESOURCES/coding ninjas/3.greedy/donuts s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Nikunj and Donuts

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Nikunj loves donuts, but he also likes to stay fit. He eats n donuts in one sitting, and each donut has a calorie count, ci. After eating a donut with k calories, he must walk at least 2^j x k(where j is the number donuts he has already eaten) miles to maintain his weight.
Given the individual calorie counts for each of the n donuts, find and print a long integer denoting the minimum number of miles Nikunj must walk to maintain his weight. Note that he can eat the donuts in any order.

### Input

The first line contains an integer, n, denoting the number of donuts. 
The second line contains n space-separated integers describing the respective calorie counts of each donut I, i.e ci.

### Output

Print a long integer denoting the minimum number of miles Nikunj must walk to maintain his weight.

### Constraints

1 = n = 40
1 = ci = 1000

### Sample Input

```text
3
1 3 2
```

### Sample Output

```text
11
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · donuts s.txt
> ```cpp
> #include <bits/stdc++.h>
> using namespace std;
>
> long long arr[100];
>
> int main() {    
>     int n;
>     cin>>n;
>     
>     for(int i=0;i<n;i++){
>         cin>>arr[i];
>     }
>     
>     sort(arr, arr+n, greater<long long>());
>     long long ans = 0;
>     for(int i=0;i<n;i++)
>         ans += (1LL<<i) * arr[i];
>     cout<<ans;
>     
>     return 0;
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/3.greedy/donuts%20q.txt) · CODING RESOURCES/coding ninjas/3.greedy/donuts q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/3.greedy/donuts%20s.txt) · CODING RESOURCES/coding ninjas/3.greedy/donuts s.txt
