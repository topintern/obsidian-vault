---
kind: "coding-problem"
title: "Distribute Candies"
collection: "Coding Ninjas"
topic: "Search and Sort"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/1.search and sort/candies q.txt","CODING RESOURCES/coding ninjas/1.search and sort/candies s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Distribute Candies

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Shaky has N (1<=N<=50000) candy boxes each of them contains a non-zero number of candies (between 1 and 1000000000). Shaky want to distibute these candies among his K (1<=K<=1000000000) IIIT-Delhi students. He want to distibute them in a way such that:
1. All students get equal number of candies.
2. All the candies which a student get must be from a single box only.
As he want to make all of them happy so he want to give as many candies as possible. Help Shaky in finding out what is the maximum number of candies which a student can get.

### Input

First line contains 1<=T<=20 the number of test cases. Then T test cases follow. First line of each test case contains N and K. Next line contains N integers, ith of which is the number of candies in ith box.

### Output

For each test case print the required answer in a seperate line.

### Sample Input

```text
2
3 2 
3 1 4
4 1
3 2 3 9
```

### Sample Output

```text
3
9
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · candies s.txt
> ```cpp
> #include<cstdio>
> #include<stdlib.h>
> #include<limits.h>
> #include<iostream>
> #include<cstdlib>
> #include<string>
> #include<cstring>
> #include<algorithm>
> #include<cmath>
> #include<map>
> #include<queue>
> #include<vector>
> #include<list>
> #include<stack>
> #include<queue>
>  
>  
> using namespace std;
> #define ll long long int
> inline ll power(int base,int n);
>  
> #define MX 50005
> #define f(x,y,z) for((x)=(y);(x)<(z);(x)++)
> #define fe(x,y,z) for((x)=(y);(x)<=(z);(x)++)
> #define fm(x,y,z) for((x)=(y) ; (x)>(z) ; (x)--)
> #define FLUSH fflush(stdout)
> #define copy(dest,src,size) memcpy(dest,src,size)
> #define NL {printf("\n");}
>  
>  
> int box[MX];
> int n,k;
> int distribute( int m ){
>     int p = 0;
>     if( m == 0) return INT_MAX;
>     for( int i=0;i<n;i++){
>         if( box[i] ) p += box[i]/m;
>     }
>     return p; //no. of persons getting chocolates.
> }
> int main(){
>     int i,j;
>     int t;
>     int choco = -1; //chocolates per person
>     int p;
>     int low, high;
>     int mid = 0;
>     int ans = 0;
>     scanf("%d",&t);
>     while(t--){
>         choco = -1;
>         ans = 0;
>         scanf("%d %d",&n,&k);
>         for(i=0;i<n;i++){
>             scanf("%d",&box[i]);
>             if( box[i] > choco ) choco = box[i]; //choco. will get max here.
>         }
>         low=0;
>         high = choco;
>         while( low<=high){
>             mid = (low+high)/2;
>             p = distribute( mid );
>             if( p < k ){ 
>                 high = mid - 1;
>             }
>             else if(p >= k){
>                 low = mid + 1;
>                 if( mid > ans ) ans = mid;
>             }
>         }
>         printf("%d\n",ans);
>     }
>     return 0;
> }
> /* problem:
>  */
> inline ll power(int base,int n){
>     ll ans=1;
>     while(n){
>         if(n&1==1) ans*=base;
>         base*=base;
>         n=(n>>1);
>     }
>     return ans;
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/1.search%20and%20sort/candies%20q.txt) · CODING RESOURCES/coding ninjas/1.search and sort/candies q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/1.search%20and%20sort/candies%20s.txt) · CODING RESOURCES/coding ninjas/1.search and sort/candies s.txt
