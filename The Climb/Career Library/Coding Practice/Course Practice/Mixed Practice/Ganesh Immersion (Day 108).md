---
kind: "coding-problem"
title: "Ganesh Immersion (Day 108)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 108 Solutions/GaneshImmersion.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Ganesh Immersion (Day 108)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Every year after Lord Ganesh chaturthi, Ganesh idols of various sizes are to be immersed 
in the Hussain Sagar lake. There is a need of  'K' cranes to immerse idols into lake.

There are 'N' number of Ganesh idols with the given sizes, 
where 'i'th idol size is idolsize[i].
and each Crane can handle maximum size 'S'. 

Each Crane carries at most 2 idols at the same time, 
and the sum of the sizes of those idols should be <= 'S'.
Find out the minimum number of Cranes 'K' required to perform immersion of all the idols.

Note: It is guaranteed that a Crane can carry one ganesh idol of any zize.

Input Format:
----------------
Line-1 -> Two Integers, N and S
Line-2 -> N space separated integers, idolsize[]

Output Format:
------------------
Print an integer as result.


Sample Input-1:
-------------------
4 3
3 2 2 1

Sample Output-1:
---------------------
3


### Explanation: 

----------------
3 Cranes required (1, 2), (2) and (3).

Sample Input-2:
-------------------
4 5
3 5 3 3

Sample Output-2:
---------------------
4


### Explanation: 

----------------
4 Cranes required (3), (3), (4), (5)

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · GaneshImmersion.txt
> ```java
> /*
>
> Every year after Lord Ganesh chaturthi, Ganesh idols of various sizes are to be immersed 
> in the Hussain Sagar lake. There is a need of  'K' cranes to immerse idols into lake.
>
> There are 'N' number of Ganesh idols with the given sizes, 
> where 'i'th idol size is idolsize[i].
> and each Crane can handle maximum size 'S'. 
>
> Each Crane carries at most 2 idols at the same time, 
> and the sum of the sizes of those idols should be <= 'S'.
> Find out the minimum number of Cranes 'K' required to perform immersion of all the idols.
>
> Note: It is guaranteed that a Crane can carry one ganesh idol of any zize.
>
> Input Format:
> ----------------
> Line-1 -> Two Integers, N and S
> Line-2 -> N space separated integers, idolsize[]
>
> Output Format:
> ------------------
> Print an integer as result.
>
>
> Sample Input-1:
> -------------------
> 4 3
> 3 2 2 1
>
> Sample Output-1:
> ---------------------
> 3
>
> Explanation: 
> ----------------
> 3 Cranes required (1, 2), (2) and (3).
>
> Sample Input-2:
> -------------------
> 4 5
> 3 5 3 3
>
> Sample Output-2:
> ---------------------
> 4
>
> Explanation: 
> ----------------
> 4 Cranes required (3), (3), (4), (5)
>
> */
>
> import java.util.*;
>
> class GaneshImmersion
> {
> 	public static int numImmerseCranes(int[] idolsize, int size) {
>         Arrays.sort(idolsize);
>         int i, j;
>         for (i = 0, j = idolsize.length - 1; i <= j; --j)
>             if (idolsize[i] + idolsize[j] <= size) ++i;
>         return idolsize.length - 1 - j;
>     }
> 	public static void main(String args[])
> 	{
> 		Scanner sc=new Scanner(System.in);
> 		int n=sc.nextInt();
> 		int size=sc.nextInt();
> 		int idolsize[]=new int[n];
> 		for(int i=0;i<n;i++)
> 			idolsize[i]=sc.nextInt();
> 		
> 		System.out.println(numImmerseCranes(idolsize,size));
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20108%20Solutions/GaneshImmersion.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 108 Solutions/GaneshImmersion.txt
