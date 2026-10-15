---
kind: "coding-problem"
title: "Sticks (Day 3)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 3 Solutions/Sticks.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Sticks (Day 3)

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

> [!example]- Reference 1 · Sticks.java
> ```java
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.*;
>
> public class Sticks {
> 	    public static int connectSticks(int[] sticks) {
> 	        if (sticks == null || sticks.length <= 1) return 0;
>
> 	        // use greedy algorithm
> 	        int result = 0;
> 	        Queue<Integer> pQueue = new PriorityQueue<>();
> 	        for (int stick: sticks) {
> 	        	pQueue.offer(stick);
> 	        }
>
> 	        while (pQueue.size() > 1) {
> 	        	int sumLength = pQueue.poll() + pQueue.poll();
> 	        	result += sumLength;
> 	        	pQueue.offer(sumLength);
> 	        }
>
> 	        return result;
> 	    }
> 		public static void main(String args[] ) throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 		String str = br.readLine();
> 		String[] numbers = str.split(" ");
> 		int[] sticks = Arrays.asList(numbers).stream().mapToInt(Integer::parseInt).toArray();
> 		System.out.println(connectSticks(sticks));
> 		}
>
> 	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%203%20Solutions/Sticks.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 3 Solutions/Sticks.java
