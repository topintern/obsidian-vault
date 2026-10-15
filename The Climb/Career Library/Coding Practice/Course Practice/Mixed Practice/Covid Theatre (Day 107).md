---
kind: "coding-problem"
title: "Covid Theatre (Day 107)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 107 Solutions/CovidTheatre.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Covid Theatre (Day 107)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Telangana Government planning to re-open the theatres in september.
Due to COVID-19 pandemic, theatre owners planning to guide the audience to sit 
in the seat that maximizes the distance to the closest person, in order to
practice the social distance in theatres.

Please help usher to guide the audience to sit in a seat by following few rules:

- There are N seats in a single row, seats are numbered from 0 to N-1.
- Maximize the distance from person to the closest person.
- If there are multiple seats with similar distance, they sit in the seat with the lowest number.
- First person always sit in seat number 0.
- If a person leaves the theatre from a seat, please consider that the seat is vacant

Create a class Theater and two functions in it.
1. int seat(): represent the seat number of audience to sit.
2. void leave(int s): person leaves the theatre from a seat number 's'.

Input Format:
----------------
Line-1 -> two integers N and P, Number of seats N, Number of Processes P
P lines of input -> each line contains funtion number and parameter list.

Output Format:
------------------
Print the alloted seat numbers in one line as output.


Sample Input-1:
-------------------
10 6
1
1
1
1
2 4
1

Sample Output-1:
---------------------
0 9 4 2 5

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · CovidTheatre.txt
> ```java
> /*
> Telangana Government planning to re-open the theatres in september.
> Due to COVID-19 pandemic, theatre owners planning to guide the audience to sit 
> in the seat that maximizes the distance to the closest person, in order to
> practice the social distance in theatres.
>
> Please help usher to guide the audience to sit in a seat by following few rules:
>
> - There are N seats in a single row, seats are numbered from 0 to N-1.
> - Maximize the distance from person to the closest person.
> - If there are multiple seats with similar distance, they sit in the seat with the lowest number.
> - First person always sit in seat number 0.
> - If a person leaves the theatre from a seat, please consider that the seat is vacant
>
> Create a class Theater and two functions in it.
> 1. int seat(): represent the seat number of audience to sit.
> 2. void leave(int s): person leaves the theatre from a seat number 's'.
>
> Input Format:
> ----------------
> Line-1 -> two integers N and P, Number of seats N, Number of Processes P
> P lines of input -> each line contains funtion number and parameter list.
>
> Output Format:
> ------------------
> Print the alloted seat numbers in one line as output.
>
>
> Sample Input-1:
> -------------------
> 10 6
> 1
> 1
> 1
> 1
> 2 4
> 1
>
> Sample Output-1:
> ---------------------
> 0 9 4 2 5
>
> */
>
> import java.util.*;
>
> class Theatre{
> 	int N;
>     ArrayList<Integer> L = new ArrayList<>();
>     public Theatre(int n) {
>         N = n;
>     }
>
>     public int seat() {
>         if (L.size() == 0) {
>             L.add(0);
>             return 0;
>         }
>         int d = Math.max(L.get(0), N - 1 - L.get(L.size() - 1));
>         for (int i = 0; i < L.size() - 1; ++i) d = Math.max(d, (L.get(i + 1) - L.get(i)) / 2);
>         if (L.get(0) == d) {
>             L.add(0, 0);
>             return 0;
>         }
>         for (int i = 0; i < L.size() - 1; ++i)
>             if ((L.get(i + 1) - L.get(i)) / 2 == d) {
>                 L.add(i + 1, (L.get(i + 1) + L.get(i)) / 2);
>                 return L.get(i + 1);
>             }
>         L.add(N - 1);
>         return N - 1;
>     }
>
>     public void leave(int p) {
>         for (int i = 0; i < L.size(); ++i) if (L.get(i) == p) L.remove(i);
>     }
> }
> class Solution
> {
> 	public static void main(String args[])
> 	{
> 		Scanner sc= new Scanner(System.in);
> 		int N=sc.nextInt();	// Row size
> 		int P=sc.nextInt();	// Number of Operations
> 		Theatre t=new Theatre(N);
> 		
> 		for(int i=0;i<P;i++)
> 		{
> 			switch(sc.nextInt())
> 			{
> 				case 1:
> 					System.out.print(t.seat()+" ");
> 					break;
> 				case 2:
> 					t.leave(sc.nextInt());
> 			}
> 		}
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20107%20Solutions/CovidTheatre.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 107 Solutions/CovidTheatre.txt
