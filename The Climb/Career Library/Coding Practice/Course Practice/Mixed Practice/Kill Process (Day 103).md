---
kind: "coding-problem"
title: "Kill Process (Day 103)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 103 Solutions/Kill Process - LeetCode.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 103 Solutions/KillProcess.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Kill Process (Day 103)

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

> [!example]- Reference 1 · KillProcess.java
> ```java
> import java.util.*;
> public class KillProcess {
>     public static List<Integer> killProcess(List<Integer> pid, List<Integer> ppid, int kill) {
>         if (kill == 0) return pid;
>         
>         int n = pid.size();
>         Map<Integer, Set<Integer>> tree = new HashMap<>();
>         for (int i = 0; i < n; i++) {
>             tree.put(pid.get(i), new HashSet<Integer>());
>         }
>         for (int i = 0; i < n; i++) {
>             if (tree.containsKey(ppid.get(i))) {
>                 Set<Integer> children = tree.get(ppid.get(i));
>                 children.add(pid.get(i));
>                 tree.put(ppid.get(i), children);
>             }
>         }
>         
>         List<Integer> result = new ArrayList<>();
>         traverse(tree, result, kill);
>         
>         return result;
>     }
>     
>     private static void traverse(Map<Integer, Set<Integer>> tree, List<Integer> result, int pid) {
>         result.add(pid);
>         
>         Set<Integer> children = tree.get(pid);
>         for (Integer child : children) {
>             traverse(tree, result, child);
>         }
>     }
> 	public static void main(String args[])
> 	{
> 		Scanner sc = new Scanner(System.in);
> 		String[] str1=sc.nextLine().split(" ");
> 		 List<Integer> pid = new ArrayList<Integer>();
> 		 for(String s:str1)
> 			pid.add(Integer.parseInt(s));
> 		String[] str2=sc.nextLine().split(" ");
> 		 List<Integer> ppid = new ArrayList<Integer>();
> 		 for(String s:str2)
> 			ppid.add(Integer.parseInt(s));
> 		int id=sc.nextInt();
> 		List<Integer> result=killProcess(pid,ppid,id);
> 		Collections.sort(result);
> 		System.out.println(result);
> 	}
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/Kill Process - Leet Code-98020bb2.pdf|Kill Process - Leet Code-98020bb2.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/Kill Process - Leet Code-98020bb2.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20103%20Solutions/Kill%20Process%20-%20LeetCode.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 103 Solutions/Kill Process - LeetCode.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20103%20Solutions/KillProcess.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 103 Solutions/KillProcess.java
