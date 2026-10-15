---
kind: "coding-problem"
title: "Jack Goes To Rapture (Day 76)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 76 Solutions/JackGoesToRapture.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Jack Goes To Rapture (Day 76)

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

> [!example]- Reference 1 · JackGoesToRapture.java
> ```java
> import java.io.*;
> import java.util.*;
> import java.text.*;
> import java.math.*;
> import java.util.regex.*;
>
> public class JackGoesToRapture {
>
>    static class path implements Comparable<path>
> 	{
> 		int d;
> 		int res;
> 		path(int x, int y)
> 		{
> 			d = x;
> 			res = y;
> 		}
> 		public int compareTo(path argument1) {
> 			return res - argument1.res;
> 		}
> 	}
> 	   public static void main(String[] args) {
>
> 		   Scanner sc = new Scanner(System.in);
> 			int nodes = sc.nextInt();
> 			int edges = sc.nextInt();
>              ArrayList<path>[] edge = new ArrayList[nodes];
> 			for(int i = 0; i < nodes; i ++)
> 				edge[i] = new ArrayList<path>();
> 				int[] sum = new int[nodes];
> 				Arrays.fill(sum, Integer.MAX_VALUE);
>              for(int i = 0; i < edges; i ++)
> 			{
> 				int destA = sc.nextInt()-1;
> 				int destB = sc.nextInt()-1;
> 				int val = sc.nextInt();
> 				edge[Math.min(destA, destB)].add(new path(Math.max(destA, destB), val));
> 				edge[Math.max(destA, destB)].add(new path(Math.min(destA, destB), val));
> 			}
> 			
> 			PriorityQueue<path> pr = new PriorityQueue<path>();
> 			pr.add(new path(0,0));
> 			while(!pr.isEmpty())
> 			{
> 				path c = pr.remove();
> 				if(c.res < sum[c.d]){
> 					sum[c.d]= c.res;
> 					if(c.d == nodes-1)
> 					{
> 						System.out.println(c.res);
> 						sc.close();
> 						return;
> 					}
> 					for(int i = 0; i < edge[c.d].size(); i ++)
> 						pr.add(new path(edge[c.d].get(i).d,Math.max(edge[c.d].get(i).res, c.res)));
> 				}
> 			}
> 			System.out.println("-1");
> 			sc.close();
> 	    }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2076%20Solutions/JackGoesToRapture.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 76 Solutions/JackGoesToRapture.java
