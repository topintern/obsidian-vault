---
kind: "coding-problem"
title: "Fractional Knapsack"
collection: "Coding Ninjas"
topic: "Greedy"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/3.greedy/fractional knapsack q.txt","CODING RESOURCES/coding ninjas/3.greedy/fractional knapsack s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Fractional Knapsack

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

You want to paint your house. The total area of your house is D units. There are a total of N workers. The ith worker is available after time Ti, has hiring cost Xi and speed Yi. This means he becomes available for hiring from time Ti and remains available after that. Once available, you can hire him with cost Xi, after which he will start painting the house immediately, covering exactly Yi units of house with paint per time unit. You may or may not hire a worker and can also hire or fire him at any later point of time. However, no more than 1 worker can be painting the house at a given time.
Since you want the work to be done as fast as possible, figure out a way to hire the workers, such that your house gets painted at the earliest possible time, with minimum cost to spend for hiring workers.
Note: You can hire a previously hired worker without paying him again.

### Input

The first line of input contains two integers "N D", the number of workers and the area of your house respectively. The ith of the next N lines denotes the ith worker, and contains three integers "Ti Xi Yi", described in the statement.

### Output

Output one integer, the minimum cost that you can spend in order to get your house painted at the earliest.

### Constraints

1 = N, T, X, Y = 10^5
1 = D = 10^11

### Sample Input

```text
3 3
1 1 1
2 2 2
3 1 5
```

### Sample Output

```text
3
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · fractional knapsack s.txt
> ```java
> import java.util.*;
>  
> public class solution {
>     public static void main(String args[] ) throws Exception {
>         Scanner sc = new Scanner(System.in);
>         
>         int n = sc.nextInt();
>         long d = sc.nextLong();
>         
>         PriorityQueue<Painter> pq = new PriorityQueue<Painter>(n, paintComp);
>         Painter p;
>         for(int i=0;i<n;i++) {
>         	long time = sc.nextLong();
>         	long cost = sc.nextLong();
>         	long unit = sc.nextLong();
>         	p = new Painter(time,cost,unit);
>         	pq.add(p);
>         }
>         
>         long totalCost = 0;
>         long prevTime = 0;
>         long prevUnit = 0;
>         long maxUnit = Long.MIN_VALUE;
>         while(!pq.isEmpty() && d > 0) {
>         	p = pq.poll();
>         	long time = p.getTime();
>         	long cost = p.getCost();
>         	long unit = p.getUnit();
>         	
>         	if(prevTime != 0) {
>         		d = d - (time - prevTime) * prevUnit;
>         		if(d <= 0)
>         			break;
>         	}
>         	if(maxUnit < unit) {
>         		maxUnit = unit;
>         		totalCost += cost;
>         		prevUnit = unit;
>         	}
>         	prevTime = time;
>         }
>         System.out.println(totalCost);
>     }
>     
>     public static Comparator<Painter> paintComp = new Comparator<Painter>(){
>         public int compare(Painter p1, Painter p2) {
>             if(p1.getTime() < p2.getTime())
>     			return -1;
>     		else if(p1.getTime() > p2.getTime())
>     			return 1;
>     		else {
>     			if(p1.getUnit() < p2.getUnit())
>     				return 1;
>     			else if(p1.getUnit() > p2.getUnit())
>     				return -1;
>     			else {
>     				if(p1.getCost() < p2.getCost())
>     					return -1;
>     				else
>     					return 1;
>     			}
>     		}
>         }
>     };
>     
>     static class Painter {
>     	long time;
>     	long cost;
>     	long unit;
>     	
>     	Painter(long time,long cost, long unit) {
>     		this.time = time;
>     		this.cost = cost;
>     		this.unit = unit;
>     	}
>     	
>     	public long getTime() {
>     		return time;
>     	}
>     	
>     	public long getCost() {
>     		return cost;
>     	}
>     	
>     	public long getUnit() {
>     		return unit;
>     	}
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/3.greedy/fractional%20knapsack%20q.txt) · CODING RESOURCES/coding ninjas/3.greedy/fractional knapsack q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/3.greedy/fractional%20knapsack%20s.txt) · CODING RESOURCES/coding ninjas/3.greedy/fractional knapsack s.txt
