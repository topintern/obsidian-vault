---
kind: "coding-problem"
title: "Weighted Job Scheduling"
collection: "Coding Ninjas"
topic: "Greedy"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/3.greedy/weighted job q.txt","CODING RESOURCES/coding ninjas/3.greedy/weighted job s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Weighted Job Scheduling

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

You are given N jobs where every job is represented as:
1.Start Time
2.Finish Time
3.Profit Associated
Find the maximum profit subset of jobs such that no two jobs in the subset overlap.

### Input

The first line of input contains one integer denoting N.
Next N lines contains three space separated integers denoting the start time, finish time and the profit associated with the ith job. 

### Output

Output one integer, the maximum profit that can be achieved.

### Constraints

1 = N = 10^6
1 = ai, di, p = 10^6

### Sample Input

```text
4
3 10 20
1 2 50
6 19 100
2 100 200
```

### Sample Output

```text
250
```

> [!tip] Cross-topic study
> The source stores this under Greedy, but the reference builds a profit table and chooses between including/excluding each job, using binary search for the previous compatible job. Also study [[The Climb/Career Library/Coding Practice/Coding Ninjas/Dynamic Programming II/Dynamic Programming II Study Guide|Dynamic Programming]].


## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · weighted job s.txt
> ```java
> import java.util.*;
>  
> // Class to represent a job
> class Job
> {
>     int start, finish, profit;
> }
>  
> // Used to sort job according to finish times
> class JobComparator implements Comparator<Job>
> {
>     public int compare(Job a, Job b)
>     {
>         return a.finish < b.finish ? -1 : a.finish == b.finish ? 0 : 1;
>     }
> }
>  
> public class solution
> {
>     /* A Binary Search based function to find the latest job
>       (before current job) that doesn't conflict with current
>       job.  "index" is index of the current job.  This function
>       returns -1 if all jobs before index conflict with it.
>       The array jobs[] is sorted in increasing order of finish
>       time. */
>     static public int binarySearch(Job jobs[], int index)
>     {
>         // Initialize 'lo' and 'hi' for Binary Search
>         int lo = 0, hi = index - 1;
>  
>         // Perform binary Search iteratively
>         while (lo <= hi)
>         {
>             int mid = (lo + hi) / 2;
>             if (jobs[mid].finish <= jobs[index].start)
>             {
>                 if (jobs[mid + 1].finish <= jobs[index].start)
>                     lo = mid + 1;
>                 else
>                     return mid;
>             }
>             else
>                 hi = mid - 1;
>         }
>  
>         return -1;
>     }
>  
>     // The main function that returns the maximum possible
>     // profit from given array of jobs
>     static public int schedule(Job jobs[])
>     {
>         // Sort jobs according to finish time
>         Arrays.sort(jobs, new JobComparator());
>  
>         // Create an array to store solutions of subproblems.
>         // table[i] stores the profit for jobs till jobs[i]
>         // (including jobs[i])
>         int n = jobs.length;
>         int table[] = new int[n];
>         table[0] = jobs[0].profit;
>  
>         // Fill entries in M[] using recursive property
>         for (int i=1; i<n; i++)
>         {
>             // Find profit including the current job
>             int inclProf = jobs[i].profit;
>             int l = binarySearch(jobs, i);
>             if (l != -1)
>                 inclProf += table[l];
>  
>             // Store maximum of including and excluding
>             table[i] = Math.max(inclProf, table[i-1]);
>         }
>  
>         return table[n-1];
>     }
>  
>     // Driver method to test above
>     public static void main(String[] args)
>     {
>         Scanner scn = new Scanner(System.in);
>         int n=scn.nextInt();
>         Job[] jobs = new Job[n];
>         for(int i=0;i<n;i++)
>         {
>             jobs[i] = new Job();
>             jobs[i].start = scn.nextInt();
>             jobs[i].finish = scn.nextInt();
>             jobs[i].profit = scn.nextInt();
>         }
>         System.out.println(schedule(jobs));
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/3.greedy/weighted%20job%20q.txt) · CODING RESOURCES/coding ninjas/3.greedy/weighted job q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/3.greedy/weighted%20job%20s.txt) · CODING RESOURCES/coding ninjas/3.greedy/weighted job s.txt
