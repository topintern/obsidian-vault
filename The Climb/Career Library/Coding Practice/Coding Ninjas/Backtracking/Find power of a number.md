---
kind: "coding-problem"
title: "Find power of a number"
collection: "Coding Ninjas"
topic: "Backtracking"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/2.backtrack/power of no q.txt","CODING RESOURCES/coding ninjas/2.backtrack/power of no s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Find power of a number

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Write a program to find x to the power n (i.e. x^n). Take x and n from the user. You need to print the answer.

### Input format

Two integers x and n (separated by space)

### Output Format

x^n (i.e. x raise to the power n)

### Sample Input 1

```text
 3 4
```

### Sample Output 1

```text
81
```

### Sample Input 2

```text
 2 5
```

### Sample Output 2

```text
32
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · power of no s.txt
> ```text
> # Problem ID: 467 Find power of a number
> l = input().strip().split(' ')
> base, n = (int(i) for i in l)
> result = 1
> for i in range(0,n):
>     result *= base
> print(result)
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/2.backtrack/power%20of%20no%20q.txt) · CODING RESOURCES/coding ninjas/2.backtrack/power of no q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/2.backtrack/power%20of%20no%20s.txt) · CODING RESOURCES/coding ninjas/2.backtrack/power of no s.txt
