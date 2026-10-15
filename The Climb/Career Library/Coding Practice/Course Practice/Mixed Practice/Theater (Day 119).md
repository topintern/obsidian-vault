---
kind: "coding-problem"
title: "Theater (Day 119)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 119 Solutons/Theater.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Theater (Day 119)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

The laser show at Lumbini park started online bookings,
It is an open theater having n rows of seats, each row consist of 10 seats.
The seats are labelled from 1 to 10 numbers, as shown below.

	Row	1 2 3	4 5 6 7 	8 9 10
		1	_ _ _	_ _ _ _		_ _ _
		2	_ _ _	_ _ _ _		_ _ _
		......
		n	_ _ _	_ _ _ _		_ _ _

You will be given n value, and a list of booked seats booked[],
i.e, booked[x]= [i,j] indicates, i-th row j-th labelled seat is booked.

If a family-group of four members have to book the seats,
with the conditions are as follows:
	- Book four adjacent seats in a single row.
	- Seats across walkway (3 and 4) or (7 and 8) are not considered to be adjacent, 
	- There is an exceptional case on which the walkway split a four members group, 
	   in to two people on each side of walkway, like [2,3 4,5] or [6,7 8,9].
	   
Find out, the maximum number of family groups can book the seats,

	   
Input Format:
-------------
Line-1: Two integers n and b, number of rows, and number of bookings.
next b lines: two integers i, j, row number and seat number.

Output Format:
--------------
Print an intger, the number of ways.



### Sample Input

---------------
3 6
1 2
1 3
1 8
2 6
3 1
3 10


### Sample Output

----------------
4


### Explanation

------------
Row		1 2 3	4 5 6 7 	8 9 10
	1		_ x x	b b b b		x _ _
	2		_ b b	b b x _		_ _ _
	3		x b b	b b b b		b b x
		
In row-1, we can fit for 1 family-group
In row-2, we can fit for 1 family-group
In row-3, we can fit for 2 family-groups

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Theater.java
> ```java
> /*
> The laser show at Lumbini park started online bookings,
> It is an open theater having n rows of seats, each row consist of 10 seats.
> The seats are labelled from 1 to 10 numbers, as shown below.
>
> 	Row	1 2 3	4 5 6 7 	8 9 10
> 		1	_ _ _	_ _ _ _		_ _ _
> 		2	_ _ _	_ _ _ _		_ _ _
> 		......
> 		n	_ _ _	_ _ _ _		_ _ _
>
> You will be given n value, and a list of booked seats booked[],
> i.e, booked[x]= [i,j] indicates, i-th row j-th labelled seat is booked.
>
> If a family-group of four members have to book the seats,
> with the conditions are as follows:
> 	- Book four adjacent seats in a single row.
> 	- Seats across walkway (3 and 4) or (7 and 8) are not considered to be adjacent, 
> 	- There is an exceptional case on which the walkway split a four members group, 
> 	   in to two people on each side of walkway, like [2,3 4,5] or [6,7 8,9].
> 	   
> Find out, the maximum number of family groups can book the seats,
>
> 	   
> Input Format:
> -------------
> Line-1: Two integers n and b, number of rows, and number of bookings.
> next b lines: two integers i, j, row number and seat number.
>
> Output Format:
> --------------
> Print an intger, the number of ways.
>
>
> Sample Input:
> ---------------
> 3 6
> 1 2
> 1 3
> 1 8
> 2 6
> 3 1
> 3 10
>
> Sample Output:
> ----------------
> 4
>
> Explanation:
> ------------
> Row		1 2 3	4 5 6 7 	8 9 10
> 	1		_ x x	b b b b		x _ _
> 	2		_ b b	b b x _		_ _ _
> 	3		x b b	b b b b		b b x
> 		
> In row-1, we can fit for 1 family-group
> In row-2, we can fit for 1 family-group
> In row-3, we can fit for 2 family-groups
> 	
> */
>
> import java.util.*;
> class Theater{
>
> 	public int maxNumberOfFamilies(int n, int[][] reservedSeats) {
> 		Map<Integer, Integer> states = new HashMap<>();
> 		for (int[] seat : reservedSeats) {
> 		  states.put(seat[0],  states.getOrDefault(seat[0], 0) | 1 << (10 - seat[1]));
> 		}
> 		System.out.println(states);
> 		int max = (n - states.size()) * 2;
> 		for (int row : states.keySet()) {
> 		  int state = states.get(row);
> 		  boolean c4 = (state & 0b0001111000) == 0;
> 		  boolean c2 = (state & 0b0111100000) == 0;
> 		  boolean c6 = (state & 0b0000011110) == 0;
> 		  if (c2 && c6) max += 2;
> 		  else if (c4 || c2 || c6) max += 1;
> 		}
> 		return max;
> 	}
> 	
> 	public static void main(String args[] )  {
>     	Scanner sc = new Scanner(System.in);
> 		int n=sc.nextInt();
> 		int r=sc.nextInt();
> 		int reserved[][]=new int[r][2];
> 		for(int i=0;i<r;i++){
> 			reserved[i][0]=sc.nextInt();
> 			reserved[i][1]=sc.nextInt();
> 		}
> 		System.out.println(new Theater().maxNumberOfFamilies(n,reserved));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20119%20Solutons/Theater.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 119 Solutons/Theater.java
