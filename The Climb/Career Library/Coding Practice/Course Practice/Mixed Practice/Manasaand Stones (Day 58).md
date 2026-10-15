---
kind: "coding-problem"
title: "Manasaand Stones (Day 58)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 58 Solutions/ManasaandStones.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Manasaand Stones (Day 58)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Manasa is out on a hike with friends. She finds a trail of stones with numbers on them. 
She starts following the trail and notices that any two consecutive stones' numbers differ by one of two values. 
Legend has it that there is a treasure trove at the end of the trail. 
If Manasa can guess the value of the last stone, the treasure will be hers.

For example, assume she finds 2 stones and their differences are a=2 or b=3. 
We know she starts with a 0 stone not included in her count.
The permutations of differences for the two stones would be [2,2],[2,3],[3,2] or [3,3]. 
Looking at each scenario, stones might have [2,4], [2,5], [3,5] or [3,6] on them. 
The last stone might have any of 4, 5 or 6 on its face.

Compute all possible numbers that might occur on the last stone given a starting stone with a 0 on it, 
a number of additional stones found, and the possible differences between consecutive stones. 
Order the list ascending.

Input Format:
- The first line contains , the number of non-zero stones found.
- The second line contains , one possible difference
- The third line contains , the other possible difference.

Output Format:
- Space-separated list of numbers which are the possible values of the last stone in increasing order.

Sample Input-1:
3 
1
2
Sample Output-1:
2 3 4 

Sample Input-2:
4
10
100
Sample Output-2:
30 120 210 300 

Explanation-1:
With differences 1 and 2, all possible series for the first test case are given below:
1. 0,1,2
2. 0,1,3
3. 0,2,3
4. 0,2,4
Hence the answer 2 3 4.


Explanation-2:
With differences 10 and 100, all possible series for the second test case are the following:
1. 0, 10, 20, 30
2. 0, 10, 20, 120
3. 0, 10, 110, 120
4. 0, 10, 110, 210
5. 0, 100, 110, 120
6. 0, 100, 110, 210
7. 0, 100, 200, 210
8. 0, 100, 200, 300
Hence the answer 30 120 210 300.


========= Testcases Program-1 =========
case =1
input =3 
1
2
output =2 3 4

case =2
input =4
10
100
output =30 120 210 300

case =3
input =6
4
8
output =20 24 28 32 36 40

case =4
input =11
3
10
output =30 37 44 51 58 65 72 79 86 93 100

case =5
input =11
3
5
output =30 32 34 36 38 40 42 44 46 48 50

case =6
input =6
5
9
output =25 29 33 37 41 45

case =7
input =5
3
23
output =12 32 52 72 92

case =8
input =73
25
25
output =1800

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ManasaandStones.txt
> ```java
> /*
> Manasa is out on a hike with friends. She finds a trail of stones with numbers on them. 
> She starts following the trail and notices that any two consecutive stones' numbers differ by one of two values. 
> Legend has it that there is a treasure trove at the end of the trail. 
> If Manasa can guess the value of the last stone, the treasure will be hers.
>
> For example, assume she finds 2 stones and their differences are a=2 or b=3. 
> We know she starts with a 0 stone not included in her count.
> The permutations of differences for the two stones would be [2,2],[2,3],[3,2] or [3,3]. 
> Looking at each scenario, stones might have [2,4], [2,5], [3,5] or [3,6] on them. 
> The last stone might have any of 4, 5 or 6 on its face.
>
> Compute all possible numbers that might occur on the last stone given a starting stone with a 0 on it, 
> a number of additional stones found, and the possible differences between consecutive stones. 
> Order the list ascending.
>
> Input Format:
> - The first line contains , the number of non-zero stones found.
> - The second line contains , one possible difference
> - The third line contains , the other possible difference.
>
> Output Format:
> - Space-separated list of numbers which are the possible values of the last stone in increasing order.
>
> Sample Input-1:
> 3 
> 1
> 2
> Sample Output-1:
> 2 3 4 
>
> Sample Input-2:
> 4
> 10
> 100
> Sample Output-2:
> 30 120 210 300 
>
> Explanation-1:
> With differences 1 and 2, all possible series for the first test case are given below:
> 1. 0,1,2
> 2. 0,1,3
> 3. 0,2,3
> 4. 0,2,4
> Hence the answer 2 3 4.
>
>
> Explanation-2:
> With differences 10 and 100, all possible series for the second test case are the following:
> 1. 0, 10, 20, 30
> 2. 0, 10, 20, 120
> 3. 0, 10, 110, 120
> 4. 0, 10, 110, 210
> 5. 0, 100, 110, 120
> 6. 0, 100, 110, 210
> 7. 0, 100, 200, 210
> 8. 0, 100, 200, 300
> Hence the answer 30 120 210 300.
>
>
> ========= Testcases Program-1 =========
> case =1
> input =3 
> 1
> 2
> output =2 3 4
>
> case =2
> input =4
> 10
> 100
> output =30 120 210 300
>
> case =3
> input =6
> 4
> 8
> output =20 24 28 32 36 40
>
> case =4
> input =11
> 3
> 10
> output =30 37 44 51 58 65 72 79 86 93 100
>
> case =5
> input =11
> 3
> 5
> output =30 32 34 36 38 40 42 44 46 48 50
>
> case =6
> input =6
> 5
> 9
> output =25 29 33 37 41 45
>
> case =7
> input =5
> 3
> 23
> output =12 32 52 72 92
>
> case =8
> input =73
> 25
> 25
> output =1800
>
>
> */
> import java.util.Scanner;
>
> public class ManasaandStones {
>     public static void main(String[] args) {
>         Scanner stdin = new Scanner(System.in);
> 		int numStones = stdin.nextInt();
> 		int a = stdin.nextInt();
> 		int b = stdin.nextInt();
> 		
> 		if (numStones <= 1) {
> 			System.out.println(0);
> 			System.exit(0);
> 		}
> 		
> 		if (a == b) {
> 			System.out.println(a * (numStones-1));
> 			System.exit(0);
> 		}
> 		
> 		int minValue = Math.min(a,b);
> 		int maxValue = Math.max(a,b);
> 		
> 		System.out.print(minValue * (numStones-1));
> 		for (int j = 1; j < numStones; j++) {
> 			System.out.print(" ");
> 			System.out.print(j * maxValue + (numStones-j-1) * minValue);
> 		}
> 		System.out.println();
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2058%20Solutions/ManasaandStones.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 58 Solutions/ManasaandStones.txt
