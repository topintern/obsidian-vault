---
kind: "coding-problem"
title: "queens-attack-2 (Day 71)"
collection: "Course Practice"
topic: "Backtracking"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 71 Solutions/queens-attack-2-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 71 Solutions/QueensAttack2.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# queens-attack-2 (Day 71)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

========= Testcases Program-3 =========
case =1
input =4 0
4 4
output =9

case =2
input =5 3
4 3
5 5
4 2
2 3
output =10

case =3
input =1 0
1 1
output =0

case =4
input =6 2
2 5
3 4
4 6
output =13

case =5
input =6 3
3 3
5 6
1 2
4 4
output =16

case =6
input =8 3
1 1
3 3
1 4
5 1
output =6

case =7
input =8 4
3 5
6 2
6 5
5 7
2 6 
output =16

case =8
input =10 3
6 7
3 4
8 5
4 7
output =23

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · QueensAttack2.java
> ```java
> /*
> ========= Testcases Program-3 =========
> case =1
> input =4 0
> 4 4
> output =9
>
> case =2
> input =5 3
> 4 3
> 5 5
> 4 2
> 2 3
> output =10
>
> case =3
> input =1 0
> 1 1
> output =0
>
> case =4
> input =6 2
> 2 5
> 3 4
> 4 6
> output =13
>
> case =5
> input =6 3
> 3 3
> 5 6
> 1 2
> 4 4
> output =16
>
> case =6
> input =8 3
> 1 1
> 3 3
> 1 4
> 5 1
> output =6
>
> case =7
> input =8 4
> 3 5
> 6 2
> 6 5
> 5 7
> 2 6 
> output =16
>
> case =8
> input =10 3
> 6 7
> 3 4
> 8 5
> 4 7
> output =23
>
> */
>
> import java.io.*;
> import java.util.*;
>
> public class QueensAttack2 {
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         int n = in.nextInt();
>         int k = in.nextInt();
>         int rQueen = in.nextInt();
>         int cQueen = in.nextInt();
>         int [][] deltas = {{1,0},{1,1},{0,1},{-1,1},{-1,0},{-1,-1},{0,-1},{1,-1}};
>         HashMap<Integer,HashSet<Integer>> obstacles = new HashMap<>();
>         for(int a0 = 0; a0 < k; a0++){
>             int rObstacle = in.nextInt();
>             int cObstacle = in.nextInt();
>             if (!obstacles.containsKey(rObstacle)) obstacles.put(rObstacle,new HashSet<>());
>             obstacles.get(rObstacle).add(cObstacle);
>         }
>         
>         int count = 0;
>         for (int d = 0; d<8; d++) {
>             int [] delta = deltas[d];
>             int r = rQueen;
>             int c = cQueen;
>             while (true) {
>                 r += delta[0];
>                 c += delta[1];
>                 if (r<=0 || c<=0 || r>n || c>n || (obstacles.getOrDefault(r,new HashSet<>()).contains(c))) {
>                     break;
>                 }
>                 count++;
>             }
>         }
>         System.out.println(count);
>     }
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/queens-attack-2-English-a5009763.pdf|queens-attack-2-English-a5009763.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/queens-attack-2-English-a5009763.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2071%20Solutions/queens-attack-2-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 71 Solutions/queens-attack-2-English.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2071%20Solutions/QueensAttack2.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 71 Solutions/QueensAttack2.java
