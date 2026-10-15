---
kind: "coding-problem"
title: "Vehicle Capacity (Day 112)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 112 Solutions/VehicleCapacity.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Vehicle Capacity (Day 112)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

UBER driver has a vehicle, daily he used go in only one direction.
Capacity of the vehicle is S (no of seats except driver seat), 

Given a list of N bookings, booking[i]= [ num_customers, pickup, drop ].
booking indicates, number of customers to pick up, and pick up, droping points.

Initially the vehicle is empty.

Return true if and only if it is possible to pick up and drop off all customers of all bookings.

Input Format:
-------------
Line-1 -> Two integers N and S, number of bookings and number of seats in the vehicle.
Next N Lines -> three space separated integers, num_customers, pickup point, dropping point

Output Format:
--------------
Print a boolean value.


Sample Input-1:
---------------
2 5
2 1 5
3 3 7

Sample Output-1:
----------------
true


Sample Input-2:
---------------
2 4
2 1 5
3 3 7

Sample Output-2:
----------------
false


Sample Input-3:
---------------
3 11
3 2 7
3 7 9
8 3 9

Sample Output-3:
----------------
true

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · VehicleCapacity.java
> ```java
> /*
> UBER driver has a vehicle, daily he used go in only one direction.
> Capacity of the vehicle is S (no of seats except driver seat), 
>
> Given a list of N bookings, booking[i]= [ num_customers, pickup, drop ].
> booking indicates, number of customers to pick up, and pick up, droping points.
>
> Initially the vehicle is empty.
>
> Return true if and only if it is possible to pick up and drop off all customers of all bookings.
>
> Input Format:
> -------------
> Line-1 -> Two integers N and S, number of bookings and number of seats in the vehicle.
> Next N Lines -> three space separated integers, num_customers, pickup point, dropping point
>
> Output Format:
> --------------
> Print a boolean value.
>
>
> Sample Input-1:
> ---------------
> 2 5
> 2 1 5
> 3 3 7
>
> Sample Output-1:
> ----------------
> true
>
>
> Sample Input-2:
> ---------------
> 2 4
> 2 1 5
> 3 3 7
>
> Sample Output-2:
> ----------------
> false
>
>
> Sample Input-3:
> ---------------
> 3 11
> 3 2 7
> 3 7 9
> 8 3 9
>
> Sample Output-3:
> ----------------
> true
>
> */
>
> import java.util.*;
>
> class VehicleCapacity{
> 	public boolean vehicleCapacity(int[][] bookings, int capacity) {    
> 		int stops[] = new int[1001]; 
> 		for (int t[] : bookings) {
> 		  stops[t[1]] += t[0];
> 		  stops[t[2]] -= t[0];
> 		}
> 		for (int i = 0; capacity >= 0 && i < 1001; ++i) capacity -= stops[i];
> 		return capacity >= 0;
> 	}
> 	
> 	public static void main(String args[] ) {
>
> 		Scanner scan = new Scanner(System.in);
> 		int N=scan.nextInt();
> 		int Cap=scan.nextInt();      
>
> 		int[][] bookings=new int[N][3];
> 		for(int i=0; i<N; i++)
> 		{
> 			for(int j=0; j<3; j++)
> 			{
> 			   bookings[i][j] = scan.nextInt();
> 			}
> 		}
> 		System.out.println(new VehicleCapacity().vehicleCapacity(bookings,Cap));
> 	} 	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20112%20Solutions/VehicleCapacity.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 112 Solutions/VehicleCapacity.java
