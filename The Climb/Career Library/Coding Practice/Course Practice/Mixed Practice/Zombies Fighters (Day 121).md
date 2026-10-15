---
kind: "coding-problem"
title: "Zombies Fighters (Day 121)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 121 Solutions/ZombiesFighters.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Zombies Fighters (Day 121)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You are given a list of integers strength[], represent the strength of the people.
all the people running in same line with same speed.
If the strength value is negative the person is a zombie running towards left,
If the strength value is positive the person is a fighter running towards right.
and the absolute value represents their strength.

If a zombie and a fighter meet, the person with smallest strength will die. 
If both have the same strength, both will die. 
Two persons moving in the same direction will never meet.

Your task is to find out the list of strengths of people who will be alive. 

Input Format:
-------------
space separated integers, list of strength[].

Output Format:
--------------
Print the list of strengths people who will be alive.


Sample Input-1:
---------------
5 10 -5

Sample Output-1:
----------------
5 10


### Explanation

------------
The 10 and -5 meet resulting in 10. The 5 and 10 never meet.


Sample Input-2:
---------------
-3 -2 2 3

Sample Output-2:
----------------
-3 -2 2 3


### Explanation

------------
The people with the strengths,
-3 and -2 moving left, 3 and 2 moving right. No one will die.


Sample Input-3:
---------------
10 2 -5

Sample Output-3:
----------------
10


### Explanation

------------
The people with the strengths,
2 and -5 meet, 2 will die, -5 is alive.
And 10 and -5 meet, -5 will die, 10 is alive.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ZombiesFighters.java
> ```java
> /*
> You are given a list of integers strength[], represent the strength of the people.
> all the people running in same line with same speed.
> If the strength value is negative the person is a zombie running towards left,
> If the strength value is positive the person is a fighter running towards right.
> and the absolute value represents their strength.
>
> If a zombie and a fighter meet, the person with smallest strength will die. 
> If both have the same strength, both will die. 
> Two persons moving in the same direction will never meet.
>
> Your task is to find out the list of strengths of people who will be alive. 
>
> Input Format:
> -------------
> space separated integers, list of strength[].
>
> Output Format:
> --------------
> Print the list of strengths people who will be alive.
>
>
> Sample Input-1:
> ---------------
> 5 10 -5
>
> Sample Output-1:
> ----------------
> 5 10
>
> Explanation:
> ------------
> The 10 and -5 meet resulting in 10. The 5 and 10 never meet.
>
>
> Sample Input-2:
> ---------------
> -3 -2 2 3
>
> Sample Output-2:
> ----------------
> -3 -2 2 3
>
> Explanation:
> ------------
> The people with the strengths,
> -3 and -2 moving left, 3 and 2 moving right. No one will die.
>
>
> Sample Input-3:
> ---------------
> 10 2 -5
>
> Sample Output-3:
> ----------------
> 10
>
> Explanation:
> ------------
> The people with the strengths,
> 2 and -5 meet, 2 will die, -5 is alive.
> And 10 and -5 meet, -5 will die, 10 is alive.
>
> */
>
> import java.util.*;
> import java.io.*;
>
> class ZombiesFighters {
>     public int[] zombiesFighters(int[] people) {
>         int[] s = new int[people.length];
>         int top = -1;
>         for (int a : people) {
>             // Stack only contains people going left or those going right but starting from a more left position => No collision prob.
>             if (a > 0) s[++top] = a;
>             else {
>                 // Kill all smaller people going right.
>                 while (top > -1 && s[top] > 0 && s[top] < -a) top--;
>                 // If nearest person is also going left or there's none, this person can keep moving left without any collision.
>                 if (top == -1 || s[top] < 0) s[++top] = a;
>                 // If there's an person going right of the same size, both die.
>                 else if (s[top] == -a) top--;
>             }
>         }
>         return Arrays.copyOf(s, top + 1);
>     }
> 	
> 	public static void main(String args[] ) throws IOException {
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 		String str = br.readLine();
> 		String[] arr = str.split(" ");
> 		int[] people = Arrays.asList(arr).stream().mapToInt(Integer::parseInt).toArray();
> 		int [] result=new ZombiesFighters().zombiesFighters(people);
> 		for(int i: result)
> 		System.out.print(i+" ");
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20121%20Solutions/ZombiesFighters.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 121 Solutions/ZombiesFighters.java
