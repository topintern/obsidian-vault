---
kind: "coding-problem"
title: "Sorting the Skills"
collection: "Coding Ninjas"
topic: "Backtracking"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/2.backtrack/sorting skills q.txt","CODING RESOURCES/coding ninjas/2.backtrack/sorting skills s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Sorting the Skills

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

There is a company named James Peterson & Co. The company has ‘n’ employees. The employees have skills from 0 to n-1. All the employees have distinct skills. The manager of James Peterson & Co. wants to sort the employees on the basis of their skills in ascending order. He is only allowed to swap two employees which are adjacent to each other. He is given the skills of employees in an array of size ‘n’. He can swap the skills as long as the absolute difference between their skills is 1. You need to help the manager out and tell whether it is possible to sort the skills of employees or not.

### Input Format

First Line will have an integer ‘t’ denoting the no. of test cases.
First line of each test case contains an integer ‘n’ denoting the no. of employees in the company.
Second line of each test case contains ‘n’ distinct integers in the range [0, n-1].

### Output Format

For each test case, print “Yes” if it is possible to sort the skills otherwise “No”.

### Constraints

1 <= t <= 10
1 <= n <= 10^5

### Sample Input

```text
2
4
1 0 3 2
3
2 1 0
```

### Sample Output

```text
Yes
No
```

### Explanation

In first T.C., [1, 0, 3, 2] -> [0, 1, 3, 2] -> [0, 1, 2, 3]
In second T.C., [2, 1, 0] -> [1, 2, 0]  OR  [2, 1, 0] -> [2, 0, 1] So, it is impossible to sort.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · sorting skills s.txt
> ```cpp
>
> // A linear CPP program to check if array becomes
> // sorted after one swap
> #include <bits/stdc++.h>
> using namespace std;
> bool checksort(int* arr, int n)
> {
>     for (int i=0; i<n-1; i++)
>     {
>
>         if (arr[i] > arr[i+1])
>         {
>             if (arr[i] - arr[i+1] == 1)
>                 swap(arr[i], arr[i+1]);
>
>             else
>                 return false;
>         }
>     }
>     return true;
> }
> int main()
> {
>     int t;
>     cin>>t;
>     for(int i=0;i<t;i++)
>     {
>         int n;
>         cin>>n;
>         int* arr=new int[n];
>         for(int i=0;i<n;i++)
>         {
>             cin>>arr[i];
>         }
>         if (checksort(arr,n))
>         cout << "Yes"<<endl;
>     else
>         cout << "No"<<endl;
>
>     }
>
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/2.backtrack/sorting%20skills%20q.txt) · CODING RESOURCES/coding ninjas/2.backtrack/sorting skills q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/2.backtrack/sorting%20skills%20s.txt) · CODING RESOURCES/coding ninjas/2.backtrack/sorting skills s.txt
