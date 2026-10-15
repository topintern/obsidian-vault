---
kind: "coding-problem"
title: "Problem1 (Day 76)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 76 Solutions/Problem1.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Problem1 (Day 76)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You are a civil engineer responsible for creating a fortress wall
which is h feet high and w feet wide. You have a brick kiln in the fortress.
Unfortunately the kiln can make only 4 kinds of bricks. 
All these bricks are 1 feet high but they can be 1 feet,2 feet ,3 feet or 4 feet wide. 

You kingdom is very rich and you can get as many bricks as you want. 
In how many ways can you build the wall?

Input Format:
    - Two space-separated integers n and m, height is n and width is m 

Output Format:
    - An integer, number of ways to build the wall


### Sample Input

3 4

### Sample Output

512

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Problem1.java
> ```java
> /*
> You are a civil engineer responsible for creating a fortress wall
> which is h feet high and w feet wide. You have a brick kiln in the fortress.
> Unfortunately the kiln can make only 4 kinds of bricks. 
> All these bricks are 1 feet high but they can be 1 feet,2 feet ,3 feet or 4 feet wide. 
>
> You kingdom is very rich and you can get as many bricks as you want. 
> In how many ways can you build the wall?
>
> Input Format:
>     - Two space-separated integers n and m, height is n and width is m 
>
> Output Format:
>     - An integer, number of ways to build the wall
>
> Sample Input:
> 3 4
> Sample Output:
> 512
> */
>
> import java.util.*;
> class Test{
>     public static int count_ways(int sw,int dp[]){
>         if(sw==0) return 1;
>         if(sw<0) return 0;
>         if(dp[sw]!=-1) return dp[sw];
>         int ans=count_ways(sw-1,dp);
>         ans+=count_ways(sw-2,dp);
>         ans+=count_ways(sw-3,dp);
>         ans+=count_ways(sw-4,dp);
>         return dp[sw]=ans;
>     }
>     public static void main(String[] args){
>         Scanner sc=new Scanner(System.in);
>         int h=sc.nextInt(),w=sc.nextInt();
>         int dp[]=new int[w+1];
>         Arrays.fill(dp,-1);
>         int ans=(int)Math.pow(count_ways(w,dp),h);
>         System.out.println(ans);
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2076%20Solutions/Problem1.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 76 Solutions/Problem1.java
