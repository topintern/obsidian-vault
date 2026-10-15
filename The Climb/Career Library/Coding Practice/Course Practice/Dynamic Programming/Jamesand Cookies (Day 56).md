---
kind: "coding-problem"
title: "Jamesand Cookies (Day 56)"
collection: "Course Practice"
topic: "Dynamic Programming"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 56 Solutions/JamesandCookies.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Jamesand Cookies (Day 56)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

James loves cookies. He wants the sweetness of all his cookies to be greater than value . 
To do this, James repeatedly mixes two cookies with the least sweetness. 
He creates a special combined cookie with:
sweetness =(1 * Least sweet cookie + 2 * 2nd least sweet cookie).

He repeats this procedure until all the cookies in his collection have a sweetness >=K.
You are given James's cookies. Print the number of operations required to give the cookies a sweetness >= K. 
Print -1 if this isn't possible.

Input Format:
  - The first line consists of integers N, the number of cookies and K, the minimum required sweetness, 
	separated by a space.
  - The next line contains N integers describing the array A where 
	Ai is the sweetness of the ith cookie in James's collection.

Output Format:
Output the number of operations that are needed to increase the cookie's sweetness >= K .
Output -1, if this isn't possible.

Sample Input
		6 7
		1 2 3 9 10 12
Sample Output
		2

Explanation
	Combine the first two cookies to create a cookie with sweetness  = 1*1 + 2*2 =5 
	After this operation, the cookies are 3 5 9 10 12.
	Then, combine the cookies with sweetness 3 and sweetness 5, to create a cookie with 
	resulting sweetness  = 1*3 + 2*5 =13
	Now, the cookies are 9 10 12 13.
	All the cookies have a sweetness >=7 .

	Thus, 2 operations are required to increase the sweetness.

========= Testcases Program-1 =========
case =1
input =3 10
1 1 1
output =-1

case =2
input =6 7
1 2 3 9 10 12
output =2

case =3
input =4 10
52 96 13 37
output =0

case =4
input =8 90
13 47 74 12 89 74 18 38
output =5

case =5
input =3 9
1 62 14
output =1

case =6
input =25 3581
6214 8543 9266 1150 7498 7209 9398 1529 1032 7384 6784 34 1449 7598 8795 756 7803 4112 298 4967 1261 1724 4272 1100 9373
output =7

case =7
input =3 200
5 6 7
output =-1

case =8
input =24 47245
3554 2227 8866 9890 212 8669 2423 7651 3878 3379 1419 6134 5767 859 2848 9309 1449 8408 8041 3367 6676 6382 4136 4871
output =20

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · JamesandCookies.txt
> ```java
> /*
> James loves cookies. He wants the sweetness of all his cookies to be greater than value . 
> To do this, James repeatedly mixes two cookies with the least sweetness. 
> He creates a special combined cookie with:
> sweetness =(1 * Least sweet cookie + 2 * 2nd least sweet cookie).
>
> He repeats this procedure until all the cookies in his collection have a sweetness >=K.
> You are given James's cookies. Print the number of operations required to give the cookies a sweetness >= K. 
> Print -1 if this isn't possible.
>
> Input Format:
>   - The first line consists of integers N, the number of cookies and K, the minimum required sweetness, 
> 	separated by a space.
>   - The next line contains N integers describing the array A where 
> 	Ai is the sweetness of the ith cookie in James's collection.
>
> Output Format:
> Output the number of operations that are needed to increase the cookie's sweetness >= K .
> Output -1, if this isn't possible.
>
> Sample Input
> 		6 7
> 		1 2 3 9 10 12
> Sample Output
> 		2
>
> Explanation
> 	Combine the first two cookies to create a cookie with sweetness  = 1*1 + 2*2 =5 
> 	After this operation, the cookies are 3 5 9 10 12.
> 	Then, combine the cookies with sweetness 3 and sweetness 5, to create a cookie with 
> 	resulting sweetness  = 1*3 + 2*5 =13
> 	Now, the cookies are 9 10 12 13.
> 	All the cookies have a sweetness >=7 .
>
> 	Thus, 2 operations are required to increase the sweetness.
>
> ========= Testcases Program-1 =========
> case =1
> input =3 10
> 1 1 1
> output =-1
>
> case =2
> input =6 7
> 1 2 3 9 10 12
> output =2
>
> case =3
> input =4 10
> 52 96 13 37
> output =0
>
> case =4
> input =8 90
> 13 47 74 12 89 74 18 38
> output =5
>
> case =5
> input =3 9
> 1 62 14
> output =1
>
> case =6
> input =25 3581
> 6214 8543 9266 1150 7498 7209 9398 1529 1032 7384 6784 34 1449 7598 8795 756 7803 4112 298 4967 1261 1724 4272 1100 9373
> output =7
>
> case =7
> input =3 200
> 5 6 7
> output =-1
>
> case =8
> input =24 47245
> 3554 2227 8866 9890 212 8669 2423 7651 3878 3379 1419 6134 5767 859 2848 9309 1449 8408 8041 3367 6676 6382 4136 4871
> output =20
>
> */
>
> import java.io.*;
> import java.util.*;
>
> public class JamesandCookies {
>
>     public static void main(String[] args) throws IOException {
>         Scanner in = new Scanner(System.in);
>         String[] line1 = in.nextLine().trim().split(" ");
>         String[] line2 = in.nextLine().trim().split(" ");
>         int N = Integer.parseInt(line1[0]);
>         int K = Integer.parseInt(line1[1]);
>
>         PriorityQueue<Integer> pq = new PriorityQueue<>();
>         for (int i = 0; i < N; i++) {
>             pq.add(Integer.parseInt(line2[i]));
>         }
>         
>         int min = pq.peek();
>         int it = 0;
>         while (min < K && pq.size() > 1) {
>             it++;
>             int a = pq.poll();
>             int b = pq.poll();
>             pq.add(a + 2 * b);
>             min = pq.peek();
>         }
>         
>         if (min >= K)
>             System.out.println(it);
>         else
>             System.out.println(-1);
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2056%20Solutions/JamesandCookies.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 56 Solutions/JamesandCookies.txt
