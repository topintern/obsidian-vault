---
kind: "coding-problem"
title: "Jim Sky (Day 46)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 46 Solutions/JimSky.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Jim Sky (Day 46)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Sujeeth has created flying machine named Sahoo-JET. 
Sahoo-Jet can only fly horizontally, independent of the environment. 
One day, Sujeeth started his flight from Dubai's highest tower, 
traveled some distance and landed on another tower of same height! 
So much fun! But unfortunately, new towers have been built recently.

Let us describe the problem in one dimensional space. We have in total N
towers aligned from left to right. The i-th tower has a height of h(i). 
A flying route can be described as (i,j) with i!=j, which means, 
Sujeeth starts his Saaho-JET at the top of the tower i and lands on the tower j. 

Since Saaho-JET can only fly horizontally, Sujeeth will remain at the height h(i) only. 
Thus the path (i,j) can be valid, only if each of the towers i,i+1....,j+1,j is not 
strictly greater than h(i) and if the height of the tower he starts from and 
arrives on have the same height. 

Help Sujeeth in counting the number of valid paths represented by ordered pairs (i,j).

Input Format:
-------------
The first line contains N, the number of towers. 
The next line contains N space separated integers representing the heights of the towers.

Output Format:
--------------
Print an integer that denotes the number of valid routes.

Sample-1
    Input :
    6
    3 2 1 2 3 3
    Output :
    8

    Explanation :
        The first line contains the number of towers. 
        The next line contains space separated integers representing the heights of the towers. 
    
        ==>   tower at position 1 can jump on tower at position 5,6 
        because of same height and towers in between is less height.
        ==>    tower at position 2 can jump on tower at position 4 
        because of same height and tower in between is less height.
        ==>   tower at position 5 can jump on tower at position 6 
        because of same height and towers in between is less height.
        ==>   total 4 jumps possible from left to right, 
        another 4 jumps possible from right to left so total 8 jumps possible.

Sample-2:
    Input:
    3
    1 1000 1
    Output:
    0
    Explanation:
        ==>   tower at position 1 cannot jump on tower at position 3
        because of tower in between has more height.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · JimSky.java
