---
kind: "coding-problem"
title: "Maximum Square Matrix With All Zeros"
collection: "Coding Ninjas"
topic: "Dynamic Programming I"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-1/max matrix with all 0's q.txt","CODING RESOURCES/coding ninjas/Dp-1/max matrix with all 0's s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Maximum Square Matrix With All Zeros

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Given a n*m matrix which contains only 0s and 1s, find out the size of maximum square sub-matrix with all 0s. You need to return the size of square with all 0s.

### Input format

Line 1 : n and m (space separated positive integers)
Next n lines : m elements of each row (separated by space).

### Output Format

Line 1 : Size of maximum square sub-matrix

### Sample Input

```text
3 3
1 1 0
1 1 1
1 1 1
```

### Sample Output

```text
1
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · max matrix with all 0's s.txt
> ```cpp
> #include <iostream>
> using namespace std;  
>
> int findMaxSquareWithAllZeros(int** arr, int row, int col){
>     /* Given a n*m matrix which contains only 0s and 1s, find out the size of
>      * maximum square sub-matrix with all 0s. You need to return the size of
>      * square with all 0s. */
>     int **storage;
>     storage = new int*[row+1];
>     for(int i=0; i<=row; i++)
>     {
>         storage[i] = new int[col+1];
>         for(int j=0; j<=col; j++)
>             storage[i][j] = 0;
>     }
>     for(int i=row-1; i>=0; i--)
>         for(int j=col-1; j>=0; j--)
>         {
>             int maximum = storage[i][j] = max(storage[i+1][j], storage[i][j+1]);
>
>             if(min(row-i, col-j)<=maximum)
>                 continue;
>
>             bool foundOne = false;
>             for(int p=0; p<=maximum; p++)
>                 for(int q=0; q<=maximum; q++)
>                     if(arr[i+p][j+q]==1){
>                         foundOne = true;
>                         p = q = maximum+1;
>                     }
>             if(foundOne==false)
>                 storage[i][j] += 1;
>         }
>     int ans = storage[0][0];
>     for(int i=0; i<=row; i++)
>         delete [] storage[i];
>     delete [] storage;
>     return ans;
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/max%20matrix%20with%20all%200's%20q.txt) · CODING RESOURCES/coding ninjas/Dp-1/max matrix with all 0's q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-1/max%20matrix%20with%20all%200's%20s.txt) · CODING RESOURCES/coding ninjas/Dp-1/max matrix with all 0's s.txt
