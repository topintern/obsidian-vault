---
kind: "coding-problem"
title: "Solution (Day 91)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 91 Solutions/Solution.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Solution (Day 91)

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

> [!example]- Reference 1 · Solution.java
> ```java
> import java.util.*;
>
> class Player {
> 	String name;
> 	int score;
>
> 	Player(String name, int score) {
> 		this.name = name;
> 		this.score = score;
> 	}
> }
>
> class Checker implements Comparator<Player>{
>
>     public int compare(Player a, Player b) {
>         // If 2 Players have the same score
>         if(a.score == b.score){
>             // Order alphabetically by name
>             return a.name.compareTo(b.name);
>         }    
>
>         // Otherwise, order higher score first  
>         return ((Integer) b.score).compareTo(a.score);
>     }
> }
>
> public class Solution {
>     public static void main(String[] args) {
>         Scanner scan = new Scanner(System.in);
>         int n = scan.nextInt();
>
>         Player[] player = new Player[n];
>         Checker checker = new Checker();
>         
>         for(int i = 0; i < n; i++){
>             player[i] = new Player(scan.next(), scan.nextInt());
>         }
>         scan.close();
>
>         Arrays.sort(player, checker);
>         for(int i = 0; i < player.length; i++){
>             System.out.printf("%s %s\n", player[i].name, player[i].score);
>         }
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2091%20Solutions/Solution.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 91 Solutions/Solution.java
