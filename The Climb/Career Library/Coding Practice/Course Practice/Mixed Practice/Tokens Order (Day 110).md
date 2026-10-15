---
kind: "coding-problem"
title: "Tokens Order (Day 110)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 110 Solutions/TokensOrder.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Tokens Order (Day 110)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

In a maths class, Teahcer given a task to a student.
Initially, Teacher provided a set of tokens(one on another) to the student
All the tokens are printed a positive number on one side and empty on other side
Intially, the number side of tokens are hidden.

Now, you do the following steps repeatedly, until all tokens are turned up:
1. Take the top token of the set, show the number, and take it out of the set.
2. If there are still tokens in the set, put the next top token of the set at the bottom of the set.
3. If there are still hidden tokens, go back to step 1. Otherwise, stop.
Return an ordering of the set that would show the tokens in increasing order.
The first entry in the answer is considered to be the top of the set.

Input Format:
-------------
Line-1 -> An integer N, no of tokens
Line-2 -> N space separated integers.

Output Format:
--------------
Print N space separated integers as result.


Sample Input-1:
---------------
7 6 5 1 2 3 4

Sample Output-1:
----------------
1 6 2 5 3 7 4


### Explanation: 

---------------
Given a set in the order 7 6 5 1 2 3 4
After reordering, the set starts as 1 6 2 5 3 7 4, where 1 is the top of the set.
Student show 1, and move 6 to the bottom.  The set is now 2 5 3 7 4 6.
Student show 2, and move 5 to the bottom.  The set is now 3 7 4 6 5.
Student show 3, and move 7 to the bottom.  The set is now 4 6 5 7
Student show 4, and move 6 to the bottom.  The set is now 5 7 6
Student show 5. and move 7 to the bottom.  The set is now 6 7
Student show 6, and move 7 to the bottom.  The set is now 7
Student show 7.
Since all the cards revealed are in increasing order, the answer is correct.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · TokensOrder.txt
> ```java
> /*
> In a maths class, Teahcer given a task to a student.
> Initially, Teacher provided a set of tokens(one on another) to the student
> All the tokens are printed a positive number on one side and empty on other side
> Intially, the number side of tokens are hidden.
>
> Now, you do the following steps repeatedly, until all tokens are turned up:
> 1. Take the top token of the set, show the number, and take it out of the set.
> 2. If there are still tokens in the set, put the next top token of the set at the bottom of the set.
> 3. If there are still hidden tokens, go back to step 1. Otherwise, stop.
> Return an ordering of the set that would show the tokens in increasing order.
> The first entry in the answer is considered to be the top of the set.
>
> Input Format:
> -------------
> Line-1 -> An integer N, no of tokens
> Line-2 -> N space separated integers.
>
> Output Format:
> --------------
> Print N space separated integers as result.
>
>
> Sample Input-1:
> ---------------
> 7 6 5 1 2 3 4
>
> Sample Output-1:
> ----------------
> 1 6 2 5 3 7 4
>
> Explanation: 
> ---------------
> Given a set in the order 7 6 5 1 2 3 4
> After reordering, the set starts as 1 6 2 5 3 7 4, where 1 is the top of the set.
> Student show 1, and move 6 to the bottom.  The set is now 2 5 3 7 4 6.
> Student show 2, and move 5 to the bottom.  The set is now 3 7 4 6 5.
> Student show 3, and move 7 to the bottom.  The set is now 4 6 5 7
> Student show 4, and move 6 to the bottom.  The set is now 5 7 6
> Student show 5. and move 7 to the bottom.  The set is now 6 7
> Student show 6, and move 7 to the bottom.  The set is now 7
> Student show 7.
> Since all the cards revealed are in increasing order, the answer is correct.
> */
>
> import java.util.*;
>
> class TokensOrder {
>     public int[] setShownIncreasing(int[] set) {
>         int n= set.length;
>         Arrays.sort(set);
>         Queue<Integer> q= new LinkedList<>();
>         for (int i=0; i<n; i++) q.add(i);
>         int[] res= new int[n];
>         for (int i=0; i<n; i++){
>             res[q.poll()]=set[i];
>             q.add(q.poll());
>         }
>         return res;
>     }
> 	
> 	public static void main(String args[])
> 	{
> 		Scanner sc = new Scanner(System.in);
> 		int N=sc.nextInt();
> 		int array[]=new int[N];
> 		
> 		for(int i=0;i<N;i++)
> 			array[i]=sc.nextInt();
> 		int result[]=new TokensOrder().setShownIncreasing(array);
> 		for(int i:result)
> 		System.out.print(i+" ");
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20110%20Solutions/TokensOrder.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 110 Solutions/TokensOrder.txt
