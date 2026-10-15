---
kind: "coding-problem"
title: "Cake Partition (Day 47)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 47 Solutions/CakePartition.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Cake Partition (Day 47)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Lasya has ordered a Cake delivery. 
The cake can be considered a perfect circle. 
There were n premade cuts in the cake when it was delivered. Each cut is a straight 
segment connecting the center of the cake with its boundary.

Let O be the center of the cake, Pi be the endpoint of the i-th cut lying on the boundary, 
and R be the point of the boundary straight to the right of O. 
Then the counterclockwise-measured angle ∠ROPi is equal to ai degrees, 
where ai is an integer between 0 and 359. 
Note that angles between 0 and 180 angles correspond to Pi in the top half of the cake, 
while angles between 180 and 360 angles correspond to the bottom half.

Lasya may cut her cake a few more times, and the new cuts still have to be straight 
segments starting at the center. She wants to make the pizza separated into several 
equal slices, with each slice being a circular sector with no cuts inside of it. 
How many new cuts Lasya will have to make?


### Input Format

------------
The first line contains a single integer n− 
    the numbers of premade cuts (2≤n≤360).

The second lines contains n integers a1,…,an − 
    angles of the cuts 1,…,n respectively (0≤a1<…,an−1<360).


### Output Format

-------------
Print a single integer − the smallest number of additional cuts Vasya has to make 
so that the pizza is divided into several equal slices.
Example-1:
    Input:
        2
        90 210
    Output:
        1
    
    Explanation:
        The pizza will be cut into three equal slices after making one extra cut at 330 degrees.


Example-2:
    Input:
        2
        0 1
    Output:
        358
    Explanation:
        Lasya will have to cut this pizza into 360 pieces of 1 degree angle each.
        so, need to make 358 new cuts.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · CakePartition.java
> ```java
> /*
>  * 
> Lasya has ordered a Cake delivery. 
> The cake can be considered a perfect circle. 
> There were n premade cuts in the cake when it was delivered. Each cut is a straight 
> segment connecting the center of the cake with its boundary.
>
> Let O be the center of the cake, Pi be the endpoint of the i-th cut lying on the boundary, 
> and R be the point of the boundary straight to the right of O. 
> Then the counterclockwise-measured angle ∠ROPi is equal to ai degrees, 
> where ai is an integer between 0 and 359. 
> Note that angles between 0 and 180 angles correspond to Pi in the top half of the cake, 
> while angles between 180 and 360 angles correspond to the bottom half.
>
> Lasya may cut her cake a few more times, and the new cuts still have to be straight 
> segments starting at the center. She wants to make the pizza separated into several 
> equal slices, with each slice being a circular sector with no cuts inside of it. 
> How many new cuts Lasya will have to make?
>
> Input Format
> ------------
> The first line contains a single integer n− 
>     the numbers of premade cuts (2≤n≤360).
>
> The second lines contains n integers a1,…,an − 
>     angles of the cuts 1,…,n respectively (0≤a1<…,an−1<360).
>
> Output Format
> -------------
> Print a single integer − the smallest number of additional cuts Vasya has to make 
> so that the pizza is divided into several equal slices.
> Example-1:
>     Input:
>         2
>         90 210
>     Output:
>         1
>     
>     Explanation:
>         The pizza will be cut into three equal slices after making one extra cut at 330 degrees.
>
>
> Example-2:
>     Input:
>         2
>         0 1
>     Output:
>         358
>     Explanation:
>         Lasya will have to cut this pizza into 360 pieces of 1 degree angle each.
>         so, need to make 358 new cuts.
>
>  */
>
>
> import java.util.*;
>
> public class CakePartition {
>
> 	public static void main(String[] args) {
> 		Scanner sc = new Scanner(System.in);
> 		
> 		int numOfPremadeCuts = sc.nextInt();
> 		
> 		
> 		int[] a = new int[numOfPremadeCuts];
> 		for (int j = 0; j < numOfPremadeCuts; j++) {
> 			a[j] = sc.nextInt();
> 		}
> 		
> 		int gcd = a[1] - a[0];
> 		for (int j = 2; j < numOfPremadeCuts; j++) {
> 			gcd = findGCD(gcd, a[j] - a[j - 1]);
> 		}
> 		
> 		gcd = findGCD(gcd, a[0] + 360 - a[numOfPremadeCuts - 1]);
> 		
> 		System.out.println((360 / gcd) - numOfPremadeCuts);
> 	
> }
>
> private static int findGCD(int a, int b) {
> 	if (b == 0) {
> 		return a;
> 	}
> 	return findGCD(b, a % b);
> }
>
>
> }
>
>
> /*
>
> =====TestCases======
> case =1
> input =3
> 30 60 90
> output =9
>
> case =2
> input =4
> 0 90 180 270
> output =0
>
> case =3
> input =5
> 10 30 60 100 150
> output =31
>
> case =4
> input =4
> 25 37 49 54
> output =356
>
> case =5
> input =2
> 0 1
> output =358
>
> case =6
> input =6
> 16 48 64 96 128 256 
> output =39
>
> case =7
> input =8
> 12 27 81 192 156 216 300 270
> output =112
>
> case =8
> input =3
> 60 120 210
> output =9
>
> case =9
> input =6
> 0 30 45 60 90 105
> output =18
>
> case =10
> input =9
> 12 36 72 78 84 120 132 150 180
> output =51
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2047%20Solutions/CakePartition.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 47 Solutions/CakePartition.java
