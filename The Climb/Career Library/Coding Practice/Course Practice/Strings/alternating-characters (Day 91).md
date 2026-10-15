---
kind: "coding-problem"
title: "alternating-characters (Day 91)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 91 Solutions/alternating-characters-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 91 Solutions/AlternatingCharacters.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# alternating-characters (Day 91)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Problem

Read the original PDF below. Its mathematical notation was not reliably preserved by text extraction.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · AlternatingCharacters.java
> ```java
> import java.util.Scanner;
> public class AlternatingCharacters {
>
> 	/**
> 	 * @param args
> 	 */
> 	public static void main(String[] args) {
> 		// TODO Auto-generated method stub
> 		Scanner s = new Scanner(System.in);
> 			int count = 0;
> 			String str = s.nextLine();
> 			for(int i=1;i<str.length();i++)
> 			{
> 				if(str.charAt(i)==str.charAt(i-1))
> 				{
> 					count++;
> 				}
> 			}
> 			System.out.println(count);	
> 	}
>
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/alternating-characters-English-807dad43.pdf|alternating-characters-English-807dad43.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/alternating-characters-English-807dad43.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2091%20Solutions/alternating-characters-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 91 Solutions/alternating-characters-English.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2091%20Solutions/AlternatingCharacters.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 91 Solutions/AlternatingCharacters.java
