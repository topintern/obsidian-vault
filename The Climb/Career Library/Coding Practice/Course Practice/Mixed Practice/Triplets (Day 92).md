---
kind: "coding-problem"
title: "Triplets (Day 92)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 92 Solutions/Triplets.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Triplets (Day 92)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Problem

The source has reference code without a separate problem statement. Establish its inputs, expected outputs, and constraints before practising.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Triplets.java
> ```java
> #include<bits/stdc++.h>
> using namespace std;
>
> map<long long,long long> l,r;
>
> int main()
> {
> 	long long n, k,ans=0 ;
> 	scanf("%lld%lld",&n,&k);
> 	long long a[n];
> 	for(int i=0;i<n;i++)
> 		scanf("%lld",&a[i]);
> 	for(int i=0;i<n;i++)
> 		r[a[i]]++;
> 	for(int i=0;i<n;i++)
> 	{
> 		r[a[i]]--;
> 		if(a[i]%k==0)
> 		{
> 			ans+=l[a[i]/k]*r[a[i]*k];
> 		}
> 		l[a[i]]++;
> 	}
> 	printf("%lld\n",ans);
> 	return 0;
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2092%20Solutions/Triplets.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 92 Solutions/Triplets.java
