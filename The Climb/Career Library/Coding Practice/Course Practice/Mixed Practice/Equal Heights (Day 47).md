---
kind: "coding-problem"
title: "Equal Heights (Day 47)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 47 Solutions/EqualHeights.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Equal Heights (Day 47)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You have three SETs of Rectangular Boxes where each Rectangular Box has the same length and width, 
but they may vary in height. In each SET, Rectangular Box is placed one on another
You can change the height of a SET by removing its topmost Rectangular Box any number of times.

Find the maximum possible height of the SETs such that all of the SETs are exactly the same height. 
This means you must remove zero or more Rectangular Boxes from 
the top of zero or more of the three SETs until they're all the same height, then print the height. 
The removals must be performed in such a way as to maximize the height.

Note: An empty SET is still a SET.

Input Format :
The first line contains three space-separated integers n1, n2, and n3, describing the respective number of Rectangular Boxs in SETs 1, 2 and 3. 
The subsequent lines describe the respective heights of each Rectangular Box in a SET from top to bottom:
The second line contains n1  space-separated integers describing the Rectangular Box heights in SET . 
The third line contains  n2 space-separated integers describing the Rectangular Box heights in SET . 
The fourth line contains  n3 space-separated integers describing the Rectangular Box heights in SET . 

Note: In each line The first element is the top of the SET.

Sample Input
------------
5 3 4
3 2 1 1 1
4 3 2
1 1 4 1

Sample Output
-------------
5

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · EqualHeights.java
> ```java
> /*
>  * 
> You have three SETs of Rectangular Boxes where each Rectangular Box has the same length and width, 
> but they may vary in height. In each SET, Rectangular Box is placed one on another
> You can change the height of a SET by removing its topmost Rectangular Box any number of times.
>
> Find the maximum possible height of the SETs such that all of the SETs are exactly the same height. 
> This means you must remove zero or more Rectangular Boxes from 
> the top of zero or more of the three SETs until they're all the same height, then print the height. 
> The removals must be performed in such a way as to maximize the height.
>
> Note: An empty SET is still a SET.
>
> Input Format :
> The first line contains three space-separated integers n1, n2, and n3, describing the respective number of Rectangular Boxs in SETs 1, 2 and 3. 
> The subsequent lines describe the respective heights of each Rectangular Box in a SET from top to bottom:
> The second line contains n1  space-separated integers describing the Rectangular Box heights in SET . 
> The third line contains  n2 space-separated integers describing the Rectangular Box heights in SET . 
> The fourth line contains  n3 space-separated integers describing the Rectangular Box heights in SET . 
>
> Note: In each line The first element is the top of the SET.
>
> Sample Input
> ------------
> 5 3 4
> 3 2 1 1 1
> 4 3 2
> 1 1 4 1
>
> Sample Output
> -------------
> 5
>  	
>  */
> import java.util.Scanner;
>
> public class EqualHeights {
>
> 	public static void main(String args[]) {
> 		Scanner sc = new Scanner(System.in);
> 		int n1, n2, n3, h, sum1 = 0, sum2 = 0, sum3 = 0, d1, d2, d3;
>
> 		n1 = sc.nextInt();
> 		n2 = sc.nextInt();
> 		n3 = sc.nextInt();
> 		int[] arr1 = new int[n1];
> 		int[] arr2 = new int[n2];
> 		int[] arr3 = new int[n3];
>
> 		for (int i = 0; i < n1; i++) {
> 			arr1[i] = sc.nextInt();
> 			sum1 += arr1[i];
> 		}
> 		d1 = 0;
>
> 		for (int i = 0; i < n2; i++) {
> 			arr2[i] = sc.nextInt();
> 			sum2 += arr2[i];
> 		}
> 		d2 = 0;
>
> 		for (int i = 0; i < n3; i++) {
> 			arr3[i] = sc.nextInt();
> 			sum3 += arr3[i];
> 		}
> 		d3 = 0;
>
> 		while (true) {
> 			if (d1 == n1 || d2 == n2 || d3 == n3) {
> 				h = 0;
> 				break;
> 			}
>
> 			if (sum1 == sum2 && sum2 == sum3) {
> 				h = sum1;
> 				break;
> 			}
>
> 			// If height op pile one is highest
> 			if (sum1 >= sum2 && sum1 >= sum3) {
> 				sum1 -= arr1[d1];
> 				d1++;
> 			}
> 			// If height op pile two is highest
> 			else if (sum2 >= sum1 && sum2 >= sum3) {
> 				sum2 -= arr2[d2];
> 				d2++;
> 			}
> 			// If height op pile three is highest
> 			else if (sum3 >= sum2 && sum3 >= sum1) {
> 				sum3 -= arr3[d3];
> 				d3++;
> 			}
> 		}
> 		System.out.println(h);
> 	}
> }
>
>
> /*
>
> =====TestCases======
> case =1
> input =8 5 9
> 6 9 4 7 10 3 4 15
> 4 3 5 13 19
> 7 4 7 3 4 5 5 5 3
> output =32
>
> case =2
> input =9 4 5
> 3 2 1 1 1 2 3 3 3
> 6 4 4 3
> 2 3 4 5 6
> output =11
>
> case =3
> input =7 7 7
> 8 7 4 3 6 4 2
> 6 7 5 2 7 3 2
> 8 6 7 1 5 4 2
> output =19
>
> case =4
> input =4 5 6
> 2 3 4 5
> 1 2 3 4 5
> 1 1 2 3 4 5
> output =14
>
> case =5
> input =21 30 42
> 11 47 38 45 13 42 20 17 44 22 8 11 12 24 14 44 43 32 44 9 19
> 50 27 21 10 41 33 21 23 17 45 42 36 23 37 49 50 30 21 44 8 11 12 24 14 44 43 32 44 9 19
> 14 8 7 18 40 13 20 29 11 40 35 24 26 49 6 6 42 26 50 48 48 46 33 27 25 33 17 29 41 35 15 8 11 12 24 14 44 43 32 44 9 19
> output =260
>
> case =6
> input =1 1 1
> 1
> 1
> 1
> output =1
>
> case =7
> input =8 9 6
> 8 4 3 6 3 4 2 4
> 9 7 6 4 2 3 2 4 2
> 4 2 3 2 4 2
> output =13
>
> case =8
> input =6 4 5
> 4 5 3 1 3 2
> 5 4 3 2
> 7 6 4 2 3
> output =9
>
> case =9
> input =7 8 6
> 7 6 3 8 9 2 4
> 8 4 5 3 2 4 1 1
> 6 4 3 5 8 3
> output =0
>
> case =10
> input =5 3 4
> 3 2 1 1 1
> 4 3 2
> 1 1 4 1
> output =5
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2047%20Solutions/EqualHeights.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 47 Solutions/EqualHeights.java
