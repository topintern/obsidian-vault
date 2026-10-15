---
kind: "coding-problem"
title: "Strobogrammatic Number (Day 99)"
collection: "Course Practice"
topic: "Math and Counting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 99 Solutions/StrobogrammaticNumber.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Strobogrammatic Number (Day 99)

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

> [!example]- Reference 1 · StrobogrammaticNumber.java
> ```java
> import java.util.*;
>
> class StrobogrammaticNumber{
>
> 	public static List<String> findStrobogrammatic(int n) {
> 		return helper(n, n);
> 	}
>
> 	static List<String> helper(int n, int m) {
> 		if (n == 0) return new ArrayList<String>(Arrays.asList(""));
> 		if (n == 1) return new ArrayList<String>(Arrays.asList("0", "1", "8"));
> 		
> 		List<String> list = helper(n - 2, m);
> 		
> 		List<String> res = new ArrayList<String>();
> 		
> 		for (int i = 0; i < list.size(); i++) {
> 			String s = list.get(i);
> 			
> 			if (n != m) res.add("0" + s + "0");
> 			
> 			res.add("1" + s + "1");
> 			res.add("6" + s + "9");
> 			res.add("8" + s + "8");
> 			res.add("9" + s + "6");
> 		}  
> 		return res;
> 	}
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		int N=sc.nextInt();
> 		List<String> list=findStrobogrammatic(N);
> 		Collections.sort(list); 
> 		System.out.println(list);
> 	}		
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2099%20Solutions/StrobogrammaticNumber.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 99 Solutions/StrobogrammaticNumber.java
