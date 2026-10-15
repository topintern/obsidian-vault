---
kind: "coding-problem"
title: "Task Scheduler (Day 32)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 32 Solutions/TaskScheduler.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Task Scheduler (Day 32)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

In operating system, process scheduling is an important concept.
CPU need to schedule the given processes given as an array of chars . 

Array contains capital letters A to Z where different letters represent different processes.

Scheduling the processes have to follow the given rules:
    - processes could be done without original order. 
    - Each process could be done in one interval. 
    - For each interval, CPU could finish one process or just be idle.

There is a non-negative cooling interval n that means between two same processes, 
there must be at least n intervals that CPU can assign with different processes or just be idle.

You need to return the least number of intervals the CPU will take to finish all the given processes.

Example:
    Input=  A A A B B B
            2
    Output= 8
    Explanation: 
        A -> B -> idle -> A -> B -> idle -> A -> B.

---------------TestCases---------------
case =1
input =A A B B B A A B B C C C D D D
4
output =21

case =2
input =A A A A B B B B C C C C C C D D D D E
5
output =31

case =3
input =X X X Y Y Y Z Z Z B B B B C C C E
3
output =17

case =4
input =K L M N O M N O P Q R S P Q R S T U V W 
2
output =20

case =5
input =A A A A A A A A A A A A
3
output =45

case =6
input =A A B B B A A B B C C C D D D
5
output =25

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · TaskScheduler.java
> ```java
> /*
> In operating system, process scheduling is an important concept.
> CPU need to schedule the given processes given as an array of chars . 
>
> Array contains capital letters A to Z where different letters represent different processes.
>
> Scheduling the processes have to follow the given rules:
>     - processes could be done without original order. 
>     - Each process could be done in one interval. 
>     - For each interval, CPU could finish one process or just be idle.
>
> There is a non-negative cooling interval n that means between two same processes, 
> there must be at least n intervals that CPU can assign with different processes or just be idle.
>
> You need to return the least number of intervals the CPU will take to finish all the given processes.
>
> Example:
>     Input=  A A A B B B
>             2
>     Output= 8
>     Explanation: 
>         A -> B -> idle -> A -> B -> idle -> A -> B.
>
> ---------------TestCases---------------
> case =1
> input =A A B B B A A B B C C C D D D
> 4
> output =21
>
> case =2
> input =A A A A B B B B C C C C C C D D D D E
> 5
> output =31
>
> case =3
> input =X X X Y Y Y Z Z Z B B B B C C C E
> 3
> output =17
>
> case =4
> input =K L M N O M N O P Q R S P Q R S T U V W 
> 2
> output =20
>
> case =5
> input =A A A A A A A A A A A A
> 3
> output =45
>
> case =6
> input =A A B B B A A B B C C C D D D
> 5
> output =25
>
> */
>
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class TaskScheduler {
>
> 	 public static int leastInterval(char[] tasks, int n) {
> 	        int[] map = new int[26];
> 	        for (char c: tasks)
> 	            map[c - 'A']++;
> 	        Arrays.sort(map);
> 	        int max_val = map[25] - 1, idle_slots = max_val * n;
> 	        for (int i = 24; i >= 0 && map[i] > 0; i--) {
> 	            idle_slots -= Math.min(map[i], max_val);
> 	        }
> 	        return idle_slots > 0 ? idle_slots + tasks.length : tasks.length;
> 	    }
> 	 
> 	 public static void main(String args[] ) throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 			char[] tasks = br.readLine().replace(" ", "").toCharArray(); 
> 			int n =Integer.parseInt(br.readLine());
>
> 			System.out.println(leastInterval(tasks,n));
> 			}
> 	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2032%20Solutions/TaskScheduler.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 32 Solutions/TaskScheduler.java
