---
kind: "coding-problem"
title: "Flip Game (Day 97)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 97 Solutions/FlipGame.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Flip Game (Day 97)

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

> [!example]- Reference 1 · FlipGame.java
> ```java
> import java.util.Scanner;
>
> class FlipGame {
>     int len;
>     char ss[];
> 	boolean canWin(String s) {
> 		len = s.length();
> 		ss = s.toCharArray();
> 		return canWin();
> 	}
> 	boolean canWin() {
> 		for (int is = 0; is <= len-2; ++is) {
> 			if (ss[is] == '$' && ss[is+1] == '$') {
> 				ss[is] = '#'; ss[is+1] = '#';
> 				boolean wins = !canWin(); 
> 				ss[is] = '$'; ss[is+1] = '$';
> 				if (wins) return true;
> 			}
> 		}
> 		return false;
> 	} 
> 	public static void main(String args[])
> 	{
> 		System.out.println(new FlipGame().canWin(new Scanner(System.in).next()));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2097%20Solutions/FlipGame.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 97 Solutions/FlipGame.java
