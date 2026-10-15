---
kind: "coding-problem"
title: "NDiv Subset (Day 61)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 61 Solutions/NDivSubset.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# NDiv Subset (Day 61)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a set of distinct integers, print the size of a maximal subset of S 
where the sum of any 2 numbers in S' is not evenly divisible by k.

For example, the array S={19,10,12,24,25,22} and k=4. 
One of the arrays that can be created is S'[0]={10,12,25}. 
Another is S'[1]={19,22,24}. 
After testing all permutations, the maximum length solution array has 3 elements.

Input Format:
	- The first line contains 2 space-separated integers, n and k, 
	  the number of values in S and the non factor.
	- The second line contains n space-separated integers describing S[i], 
	  the unique values of the set.
Note: All of the given numbers are distinct.

Output Format:
Print the size of the largest possible subset (S').

Sample Input
4 3
1 7 2 4

Sample Output
3

Explanation
The sums of all permutations of two elements from S={1,7,2,4} are:
	1 + 7 = 8
	1 + 2 = 3
	1 + 4 = 5
	7 + 2 = 9
	7 + 4 = 11
	2 + 4 = 6
We see that only S'={1,7,4} will not ever sum to a multiple of 3.


========= Testcases Program-2 =========
case =1
input =4 3
1 7 2 4
output =3

case =2
input =5 5
2 7 12 17 22
output =5

case =3
input =10 5
770528134 663501748 384261537 800309024 103668401 538539662 385488901 101262949 557792122 46058493
output =6

case =4
input =5 1
1 2 3 4 5
output =1

case =5
input =10 4
1 2 3 4 5 6 7 8 9 10
output =5

case =6
input =15 7
278 576 496 727 410 124 338 149 209 702 282 718 771 575 436
output =11

case =7
input =13 11
582740017 954896345 590538156 298333230 859747706 155195851 331503493 799588305 164222042 563356693 80522822 432354938 652248359
output =11

case =8
input =6 9
422346306 940894801 696810740 862741861 85835055 313720373
output =5

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · NDivSubset.java
> ```java
> /*
> Given a set of distinct integers, print the size of a maximal subset of S 
> where the sum of any 2 numbers in S' is not evenly divisible by k.
>
> For example, the array S={19,10,12,24,25,22} and k=4. 
> One of the arrays that can be created is S'[0]={10,12,25}. 
> Another is S'[1]={19,22,24}. 
> After testing all permutations, the maximum length solution array has 3 elements.
>
> Input Format:
> 	- The first line contains 2 space-separated integers, n and k, 
> 	  the number of values in S and the non factor.
> 	- The second line contains n space-separated integers describing S[i], 
> 	  the unique values of the set.
> Note: All of the given numbers are distinct.
>
> Output Format:
> Print the size of the largest possible subset (S').
>
> Sample Input
> 4 3
> 1 7 2 4
>
> Sample Output
> 3
>
> Explanation
> The sums of all permutations of two elements from S={1,7,2,4} are:
> 	1 + 7 = 8
> 	1 + 2 = 3
> 	1 + 4 = 5
> 	7 + 2 = 9
> 	7 + 4 = 11
> 	2 + 4 = 6
> We see that only S'={1,7,4} will not ever sum to a multiple of 3.
>
>
> ========= Testcases Program-2 =========
> case =1
> input =4 3
> 1 7 2 4
> output =3
>
> case =2
> input =5 5
> 2 7 12 17 22
> output =5
>
> case =3
> input =10 5
> 770528134 663501748 384261537 800309024 103668401 538539662 385488901 101262949 557792122 46058493
> output =6
>
> case =4
> input =5 1
> 1 2 3 4 5
> output =1
>
> case =5
> input =10 4
> 1 2 3 4 5 6 7 8 9 10
> output =5
>
> case =6
> input =15 7
> 278 576 496 727 410 124 338 149 209 702 282 718 771 575 436
> output =11
>
> case =7
> input =13 11
> 582740017 954896345 590538156 298333230 859747706 155195851 331503493 799588305 164222042 563356693 80522822 432354938 652248359
> output =11
>
> case =8
> input =6 9
> 422346306 940894801 696810740 862741861 85835055 313720373
> output =5
>
> */
>
> import java.util.*;
> import java.math.*;
>
> public class NDivSubset {
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         int n = in.nextInt();
>         int k = in.nextInt();
>         int a[] = new int[n];
>         int cnts[] = new int[k];
>         for(int a_i=0; a_i < n; a_i++){
>             a[a_i] = in.nextInt();
>             cnts[a[a_i]%k]++;
>         }
>         int cnt = 0;
>         for (int i=1;i<=k/2;i++) {
>             if (2*i!=k) {
>                 cnt += Math.max(cnts[i],cnts[k-i]);
>             }
>         }
>         if (k%2==0) {
>             if (cnts[k/2]>0) {
>                 cnt ++;
>             }
>         }
>         if (cnts[0]>0) {
>             cnt ++;
>         }
>         System.out.println(cnt);
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2061%20Solutions/NDivSubset.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 61 Solutions/NDivSubset.java
