---
kind: "coding-problem"
title: "Edit Distance"
collection: "Coding Ninjas"
topic: "Dynamic Programming II"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-2/edit dist q.txt","CODING RESOURCES/coding ninjas/Dp-2/edit dist s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Edit Distance

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Given two strings s and t of lengths m and n respectively, find the Edit Distance between the strings. Edit Distance of two strings is minimum number of steps required to make one string equal to other. In order to do so you can perform following three operations only :
1. Delete a character

2. Replace a character with another one

3. Insert a character
Note - Strings don't contain spaces

### Input Format

Line 1 : String s
Line 2 : String t

### Output Format

Line 1 : Edit Distance value

### Constraints

1<= m,n <= 20

### Sample Input 1

```text
abc
dc
```

### Sample Output 1

```text
2
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · edit dist s.txt
> ```cpp
> #include<iostream>
> #include<cstring>
> using namespace std;
> int helper(string s1, string s2, int **a){
>   int m=s1.size(),n=s2.size();
>   if(m<=0||n<=0){
>     return max(m,n);
>   }
>   if(a[m][n]!=-1)
>     return a[m][n];
>   else{
>   if(s1[0]==s2[0]){
>     int x=helper(s1.substr(1),s2.substr(1),a);
>     a[m-1][n-1]=x;
>     a[m][n]=x;
>   }
>     else{
>        a[m][n-1]=helper(s1,s2.substr(1),a);
>        a[m-1][n-1]=helper(s1.substr(1),s2.substr(1),a);
>        a[m-1][n]=helper(s1.substr(1),s2,a);
>       a[m][n]=min(a[m][n-1],min(a[m-1][n-1],a[m-1][n]))+1;
>     }
>   }
>   return a[m][n];
> }
> int editDistance(string s1, string s2){
>   
>  int m=s1.size()+1,n=s2.size()+1;
>  int **ans = new int*[m];
> 	for(int i = 0; i < m; i++) {
> 		ans[i] = new int[n];
> 		for(int j = 0; j < n; j++) {
> 			ans[i][j] = -1;
> 		}
> 	}
>   return helper(s1,s2,ans);
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/edit%20dist%20q.txt) · CODING RESOURCES/coding ninjas/Dp-2/edit dist q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/edit%20dist%20s.txt) · CODING RESOURCES/coding ninjas/Dp-2/edit dist s.txt
