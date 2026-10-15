---
kind: "coding-problem"
title: "Whois Winner (Day 109)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 109 Solutions/WhoisWinner.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Whois Winner (Day 109)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Indian Super League organizing a football match at Eden Gardens.
The teams are Bangalore and Chennai are playing opposite each other.

After Match starts, each team making some goals at certain time, 
for example, goal 'goal[i]' was made by a player at time 'time[i]'.
goal[i]: indicates the team number 0 (Bangalore) or 1 (Chennai).
time[i]: indicates the time of the goal made.

Now, your task is to find out the leading team at given time t[j].

Input Format:
------------------
Line-1: Two integers N and K, no of goalsgoal[i] and no of times t[j]
Line-2: N space seperated integers only 0's and 1', goals[i]
Line-3: N space seperated integers, time[i]
Line-4: K space seperated integers , t[i]
 
Output Format:
------------------
Print K space seperated integers as result.


Sample Input-1:
--------------------
7 5
0 1 1 0 0 1 0
0 5 10 15 20 25 30
3 12 25 15 24

Sample Output-1:
---------------------
0 1 1 0 0 1


### Explanation

---------------
At time 3, the goals are [0], and 0 is leading.
At time 12, the goals are [0,1,1], and 1 is leading.
At time 25, the goals are [0,1,1,0,0,1], and 1 is leading (as ties go to the most recent goal)
At time 15, the goals are [0,1,1,0], and 0 is leading (as ties go to the most recent goal)
At time 25, the goals are [0,1,1,0,0], and 0 is leading.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · WhoisWinner.txt
> ```java
> /*
> Indian Super League organizing a football match at Eden Gardens.
> The teams are Bangalore and Chennai are playing opposite each other.
>
> After Match starts, each team making some goals at certain time, 
> for example, goal 'goal[i]' was made by a player at time 'time[i]'.
> goal[i]: indicates the team number 0 (Bangalore) or 1 (Chennai).
> time[i]: indicates the time of the goal made.
>
> Now, your task is to find out the leading team at given time t[j].
>
> Input Format:
> ------------------
> Line-1: Two integers N and K, no of goalsgoal[i] and no of times t[j]
> Line-2: N space seperated integers only 0's and 1', goals[i]
> Line-3: N space seperated integers, time[i]
> Line-4: K space seperated integers , t[i]
>  
> Output Format:
> ------------------
> Print K space seperated integers as result.
>
>
> Sample Input-1:
> --------------------
> 7 5
> 0 1 1 0 0 1 0
> 0 5 10 15 20 25 30
> 3 12 25 15 24
>
> Sample Output-1:
> ---------------------
> 0 1 1 0 0 1
>
> Explanation:
> ---------------
> At time 3, the goals are [0], and 0 is leading.
> At time 12, the goals are [0,1,1], and 1 is leading.
> At time 25, the goals are [0,1,1,0,0,1], and 1 is leading (as ties go to the most recent goal)
> At time 15, the goals are [0,1,1,0], and 0 is leading (as ties go to the most recent goal)
> At time 25, the goals are [0,1,1,0,0], and 0 is leading.
> */
>
> import java.util.*;
>
> class WhoisWinner {
>
>     Map<Integer, Integer> m = new HashMap<>();
>     int[] time;
>     public TopVotedCandidate(int[] goals, int[] times) {
>         int n = goals.length, lead = -1;
>         Map<Integer, Integer> count = new HashMap<>();
>         time = times;
>         for (int i = 0; i < n; ++i) {
>             count.put(goals[i], count.getOrDefault(goals[i], 0) + 1);
>             if (i == 0 || count.get(goals[i]) >= count.get(lead)) lead = goals[i];
>             m.put(times[i], lead);
>         }
>     }
>
>     public int q(int t) {
>         int i = Arrays.binarySearch(time, t);
>         return i < 0 ? m.get(time[-i-2]) : m.get(time[i]);
>     }
> 	
> 	
> 	public static void main(String args[])
> 	{
> 		Scanner sc = new Scanner(System.in);
> 		int n=sc.nextInt();
> 		int t=sc.nextInt();
> 		
> 		int goals[]=new int[n];
> 		int times[]=new int[n];
> 		for(int i=0;i<n;i++)
> 			goals[i]=sc.nextInt();
> 		for(int i=0;i<n;i++)
> 			times[i]=sc.nextInt();
> 		
> 		WhoisWinner tvc= new WhoisWinner(goals,times);
> 		
> 		for(int i=0;i<t;i++)
> 		System.out.print(tvc.q(sc.nextInt())+" ");
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20109%20Solutions/WhoisWinner.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 109 Solutions/WhoisWinner.txt
