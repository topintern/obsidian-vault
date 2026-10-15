---
kind: "coding-problem"
title: "Milkand Cup (Day 122)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 122 solutions/Milkand Cup.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Milkand Cup (Day 122)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Ramu is a milk supplier to Somu. He has only two aluminium cups of capacity m and n litres..
Using these two cups, he can measure the milk. 
He has to supply exactly P litres of milk to Somu.

To measure the milk, operations allowed are:
	- Fill one of the cups completely with milk.
	- Empty the other cup.
	- Pour milk from one cup into another cup till it fills completely,
	 or the first cup itself is empty.
	 
Such that, at the end one or both cups contains P litres of the milk.
	
Please help Ramu, to check whether P litres of milk can be measured
using the two cups or not.

Input Format:
-------------
3 space separated integers, m, n and P.

Output Format:
--------------
Print a boolean value.


Sample Input-1:
---------------
3 5 4

Sample Output-1:
----------------
true


Sample Input-2:
---------------
2 4 5

Sample Output-2:
----------------
false

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Milkand Cup.java
> ```java
> /*
> Ramu is a milk supplier to Somu. He has only two aluminium cups of capacity m and n litres..
> Using these two cups, he can measure the milk. 
> He has to supply exactly P litres of milk to Somu.
>
> To measure the milk, operations allowed are:
> 	- Fill one of the cups completely with milk.
> 	- Empty the other cup.
> 	- Pour milk from one cup into another cup till it fills completely,
> 	 or the first cup itself is empty.
> 	 
> Such that, at the end one or both cups contains P litres of the milk.
> 	
> Please help Ramu, to check whether P litres of milk can be measured
> using the two cups or not.
>
> Input Format:
> -------------
> 3 space separated integers, m, n and P.
>
> Output Format:
> --------------
> Print a boolean value.
>
>
> Sample Input-1:
> ---------------
> 3 5 4
>
> Sample Output-1:
> ----------------
> true
>
>
> Sample Input-2:
> ---------------
> 2 4 5
>
> Sample Output-2:
> ----------------
> false
>
> */
> import java.util.*;
>
> class MilkandCup {
> 	public boolean canMeasureMilk(int x, int y, int z) {
> 		//limit brought by the statement that water is finallly in one or both buckets
> 		if(x + y < z) return false;
> 		//case x or y is zero
> 		if( x == z || y == z || x + y == z ) return true;
> 		
> 		//get GCD, then we can use the property of Bézout's identity
> 		return z%GCD(x, y) == 0;
> 	}
>
> 	public int GCD(int a, int b){
> 		while(b != 0 ){
> 			int temp = b;
> 			b = a%b;
> 			a = temp;
> 		}
> 		return a;
> 	}
>
> 	public static void main(String[] args) {
> 		Scanner sc = new Scanner(System.in);
> 		int m=sc.nextInt();
> 		int n=sc.nextInt();
> 		int P=sc.nextInt();
> 		System.out.print(new MilkandCup().canMeasureMilk(m,n,P));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20122%20solutions/Milkand%20Cup.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 122 solutions/Milkand Cup.java
