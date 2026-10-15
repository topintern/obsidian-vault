---
kind: "coding-problem"
title: "Momos Market"
collection: "Coding Ninjas"
topic: "Search and Sort"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/1.search and sort/momos q.txt","CODING RESOURCES/coding ninjas/1.search and sort/momos s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Momos Market

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Shreya loves to eat momos. Her mother gives her money to buy vegetables but she manages to save some money out of it daily. After buying vegetables, she goes to "Momos Market", where there are ‘n’ number of shops of momos. Each of the shops of momos has a rate per momo. She visits the market and starts buying momos (one from each shop) starting from the first shop. She will visit the market for ‘q’ days. You have to tell that how many momos she can buy each day if she starts buying from the first shop daily. She cannot use the remaining money of one day on some other day. But she will save them for other expenses in the future, so, you also need to tell the sum of money left with her at the end of each day.

### Input Format

First line will have an integer ‘n’ denoting the number of shops in market.
Next line will have ‘n’ numbers denoting the price of one momo of each shop.
Next line will have an integer ‘q’ denoting the number of days she will visit the market.
Next ‘q’ lines will have one integer ‘X’ denoting the money she saved after buying vegetables.

### Constraints

1 <= n <= 10^5
1 <= q <= 10^5
1 <= X <= 10^9

### Output

There will be ‘q’ lines of output each having two space separated integers denoting number of momos she can buy and amount of money she saved each day.

### Sample Input

```text
4
2 1 6 3
1
11
```

### Sample Output

```text
3 2
```

### Explanation

Shreya visits the "Momos Market" for only one day. She has 11 INR to spend. She can buy 3 momos, each from the first 3 shops. She would 9 INR (2 + 1 + 6) for the same and hence, she will save 2 INR.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · momos s.txt
> ```cpp
> #include<iostream>
> using namespace std;
>
> int search(long arr[], int low, int high, long x)
> {
>   if(low>high)
>   {
>     return -1;
>   }
>   if(x>=arr[high])
>   {
>     return high;
>   }
>   int mid=(low+high)/2;
>   if(arr[mid]==x)
>   {
>     return mid;
>   }
>   if(mid>0 && arr[mid-1]<=x && x<arr[mid])
>   {
>     return mid-1;
>   }
>   if(x<arr[mid])
>   {
>     return search(arr,low,mid-1,x);
>   }
>   return search(arr,mid+1,high,x);
> }
> int main()
> {
>   int n;
>   cin>>n;
>   long* arr=new long[n];
>   for(int i=0;i<n;i++)
>   {
>     cin>>arr[i];
>   }
>   long* prefix=new long[n];
>   prefix[0]=arr[0];
>   for(int i=1;i<n;i++)
>   {
>     prefix[i]=prefix[i-1]+arr[i];
>   }
>   int q;
>   cin>>q;
>   while(q-->0)
>   {
>     long x;
>     cin>>x;
>     int s=search(prefix,0,n-1,x);
>     long val=x;
>     if(s!=-1)
>     {
> 	val-=prefix[s];
>     }
>     cout<<s+1<<" "<<val<<endl;
>   }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/1.search%20and%20sort/momos%20q.txt) · CODING RESOURCES/coding ninjas/1.search and sort/momos q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/1.search%20and%20sort/momos%20s.txt) · CODING RESOURCES/coding ninjas/1.search and sort/momos s.txt
