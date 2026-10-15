---
kind: "coding-problem"
title: "Salary Blues (Day 65)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 65 Solutions/SalaryBlues.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Salary Blues (Day 65)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Manager of HackerX company is having big trouble. 
Workers are very unhappy with the way salary is given to them. 
They want every worker to have the same salary, otherwise they will go on a strike.

Their current salaries are denoted by a sequence of N integers: A1, A2, A3 ... AN . 
Manager has decided to take action and make their salaries equal. 
He uses the following process until all salaries are equal. This method is called normalization:
a) Select any two different values from A.
b) Replace larger value with the difference of the two. 
	Difference of two positive integers B and C is defined as |B-C|.

He knows that the final value will always be unique.
Now, Q queries are given. In each query you are given an integer K. 
K is the amount to be added to everyone's salary as bonus, before the normalization.

Input Format:
First line contains, N and Q, the number of employees and the number of queries. 
Next line contains N space seperated positive integers denoting the array A. 
Next line contain q space seperated queries. Each query consists of one integer per line denoting K.

Output Format:
For each query, print the normalized salary (which is same for everyone in the end) in one line.


### Constraints

1 ≤ N ≤ 105
1 ≤ Q ≤ 105
1 ≤ A[i] ≤ 1014
0 ≤ K ≤ 109


### Sample Input

4 2
9 12 3 6
0
3

### Sample Output

3
3

### Explanation

for sample input:
If 0 is added to every element of array A, it will remain same.
One way to normalise A is this:
1. Picking 12 and 3 gives: 9 9 3 6
2. Picking 3 and 6 gives: 9 9 3 3
3. Picking 9 and 3 gives: 6 9 3 3
4. Picking 9 and 3 gives: 6 6 3 3
5. Picking 6 and 3 gives: 3 6 3 3
6. Picking 6 and 3 gives: 3 3 3 3

If 3 is added to every element of array A, it will become 12 15 6 9.
One way to normalise A is this:
1. Picking 15 and 6 gives: 12 9 6 9
2. Picking 12 and 9 gives: 3 9 6 9
3. Picking 9 and 6 gives: 3 3 6 9
4. Picking 9 and 6 gives: 3 3 6 3
5. Picking 6 and 3 gives: 3 3 3 3

========= Testcases Program-2 =========
case =1
input =7 4
5 15 25 35 65 45 55
0 4 7 3
output =5 1 2 2

case =2
input =4 2
9 12 3 6
0 3
output =3 3

case =3
input =6 3
8 24 56 78 36 108
7 13 6
output =1 1 2

case =4
input =10 10
7278810 10575180 19484850 21829500 23645160 24017070 27500550 28082670 30558990 34516020
0 5442497 1718799 9455399 1596317 4422429 110609 8881775 9583872 9884582 
output =2310 1 3 1 1 33 1 35 6 2

case =5
input =7 6
27 81 45 81 120 180 135
5 15 20 35 45 60 
output =1 3 1 1 3 3

case =6
input =7 3
270 810 450 360 120 180 150
50 20 60 
output =10 10 30

case =7
input =5 4
200 400 800 600 1000
50 100 150 200
output =50 100 50 200

