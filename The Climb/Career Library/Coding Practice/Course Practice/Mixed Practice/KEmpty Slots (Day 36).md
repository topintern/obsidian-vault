---
kind: "coding-problem"
title: "KEmpty Slots (Day 36)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 36 Solutions/KEmptySlots.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# KEmpty Slots (Day 36)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You have N bulbs in a row numbered from 1 to N. Initially, all the bulbs are turned off. We turn on exactly one bulb everyday until all bulbs are on after N days.

You are given an array bulbs of length N where bulbs[i] = x means that on the (i+1)th day, we will turn on the bulb at position x where i is 0-indexed and x is 1-indexed.

Given an integer K, find out the minimum day number such that there exists two turned on bulbs that have exactly K bulbs between them that are all turned off.

If there isn't such day, return -1.

 

Example 1:

Input: 
bulbs: [1,3,2]
K: 1
Output: 2

### Explanation

On the first day: bulbs[0] = 1, first bulb is turned on: [1,0,0]
On the second day: bulbs[1] = 3, third bulb is turned on: [1,0,1]
On the third day: bulbs[2] = 2, second bulb is turned on: [1,1,1]
We return 2 because on the second day, there were two on bulbs with one off bulb between them.
Example 2:

Input: 
bulbs: [1,2,3]
K: 1
Output: -1

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · KEmptySlots.java
> ```java
> /*
>  * 
>  * 
>  * 
>  * 
> You have N bulbs in a row numbered from 1 to N. Initially, all the bulbs are turned off. We turn on exactly one bulb everyday until all bulbs are on after N days.
>
> You are given an array bulbs of length N where bulbs[i] = x means that on the (i+1)th day, we will turn on the bulb at position x where i is 0-indexed and x is 1-indexed.
>
> Given an integer K, find out the minimum day number such that there exists two turned on bulbs that have exactly K bulbs between them that are all turned off.
>
> If there isn't such day, return -1.
>
>  
>
> Example 1:
>
> Input: 
> bulbs: [1,3,2]
> K: 1
> Output: 2
> Explanation:
> On the first day: bulbs[0] = 1, first bulb is turned on: [1,0,0]
> On the second day: bulbs[1] = 3, third bulb is turned on: [1,0,1]
> On the third day: bulbs[2] = 2, second bulb is turned on: [1,1,1]
> We return 2 because on the second day, there were two on bulbs with one off bulb between them.
> Example 2:
>
> Input: 
> bulbs: [1,2,3]
> K: 1
> Output: -1
>
>  */
>
> package Elite2020;
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class KEmptySlots {
>
> 	public static int kEmptySlots(int[] bulbs, int k) {
>         int[] days =  new int[bulbs.length];
>         for(int i=0; i<bulbs.length; i++)days[bulbs[i] - 1] = i + 1;
>         int left = 0, right = k + 1, res = Integer.MAX_VALUE;
>         for(int i = 0; right < days.length; i++){
>             if(days[i] < days[left] || days[i] <= days[right]){
>                 if(i == right)res = Math.min(res, Math.max(days[left], days[right]));   //we get a valid subarray
>                 left = i; 
>                 right = k + 1 + i;
>             }
>         }
>         return (res == Integer.MAX_VALUE)?-1:res;
>     }
> 	
> 	public static void main(String args[] ) throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		String[] numberline = str.split(" ");
> 		int[] bulbs = Arrays.asList(numberline).stream().mapToInt(Integer::parseInt).toArray();
> 		int K = Integer.parseInt(br.readLine());
>
> 		System.out.println(kEmptySlots(bulbs,K));   
> 		
> 		}
> 	
> 	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2036%20Solutions/KEmptySlots.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 36 Solutions/KEmptySlots.java