> ```java
> /*
> Sujeeth has created flying machine named Sahoo-JET. 
> Sahoo-Jet can only fly horizontally, independent of the environment. 
> One day, Sujeeth started his flight from Dubai's highest tower, 
> traveled some distance and landed on another tower of same height! 
> So much fun! But unfortunately, new towers have been built recently.
>
> Let us describe the problem in one dimensional space. We have in total N
> towers aligned from left to right. The i-th tower has a height of h(i). 
> A flying route can be described as (i,j) with i!=j, which means, 
> Sujeeth starts his Saaho-JET at the top of the tower i and lands on the tower j. 
>
> Since Saaho-JET can only fly horizontally, Sujeeth will remain at the height h(i) only. 
> Thus the path (i,j) can be valid, only if each of the towers i,i+1....,j+1,j is not 
> strictly greater than h(i) and if the height of the tower he starts from and 
> arrives on have the same height. 
>
> Help Sujeeth in counting the number of valid paths represented by ordered pairs (i,j).
>
> Input Format:
> -------------
> The first line contains N, the number of towers. 
> The next line contains N space separated integers representing the heights of the towers.
>
> Output Format:
> --------------
> Print an integer that denotes the number of valid routes.
>
> Sample-1
>     Input :
>     6
>     3 2 1 2 3 3
>     Output :
>     8
>
>     Explanation :
>         The first line contains the number of towers. 
>         The next line contains space separated integers representing the heights of the towers. 
>     
>         ==>   tower at position 1 can jump on tower at position 5,6 
>         because of same height and towers in between is less height.
>         ==>    tower at position 2 can jump on tower at position 4 
>         because of same height and tower in between is less height.
>         ==>   tower at position 5 can jump on tower at position 6 
>         because of same height and towers in between is less height.
>         ==>   total 4 jumps possible from left to right, 
>         another 4 jumps possible from right to left so total 8 jumps possible.
>
> Sample-2:
>     Input:
>     3
>     1 1000 1
>     Output:
>     0
>     Explanation:
>         ==>   tower at position 1 cannot jump on tower at position 3
>         because of tower in between has more height.
>
> */
>
> import java.util.ArrayList;
> import java.util.List;
> import java.util.Scanner;
> import java.util.Stack;
>
> public class JimSky {
>
> 	public static void main(String[] args) {
> 		int[] a;
> 		Scanner sc = new Scanner(System.in);
> 			int n = sc.nextInt();
> 			a = new int[n];
> 			for (int i = 0; i < n; i++) {
> 				a[i] = sc.nextInt();// input all heights of skyscrapers
> 			}
> 		
> 		Stack<List<Integer>> start = new Stack<>();
> 		
> 		long c = 0;
> 		for (int i = 0; i < a.length; i++) {
> 			//make sure skyscraper heights are in descending order.
> 			//if not , remove the less height skyscraper from the stack
> 			while (!start.empty() && start.peek().get(0) < a[i]) {
> 				start.pop();
> 			}
> 			//compare top of the stack skyscraper height with current skyscraper height
> 			//if both are equal,  
> 			if (!start.empty() && start.peek().get(0) == a[i]) {
> 				c += start.peek().get(1);//increment the count by frequency of current skyscraper
> 				start.peek().set(1, start.peek().get(1) + 1);//update the frequency of current skyscraper in stack
> 			} else {
> 				List<Integer> newStart = new ArrayList<>(2);
> 				newStart.add(a[i]);//add height of the skyscraper
> 				newStart.add(1);//add its initial frequency as 1.
> 				start.push(newStart);
> 			}			
> 			
> 		}
> 		System.out.println(c * 2); // multiply by 2 because from right to left  jump is also possible
> 	}
>
> }
>
>
>
> /*
> ======TestCases======
> case =1
> input =6
> 3 2 1 2 3 3
> output =8
>
> case =2
> input =3
> 1 1000 1
> output =0
>
> case =2
> input =10
> 1 1 1 1 1 1 1 1 1 1
> output =90
>
> case =3
> input =20
> 7 7 6 5 4 3 4 5 2 5 6 7 8 3 9 3 3 3 4 9
> output =24
>
> case =4
> input =30
> 103 23 45 67 23 89 103 89 23 45 33 32 32 33 45 23 89 103 103 95 97 87 77 67 57 47 35 32 87 95
> output =22
>
> case =5
> input =50
> 103 23 45 67 23 89 103 89 23 45 33 32 32 7 7 6 5 4 3 4 5 2 5 6 7 8 3 9 3 3 3 4 9 33 45 23 89 103 103 95 97 87 77 67 57 47 35 32 87 95
> output =46
>
> case =6
> input =100
> 2 3 1 3 3 3 3 1 2 3 2 2 3 2 1 2 1 3 1 1 3 3 1 1 3 1 3 2 1 3 2 2 1 1 2 1 2 2 2 1 1 3 1 1 2 2 1 2 2 3 1 2 2 1 3 2 3 1 3 3 1 1 2 2 1 1 2 3 3 1 1 3 3 2 3 2 2 2 3 2 2 2 3 1 3 1 1 2 3 1 2 3 2 2 2 2 1 1 1 3
> output =972
>
> case =7
> input =192
> 1 1 2 3 3 3 2 1 3 3 2 3 3 3 2 2 3 2 2 3 2 3 3 3 1 2 3 3 1 3 1 2 1 3 1 3 2 3 2 1 2 3 1 2 2 1 3 2 2 2 1 3 3 3 1 3 1 2 3 3 3 3 3 2 2 3 2 3 1 2 3 3 3 1 1 1 2 3 3 2 2 1 3 2 3 3 1 1 1 2 2 3 1 1 2 2 2 3 1 1 1 3 2 2 2 2 1 3 1 3 1 1 1 1 1 2 3 1 1 3 1 2 2 2 2 3 3 3 3 2 3 2 1 1 2 1 3 3 1 1 1 2 2 2 1 1 3 1 2 1 2 1 3 2 1 3 1 1 3 2 1 2 1 3 1 3 1 2 1 3 1 3 3 2 1 1 1 3 2 3 2 2 1 3 1 3 2 1 1 1 2 2
> output =4560
>
> case =8
> input =256
> 1 1 2 3 3 3 2 1 3 3 2 3 3 3 2 2 3 2 2 3 2 3 3 3 1 2 3 3 1 3 1 2 1 3 1 3 2 3 2 1 2 3 1 2 2 1 3 2 2 2 1 3 3 3 1 3 1 2 3 3 3 3 3 2 2 3 2 3 1 2 3 3 3 1 1 1 2 3 3 2 2 1 3 2 3 3 1 1 1 2 2 3 1 1 2 2 2 3 1 1 1 3 2 2 2 2 1 3 1 3 1 1 1 1 1 2 3 1 1 3 1 2 2 2 2 3 3 3 3 2 3 2 1 1 2 1 3 3 1 1 1 2 2 2 1 1 3 1 2 1 2 1 3 2 1 3 1 1 3 2 1 2 1 3 1 3 1 2 1 3 1 3 3 2 1 1 1 3 2 3 2 2 1 3 1 3 2 1 1 1 2 2 3 3 3 1 3 1 1 3 2 1 2 1 1 3 2 2 1 2 3 1 2 1 1 3 2 3 1 3 2 3 1 1 2 3 2 2 3 3 3 2 3 1 1 1 2 3 3 2 1 3 3 3 3 2 3 3 1 2 1 2 3 3 2 1
> output =8720
>
> case =9
> input =448
> 2 3 1 3 3 3 3 1 2 3 2 2 3 2 1 2 1 3 1 1 3 3 1 1 3 1 3 2 1 3 2 2 1 1 2 1 2 2 2 1 1 3 1 1 2 2 1 2 2 3 1 2 2 1 3 2 3 1 3 3 1 1 2 2 1 1 2 3 3 1 1 3 3 2 3 2 2 2 3 2 2 2 3 1 3 1 1 2 3 1 2 3 2 2 2 2 1 1 1 3 3 2 1 1 2 3 2 1 1 2 2 2 1 1 3 1 2 1 2 2 3 1 2 2 3 2 1 1 2 2 3 2 3 2 2 1 1 1 2 1 1 1 1 3 1 2 3 2 1 1 3 2 3 3 1 2 2 1 1 3 2 3 3 3 1 2 1 3 1 3 1 2 1 2 3 1 3 2 2 1 2 3 2 2 1 3 2 1 3 3 1 2 3 2 3 3 2 1 2 3 3 1 2 2 2 3 2 2 2 3 3 2 1 1 2 1 2 1 2 2 3 2 2 2 1 1 2 3 3 3 2 1 3 3 2 3 3 3 2 2 3 2 2 3 2 3 3 3 1 2 3 3 1 3 1 2 1 3 1 3 2 3 2 1 2 3 1 2 2 1 3 2 2 2 1 3 3 3 1 3 1 2 3 3 3 3 3 2 2 3 2 3 1 2 3 3 3 1 1 1 2 3 3 2 2 1 3 2 3 3 1 1 1 2 2 3 1 1 2 2 2 3 1 1 1 3 2 2 2 2 1 3 1 3 1 1 1 1 1 2 3 1 1 3 1 2 2 2 2 3 3 3 3 2 3 2 1 1 2 1 3 3 1 1 1 2 2 2 1 1 3 1 2 1 2 1 3 2 1 3 1 1 3 2 1 2 1 3 1 3 1 2 1 3 1 3 3 2 1 1 1 3 2 3 2 2 1 3 1 3 2 1 1 1 2 2 3 3 3 1 3 1 1 3 2 1 2 1 1 3 2 2 1 2 3 1 2 1 1 3 2 3 1 3 2 3 1 1
> output =20120
>
> case =10
> input =500
> 2 3 1 3 3 3 3 1 2 3 2 2 3 2 1 2 1 3 1 1 3 3 1 1 3 1 3 2 1 3 2 2 1 1 2 1 2 2 2 1 1 3 1 1 2 2 1 2 2 3 1 2 2 1 3 2 3 1 3 3 1 1 2 2 1 1 2 3 3 1 1 3 3 2 3 2 2 2 3 2 2 2 3 1 3 1 1 2 3 1 2 3 2 2 2 2 1 1 1 3 3 2 1 1 2 3 2 1 1 2 2 2 1 1 3 1 2 1 2 2 3 1 2 2 3 2 1 1 2 2 3 2 3 2 2 1 1 1 2 1 1 1 1 3 1 2 3 2 1 1 3 2 3 3 1 2 2 1 1 3 2 3 3 3 1 2 1 3 1 3 1 2 1 2 3 1 3 2 2 1 2 3 2 2 1 3 2 1 3 3 1 2 3 2 3 3 2 1 2 3 3 1 2 2 2 3 2 2 2 3 3 2 1 1 2 1 2 1 2 2 3 2 2 2 1 1 2 3 3 3 2 1 3 3 2 3 3 3 2 2 3 2 2 3 2 3 3 3 1 2 3 3 1 3 1 2 1 3 1 3 2 3 2 1 2 3 1 2 2 1 3 2 2 2 1 3 3 3 1 3 1 2 3 3 3 3 3 2 2 3 2 3 1 2 3 3 3 1 1 1 2 3 3 2 2 1 3 2 3 3 1 1 1 2 2 3 1 1 2 2 2 3 1 1 1 3 2 2 2 2 1 3 1 3 1 1 1 1 1 2 3 1 1 3 1 2 2 2 2 3 3 3 3 2 3 2 1 1 2 1 3 3 1 1 1 2 2 2 1 1 3 1 2 1 2 1 3 2 1 3 1 1 3 2 1 2 1 3 1 3 1 2 1 3 1 3 3 2 1 1 1 3 2 3 2 2 1 3 1 3 2 1 1 1 2 2 3 3 3 1 3 1 1 3 2 1 2 1 1 3 2 2 1 2 3 1 2 1 1 3 2 3 1 3 2 3 1 1 2 3 2 2 3 3 3 2 3 1 1 1 2 3 3 2 1 3 3 3 3 2 3 3 1 2 1 2 3 3 2 1 1 1 1 1 2 1 3 2 2 2 3 3 3 1 3 1 3 1 3 3
> output =27150
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2046%20Solutions/JimSky.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 46 Solutions/JimSky.java
