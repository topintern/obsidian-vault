---
kind: "coding-problem"
title: "Savethe Prisoner (Day 61)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 61 Solutions/SavethePrisoner.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Savethe Prisoner (Day 61)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

A jail has a number of prisoners and a number of treats to pass out to them. 
Their jailer decides the fairest way to divide the treats is to seat 
the prisoners around a circular table in sequentially numbered chairs. 
A chair number will be drawn from a hat. 
Beginning with the prisoner in that chair, one candy will be handed to each prisoner 
sequentially around the table until all have been distributed.

The jailer is playing a little joke, though. 
The last piece of candy looks like all the others, but it tastes awful. 
Determine the chair number occupied by the prisoner who will receive that candy.

For example, there are 4 prisoners and 6 pieces of candy. 
The prisoners arrange themselves in seats numbered 1 to 4. 
Let's suppose two is drawn from the hat. 
Prisoners receive candy at positions 2,3,4,1,2,3. The prisoner who receives the awful treat, sits in chair number .

Input Format:
Line contain 3 space-separated integers:
-n : the number of prisoners
-m : the number of sweets
-s : the chair number to start passing out treats at

Output Format:
Print the chair number of the prisoner who receives the awful treat.

Sample Input-1
5 2 2
Sample Output-1
3
Explanation-1
Distribution starts at seat 2 so prisoners in seats 2 and 3 get sweets. Warn prisoner 3	.

Sample Input-2
7 19 2
Sample Output-2
6
Explanation-2
There are 7 prisoners, 19 sweets and they are passed out starting at chair 2. 
The candies go all around twice and there are 5 more candies passed to each prisoner from seat 2 to seat 6.


========= Testcases Program-3 =========
case =1
input =144 797951344 1
output =112

case =2
input =17 900306316 1
output =1

case =3
input =169 647839529 169
output =167

case =4
input =5 311730064 2
output =5

case =5
input =4 463934462 4
output =1

case =6
input =155634995 840192364 67379577
output =129396965

case =7
input =543780156 962564973 467116054
output =342120714

case =8
input =984873585 997634055 103050157
output =115810626

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SavethePrisoner.java
> ```java
> /*
>
> A jail has a number of prisoners and a number of treats to pass out to them. 
> Their jailer decides the fairest way to divide the treats is to seat 
> the prisoners around a circular table in sequentially numbered chairs. 
> A chair number will be drawn from a hat. 
> Beginning with the prisoner in that chair, one candy will be handed to each prisoner 
> sequentially around the table until all have been distributed.
>
> The jailer is playing a little joke, though. 
> The last piece of candy looks like all the others, but it tastes awful. 
> Determine the chair number occupied by the prisoner who will receive that candy.
>
> For example, there are 4 prisoners and 6 pieces of candy. 
> The prisoners arrange themselves in seats numbered 1 to 4. 
> Let's suppose two is drawn from the hat. 
> Prisoners receive candy at positions 2,3,4,1,2,3. The prisoner who receives the awful treat, sits in chair number .
>
> Input Format:
> Line contain 3 space-separated integers:
> -n : the number of prisoners
> -m : the number of sweets
> -s : the chair number to start passing out treats at
>
> Output Format:
> Print the chair number of the prisoner who receives the awful treat.
>
> Sample Input-1
> 5 2 2
> Sample Output-1
> 3
> Explanation-1
> Distribution starts at seat 2 so prisoners in seats 2 and 3 get sweets. Warn prisoner 3	.
>
> Sample Input-2
> 7 19 2
> Sample Output-2
> 6
> Explanation-2
> There are 7 prisoners, 19 sweets and they are passed out starting at chair 2. 
> The candies go all around twice and there are 5 more candies passed to each prisoner from seat 2 to seat 6.
>
>
> ========= Testcases Program-3 =========
> case =1
> input =144 797951344 1
> output =112
>
> case =2
> input =17 900306316 1
> output =1
>
> case =3
> input =169 647839529 169
> output =167
>
> case =4
> input =5 311730064 2
> output =5
>
> case =5
> input =4 463934462 4
> output =1
>
> case =6
> input =155634995 840192364 67379577
> output =129396965
>
> case =7
> input =543780156 962564973 467116054
> output =342120714
>
> case =8
> input =984873585 997634055 103050157
> output =115810626
>
> */
>
> import java.util.*;
>
> public class SavethePrisoner {
>     public static void main(String[] args) {
>         /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
>         final Scanner scan = new Scanner(System.in);
>         int t = scan.nextInt();
>         long n, m, s;
>         long mod;
>         for (int i = 0; i < t; ++i) {
>             n = scan.nextLong();
>             m = scan.nextLong();
>             s = scan.nextLong();              
>             mod = (m - 1 + s) % n;
>             if ( mod == 0) {
>                 System.out.println(n); 
>             } else {
>                 System.out.println(mod);
>             }
>         }        
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2061%20Solutions/SavethePrisoner.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 61 Solutions/SavethePrisoner.java