case =8
input =10 4
450 360 750 90 600 45 1350 150 300 900
10 20 30 45
output =5 5 15 15

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SalaryBlues.java
> ```java
> /*
>
> Manager of HackerX company is having big trouble. 
> Workers are very unhappy with the way salary is given to them. 
> They want every worker to have the same salary, otherwise they will go on a strike.
>
> Their current salaries are denoted by a sequence of N integers: A1, A2, A3 ... AN . 
> Manager has decided to take action and make their salaries equal. 
> He uses the following process until all salaries are equal. This method is called normalization:
> a) Select any two different values from A.
> b) Replace larger value with the difference of the two. 
> 	Difference of two positive integers B and C is defined as |B-C|.
>
> He knows that the final value will always be unique.
> Now, Q queries are given. In each query you are given an integer K. 
> K is the amount to be added to everyone's salary as bonus, before the normalization.
>
> Input Format:
> First line contains, N and Q, the number of employees and the number of queries. 
> Next line contains N space seperated positive integers denoting the array A. 
> Next line contain q space seperated queries. Each query consists of one integer per line denoting K.
>
> Output Format:
> For each query, print the normalized salary (which is same for everyone in the end) in one line.
>
> Constraints
> 1 ≤ N ≤ 105
> 1 ≤ Q ≤ 105
> 1 ≤ A[i] ≤ 1014
> 0 ≤ K ≤ 109
>
> Sample Input:
> 4 2
> 9 12 3 6
> 0
> 3
> Sample Output:
> 3
> 3
> Explanation:
> for sample input:
> If 0 is added to every element of array A, it will remain same.
> One way to normalise A is this:
> 1. Picking 12 and 3 gives: 9 9 3 6
> 2. Picking 3 and 6 gives: 9 9 3 3
> 3. Picking 9 and 3 gives: 6 9 3 3
> 4. Picking 9 and 3 gives: 6 6 3 3
> 5. Picking 6 and 3 gives: 3 6 3 3
> 6. Picking 6 and 3 gives: 3 3 3 3
>
> If 3 is added to every element of array A, it will become 12 15 6 9.
> One way to normalise A is this:
> 1. Picking 15 and 6 gives: 12 9 6 9
> 2. Picking 12 and 9 gives: 3 9 6 9
> 3. Picking 9 and 6 gives: 3 3 6 9
> 4. Picking 9 and 6 gives: 3 3 6 3
> 5. Picking 6 and 3 gives: 3 3 3 3
>
> ========= Testcases Program-2 =========
> case =1
> input =7 4
> 5 15 25 35 65 45 55
> 0 4 7 3
> output =5 1 2 2
>
> case =2
> input =4 2
> 9 12 3 6
> 0 3
> output =3 3
>
> case =3
> input =6 3
> 8 24 56 78 36 108
> 7 13 6
> output =1 1 2
>
> case =4
> input =10 10
> 7278810 10575180 19484850 21829500 23645160 24017070 27500550 28082670 30558990 34516020
> 0 5442497 1718799 9455399 1596317 4422429 110609 8881775 9583872 9884582 
> output =2310 1 3 1 1 33 1 35 6 2
>
> case =5
> input =7 6
> 27 81 45 81 120 180 135
> 5 15 20 35 45 60 
> output =1 3 1 1 3 3
>
> case =6
> input =7 3
> 270 810 450 360 120 180 150
> 50 20 60 
> output =10 10 30
>
> case =7
> input =5 4
> 200 400 800 600 1000
> 50 100 150 200
> output =50 100 50 200
>
> case =8
> input =10 4
> 450 360 750 90 600 45 1350 150 300 900
> 10 20 30 45
> output =5 5 15 15
>
> */
>
> import java.io.IOException;
> import java.util.Scanner;
>
> public class SalaryBlues {
> 	
> 	public static void main(String[] args) throws IOException {
> 		Scanner sc = new Scanner(System.in);
> 		int n = sc.nextInt();
> 		int q = sc.nextInt();
> 		long[] a = new long[n];
> 		int queries[] =new int[q];
> 		long min = Long.MAX_VALUE;
> 		for(int i = 0; i < n; ++i) {
> 			a[i] = sc.nextLong();
> 			min = Math.min(min, a[i]);
> 		}
> 		long g = 0;
> 		for(int i = 0; i < n; ++i) {
> 			if(a[i] > min) {
> 				g = gcd(a[i] - min, g);
> 			}
> 		}
> 		for(int i = 0; i < q; ++i) {
> 			queries[i] = sc.nextInt();
> 		}
> 		for(int i = 0; i < q; ++i) {
> 			System.out.print(gcd(min + queries[i], g) +" ");
> 		}
> 	}
> 	
> 	static long gcd(long a, long b) {
> 		return b == 0 ? a : gcd(b, a % b);
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2065%20Solutions/SalaryBlues.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 65 Solutions/SalaryBlues.java
