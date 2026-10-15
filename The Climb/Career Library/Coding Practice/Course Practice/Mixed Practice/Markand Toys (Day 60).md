---
kind: "coding-problem"
title: "Markand Toys (Day 60)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 60 Solutions/MarkandToys.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Markand Toys (Day 60)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Mark and Jane are very happy after having their first child. 
Their son loves toys, so Mark wants to buy some. 
There are a number of different toys lying in front of him, tagged with their prices. 
Mark has only a certain amount to spend, 
and he wants to maximize the number of toys he buys with this money.

Given a list of prices and an amount to spend, 
what is the maximum number of toys Mark can buy? 

For example, if prices=[1,2,3,4] and Mark has k=7 to spend, he can buy items [1,2,3] for 6, 
or [3,4] for 7 units of currency. He would choose the first group of 3 items.

Input Format:
	- The first line contains two integers, n and k, the number of priced toys and the amount Mark has to spend.
	- The next line contains n space-separated integers prices[i]

Note:A toy can't be bought multiple times.

Output Format:
	- An integer that denotes the maximum number of toys Mark can buy for his son.

Sample Input
	7 50
	1 12 5 111 200 1000 10
Sample Output
	4
Explanation
He can buy only 4 toys at most. These toys have the following prices: 1,12,5,10


========= Testcases Program-3 =========
case =1
input =7 50
1 12 5 111 200 1000 10
output =4

case =2
input =4 7
1 2 3 4
output =6

case =3
input =5 15
3 7 2 9 4
output =3

case =4
input =10 124
78 64 30 17 83 39 43 18 30 48
output =4

case =5
input =20 1024
350 803 965 568 123 636 473 268 201 284 199 312 622 155 109 640 141 827 574 839
output =6

case =6
input =15 1024
674 682 789 232 971 920 573 109 898 200 393 147 210 499 336
output =5

case =7
input =25 1575
334 996 112 932 293 442 905 796 231 193 290 659 454 399 636 462 259 371 966 778 247 765 811 518 147
output =7

case =8
input =25 5432
941 855 895 910 620 897 799 909 831 798 597 540 720 696 618 859 945 617 780 712 686 964 764 633 960
output =8

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MarkandToys.java
> ```java
> /*
> Mark and Jane are very happy after having their first child. 
> Their son loves toys, so Mark wants to buy some. 
> There are a number of different toys lying in front of him, tagged with their prices. 
> Mark has only a certain amount to spend, 
> and he wants to maximize the number of toys he buys with this money.
>
> Given a list of prices and an amount to spend, 
> what is the maximum number of toys Mark can buy? 
>
> For example, if prices=[1,2,3,4] and Mark has k=7 to spend, he can buy items [1,2,3] for 6, 
> or [3,4] for 7 units of currency. He would choose the first group of 3 items.
>
> Input Format:
> 	- The first line contains two integers, n and k, the number of priced toys and the amount Mark has to spend.
> 	- The next line contains n space-separated integers prices[i]
>
> Note:A toy can't be bought multiple times.
>
> Output Format:
> 	- An integer that denotes the maximum number of toys Mark can buy for his son.
>
> Sample Input
> 	7 50
> 	1 12 5 111 200 1000 10
> Sample Output
> 	4
> Explanation
> He can buy only 4 toys at most. These toys have the following prices: 1,12,5,10
>
>
> ========= Testcases Program-3 =========
> case =1
> input =7 50
> 1 12 5 111 200 1000 10
> output =4
>
> case =2
> input =4 7
> 1 2 3 4
> output =6
>
> case =3
> input =5 15
> 3 7 2 9 4
> output =3
>
> case =4
> input =10 124
> 78 64 30 17 83 39 43 18 30 48
> output =4
>
> case =5
> input =20 1024
> 350 803 965 568 123 636 473 268 201 284 199 312 622 155 109 640 141 827 574 839
> output =6
>
> case =6
> input =15 1024
> 674 682 789 232 971 920 573 109 898 200 393 147 210 499 336
> output =5
>
> case =7
> input =25 1575
> 334 996 112 932 293 442 905 796 231 193 290 659 454 399 636 462 259 371 966 778 247 765 811 518 147
> output =7
>
> case =8
> input =25 5432
> 941 855 895 910 620 897 799 909 831 798 597 540 720 696 618 859 945 617 780 712 686 964 764 633 960
> output =8
>
> */
>
> import java.io.*;
> import java.util.*;
>
> public class MarkandToys {
> 	public static void main(String[] args) {
> 		Scanner scn=new Scanner(System.in);
> 		
> 		int n=scn.nextInt();
> 		int arr[]=new int[n];
> 		
> 		int k=scn.nextInt();
> 		
> 		for(int i=0;i<n;i++)
> 		{
> 			arr[i]=scn.nextInt();
> 		}
> 		long count=0L;
> 		long add=0L;
> 		Arrays.sort(arr);
> 		for(int i=0;i<n;i++)
> 		{
> 			if(arr[i]<k)
> 			{
> 			add=add+arr[i];
> 				if(add<k)
> 				{
> 					count++;		
> 				}
> 			}			
> 		}
>         System.out.println(count);		
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2060%20Solutions/MarkandToys.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 60 Solutions/MarkandToys.java
