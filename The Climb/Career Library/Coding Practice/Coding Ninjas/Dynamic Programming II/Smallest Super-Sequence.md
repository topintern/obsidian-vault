---
kind: "coding-problem"
title: "Smallest Super-Sequence"
collection: "Coding Ninjas"
topic: "Dynamic Programming II"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-2/smaller supersequence q.txt","CODING RESOURCES/coding ninjas/Dp-2/smallest supersequence s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Smallest Super-Sequence

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Given two strings S and T, find and return the length of their smallest super-sequence.
A shortest super sequence of two strings is defined as the shortest possible string containing both strings as subsequences.
Note that if the two strings do not have any common characters, then return the sum of lengths of the two strings.

### Input Format

Line 1 : A string
Line 2: Another string

### Output Format

Length of the smallest super-sequence of given two strings. 

### Sample Input

```text
ab
ac
```

### Sample Output

```text
3
Sample Output Explanation:
Their smallest super-sequence can be "abc" which has length=3.
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · smallest supersequence s.txt
> ```text
> int smallestSuperSequence(char str1[], int len1, char str2[], int len2)
> {
>     int superseq[len1+1][len2+1];
>     for(int p=0; p<=len1; p++)
>     {
>         for(int q=0; q<=len2; q++)
>         {
>            if(p==0)
>            {
>                superseq[p][q]=q;
>            }
>            else if(q==0)
>            {
>                superseq[p][q]=p;
>            }
>            else if(str1[p-1] == str2[q-1])
>            {
>                superseq[p][q]=1+superseq[p-1][q-1];
>            }
>            else
>            {
>                superseq[p][q] = 1 + min(superseq[p-1][q], superseq[p][q-1]);
>            }
>         }
>     }
>     return superseq[len1][len2];
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/smaller%20supersequence%20q.txt) · CODING RESOURCES/coding ninjas/Dp-2/smaller supersequence q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/smallest%20supersequence%20s.txt) · CODING RESOURCES/coding ninjas/Dp-2/smallest supersequence s.txt
