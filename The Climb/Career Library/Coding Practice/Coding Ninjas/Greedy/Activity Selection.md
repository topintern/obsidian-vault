---
kind: "coding-problem"
title: "Activity Selection"
collection: "Coding Ninjas"
topic: "Greedy"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/3.greedy/activity q.txt","CODING RESOURCES/coding ninjas/3.greedy/activity s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Activity Selection

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

You are given n activities with their start and finish times. Select the maximum number of activities that can be performed by a single person, assuming that a person can only work on a single activity at a time.

### Input

The first line of input contains one integer denoting N.
Next N lines contains two space separated integers denoting the start time and finish time for the ith activity.

### Output

Output one integer, the maximum number of activities that can be performed

### Constraints

1 = N = 10^6
1 = ai, di = 10^9

### Sample Input

```text
6
1 2
3 4
0 6
5 7
8 9
5 9
```

### Sample Output

```text
4
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · activity s.txt
> ```text
> n = int(input())
> intervals = []
> for i in range(0 , n):
> 		intervals.append(tuple(map(int, input().split())))
> intervals.sort(key=lambda x: x[1])
> count = 1
> max = intervals[0][1]
> for i in range(0 , n):
> 	if intervals[i][0] >= max:
> 		count+=1
> 		max = intervals[i][1]
> print(count)
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/3.greedy/activity%20q.txt) · CODING RESOURCES/coding ninjas/3.greedy/activity q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/3.greedy/activity%20s.txt) · CODING RESOURCES/coding ninjas/3.greedy/activity s.txt
