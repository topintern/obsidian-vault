---
kind: "coding-problem"
title: "Add Bold Tag in String (Day 103)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 103 Solutions/Add Bold Tag in String - LeetCode.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 103 Solutions/AddBoldTag.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Add Bold Tag in String (Day 103)

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

> [!example]- Reference 1 · AddBoldTag.java
> ```java
> import java.util.*;
>
> public class AddBoldTag {
>     public static String addBoldTag(String s, String[] dict) {
>         boolean[] bold = new boolean[s.length()];
>         for (int i = 0, end = 0; i < s.length(); i++) {
>             for (String word : dict) {
>                 if (s.startsWith(word, i)) {
>                     end = Math.max(end, i + word.length());
>                 }
>             }
>             bold[i] = end > i;
>         }
>         
>         StringBuilder result = new StringBuilder();
>         for (int i = 0; i < s.length(); i++) {
>             if (!bold[i]) {
>                 result.append(s.charAt(i));
>                 continue;
>             }
>             int j = i;
>             while (j < s.length() && bold[j]) j++;
>             result.append("<i>" + s.substring(i, j) + "</i>");
>             i = j - 1;
>         }
>         
>         return result.toString();
>     }
> 	public static void main(String args[])
> 	{
> 		Scanner sc = new Scanner(System.in);
> 		String s=sc.nextLine();
> 		String[] str=sc.nextLine().split(" ");
> 		System.out.println(addBoldTag(s,str));
> 	}
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/Add Bold Tag in String - Leet Code-d8ce63f8.pdf|Add Bold Tag in String - Leet Code-d8ce63f8.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/Add Bold Tag in String - Leet Code-d8ce63f8.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20103%20Solutions/Add%20Bold%20Tag%20in%20String%20-%20LeetCode.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 103 Solutions/Add Bold Tag in String - LeetCode.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20103%20Solutions/AddBoldTag.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 103 Solutions/AddBoldTag.java
