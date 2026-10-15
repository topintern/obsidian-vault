---
kind: "coding-problem"
title: "Pqueue (Day 3)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 3 Solutions/pqueue.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Pqueue (Day 3)

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

> [!example]- Reference 1 · pqueue.java
> ```java
> import java.util.*;
> import java.io.*;
> class pqueue
> {
> 	public static void main(String args[])
> 	{
> 		int n;
> 		Scanner sc=new Scanner(System.in);
> 		n=sc.nextInt();
> 		PriorityQueue<Integer> p=new PriorityQueue<Integer>();
> 		while(n!=0)
> 		{
> 			p.add(sc.nextInt());
> 			n--;
> 		}
> 		int s=0,c=0;
> 		while(p.size()>1)
> 		{
>            s=p.poll()+p.poll();
>            c+=s;
>            p.add(s);
> 		}
> 		System.out.println(c);
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%203%20Solutions/pqueue.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 3 Solutions/pqueue.java
