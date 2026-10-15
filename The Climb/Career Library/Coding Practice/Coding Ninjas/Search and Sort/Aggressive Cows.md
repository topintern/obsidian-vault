---
kind: "coding-problem"
title: "Aggressive Cows"
collection: "Coding Ninjas"
topic: "Search and Sort"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/1.search and sort/aggresive cows q.txt","CODING RESOURCES/coding ninjas/1.search and sort/aggresive cows s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Aggressive Cows

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Farmer John has built a new long barn, with N (2 <= N <= 100,000) stalls. The stalls are located along a straight line at positions x1,...,xN (0 <= xi <= 1,000,000,000).
His C (2 <= C <= N) cows don't like this barn layout and become aggressive towards each other once put into a stall. To prevent the cows from hurting each other, FJ wants to assign the cows to the stalls, such that the minimum distance between any two of them is as large as possible. What is the largest minimum distance?

### Input

t – the number of test cases, then t test cases follows. 
* Line 1: Two space-separated integers: N and C
* Lines 2..N+1: Line i+1 contains an integer stall location, xi

### Output

For each test case output one integer: the largest minimum distance.

### Sample Input

```text
1
5 3
1
2
8
4
9
```

### Sample Output

```text
3 
```

### Output details

FJ can put his 3 cows in the stalls at positions 1, 4 and 8, 
resulting in a minimum distance of 3.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · aggresive cows s.txt
> ```cpp
> #include<bits/stdc++.h>
> using namespace std;
>
>
> bool ispossibleCows(int* arr,int n,int dmid,int cows){
>     int tempcows=cows;
>     tempcows--;
>     int lastcow=0;
>     for(int i=1;i<n;i++){
>         if(arr[i]-arr[lastcow]>=dmid){
>             lastcow=i;
>             tempcows--;
>         }
>     }
>     if(tempcows<=0){
>         return true;
>     }
>     else{
>         return false;
>     }
> }
>
> void AggresiveCows(int*arr,int n,int dmin,int dmax,int cows){
>     int dmid=(dmin+dmax)/2;
>     if(dmin>dmax){
>         cout<<dmax<<endl;
>         return;
>     }
>     if(ispossibleCows(arr,n,dmid,cows)){
>         AggresiveCows(arr,n,dmid+1,dmax,cows);
>     }
>     else{
>         AggresiveCows(arr,n,dmin,dmid-1,cows);
>     }
> }
>
> int main() {
>
>     
>   int T;
>     cin>>T;
>     while(T--){
>
>         int n,c;
>         cin>>n>>c;
>         int* arr=new int[n];
>         for(int i=0;i<n;i++){
>             cin>>arr[i];
>         }
>         sort(arr,arr+n);
>         int dmin=0;
>         int dmax=arr[n-1];
>         AggresiveCows(arr,n,dmin,dmax,c);
>         delete []arr;
>     }
>         
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/1.search%20and%20sort/aggresive%20cows%20q.txt) · CODING RESOURCES/coding ninjas/1.search and sort/aggresive cows q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/1.search%20and%20sort/aggresive%20cows%20s.txt) · CODING RESOURCES/coding ninjas/1.search and sort/aggresive cows s.txt
