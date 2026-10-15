---
kind: "coding-problem"
title: "Fun Game (Day 89)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 89 Solutions/FunGame.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Fun Game (Day 89)

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

> [!example]- Reference 1 · FunGame.java
> ```java
> import java.util.*;
>
> public class FunGame {
>     static int choice(int a[], int b[], boolean visited[]){
>         int maxGain=-1;
>         int index=0;
>         for(int i=0;i< a.length ;i++){
>             if((maxGain<(a[i]+b[i]))&&( !visited[i] )){
>                 index=i;                
>                 maxGain=a[i]+b[i];
>             }            
>         }
>         return index;
>     }
>     
>     static void playgame(Scanner sc){
>         int pointsA=0, pointsB=0;
>         int n=sc.nextInt();
>         int[] a = new int[n];
>         for(int i=0;i<n;i++)
>             a[i]=sc.nextInt();
>         
>         int[] b = new int[n];
>         for(int i=0;i<n;i++)
>             b[i]=sc.nextInt();
>         
>         boolean[] visited = new boolean[n];
>         Arrays.fill(visited, false);
>         
>         for(int i=0;i<n;i++){
>             if(i%2==0){
>                 int index=choice(a, b, visited);
>                 visited[index]=true;
>                 pointsA += a[index];
>             }
>             else{
>                 int index=choice(a, b, visited);
>                 visited[index]=true;
>                 pointsB += b[index];
>             }            
>         }
>         if(pointsA>pointsB)
>             System.out.println("First");
>         else if(pointsB>pointsA)
>             System.out.println("Second");
>         else
>             System.out.println("Tie");            
>     }
>     
>     public static void main(String[] args) {
>         Scanner sc=new Scanner(System.in);
>         playgame(sc);
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2089%20Solutions/FunGame.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 89 Solutions/FunGame.java
