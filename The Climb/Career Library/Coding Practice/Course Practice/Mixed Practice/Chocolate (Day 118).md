---
kind: "coding-problem"
title: "Chocolate (Day 118)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 118 Solutions/Chocolate.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Chocolate (Day 118)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

In a class of N students, each student assigned with a score,
based on their performance in curriculum and other activities.

On the independence day, all the students stand in a line.
The teacher has to distribute the chocolates to all the students,

The distribution of chocolates is as follows,
 - Each student will get one chocolate for sure, and
 - The students with more score should recieve more chocolates 
than the students besides him(both left and right).

Can you help the teacher to find the minimum number of chocolates to distribute?

Input Format:
-------------
Lien-1 -> An integer N, number of students
Line-2 -> N space separated integers, scores of the students in the line.

Output Format:
--------------
Print an integer, minimum number of chocolates.


Sample Input-1:
---------------
3
1 0 2

Sample Output-1:
----------------
5


### Explanation: 

------------
You can distribute to the first, second and third student with 2, 1, 2 chocolates respectively.


Sample Input-2:
---------------
3
2 3 3

Sample Output-2:
----------------
4


### Explanation: 

------------
You can distribute to the first, second and third student with 1, 2, 1 chocolates
respectively. The third student gets 1 candy because it satisfies the above two rules.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Chocolate.java
> ```java
> /*
> In a class of N students, each student assigned with a score,
> based on their performance in curriculum and other activities.
>
> On the independence day, all the students stand in a line.
> The teacher has to distribute the chocolates to all the students,
>
> The distribution of chocolates is as follows,
>  - Each student will get one chocolate for sure, and
>  - The students with more score should recieve more chocolates 
> than the students besides him(both left and right).
>
> Can you help the teacher to find the minimum number of chocolates to distribute?
>
> Input Format:
> -------------
> Lien-1 -> An integer N, number of students
> Line-2 -> N space separated integers, scores of the students in the line.
>
> Output Format:
> --------------
> Print an integer, minimum number of chocolates.
>
>
> Sample Input-1:
> ---------------
> 3
> 1 0 2
>
> Sample Output-1:
> ----------------
> 5
>
> Explanation: 
> ------------
> You can distribute to the first, second and third student with 2, 1, 2 chocolates respectively.
>
>
> Sample Input-2:
> ---------------
> 3
> 2 3 3
>
> Sample Output-2:
> ----------------
> 4
>
> Explanation: 
> ------------
> You can distribute to the first, second and third student with 1, 2, 1 chocolates
> respectively. The third student gets 1 candy because it satisfies the above two rules.
>
> */
>
> import java.util.*;
>
> class Chocolate {
>     public int chocolate(int[] score) {
>         if(score.length == 0)
>             return 0;
>         int[] ans = new int[score.length];
>         ans[0] = 1;
>         for(int i = 1; i<score.length; i++){
>             if(score[i]>score[i-1])
>                 ans[i] = ans[i-1]+1;
>             else
>                 ans[i] = 1;
>         }
>         int sum = ans[score.length-1];
>         for(int i = score.length-2; i >= 0; i--){
>             if(score[i]>score[i+1])
>                 ans[i] = Math.max(ans[i], ans[i+1]+1);
>             sum += ans[i];
>         }
>         return sum;
>     }
> 	public static void main( String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		int N=sc.nextInt();
> 		int[] score=new int[N];
> 		for(int i=0;i<N;i++)
> 			score[i]=sc.nextInt();
> 		System.out.println(new Chocolate().chocolate(score));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20118%20Solutions/Chocolate.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 118 Solutions/Chocolate.java
