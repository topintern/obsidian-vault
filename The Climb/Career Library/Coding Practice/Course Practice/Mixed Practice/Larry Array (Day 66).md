---
kind: "coding-problem"
title: "Larry Array (Day 66)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 66 Solutions/LarryArray.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Larry Array (Day 66)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Larry has been given a permutation of a sequence of natural numbers 
incrementing from 1 as an array. He must determine whether the array can be sorted 
using the following operation any number of times:
-Choose any 3 consecutive indices and rotate their elements in 
such a way that ABC->BCA->CAB->ABC.

For example, if A={1,6,5,2,4,3}:

A				rotate 
[1,6,5,2,4,3]		[6,5,2]
[1,5,2,6,4,3]		[5,2,6]
[1,2,6,5,4,3]		[5,4,3]
[1,2,6,3,5,4]		[6,3,5]
[1,2,3,5,6,4]		[5,6,4]
[1,2,3,4,5,6]
YES

Input Format:
The first line contains an integer n, the length of A.
The next line contains n space-separated integers .

Constraints:
3<=n<=1000
1<=A[i]<=n
 
Output Format:
print YES if A can be fully sorted. Otherwise, print NO.

Sample Input1:
3
3 1 2
Sample Output1:
YES

Sample Input2:
5
1 2 3 5 4
Sample Output2:
NO

Explanation

Sample #1:
A=[3,1,2]->rotate->[3,1,2]->A=[1,2,3]
A is now sorted, so we print YES.

Sample #2:
No sequence of rotations will result in a sorted . Thus, we print NO.


========= Testcases Program-2 =========
case =1
input =12
9 6 8 12 3 7 1 11 10 2 5 4
output =NO

case =2
input =21
17 21 2 1 16 9 12 11 6 18 20 7 14 8 19 10 3 4 13 5 15
output =YES

case =3
input =15
5 8 13 3 10 4 12 1 2 7 14 6 15 11 9
output =NO

case =4
input =13
8 10 6 11 7 1 9 12 3 5 13 4 2
output =YES

case =5
input =18
7 9 15 8 10 16 6 14 5 13 17 12 3 11 4 1 18 2
output =NO

case =6
input =3
3 1 2
output =YES

case =7
input =4
1 3 4 2
output =YES

case =8
input =5
1 2 3 5 4
output =NO

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · LarryArray.java
> ```java
> /*
> Larry has been given a permutation of a sequence of natural numbers 
> incrementing from 1 as an array. He must determine whether the array can be sorted 
> using the following operation any number of times:
> -Choose any 3 consecutive indices and rotate their elements in 
> such a way that ABC->BCA->CAB->ABC.
>
> For example, if A={1,6,5,2,4,3}:
>
> A				rotate 
> [1,6,5,2,4,3]		[6,5,2]
> [1,5,2,6,4,3]		[5,2,6]
> [1,2,6,5,4,3]		[5,4,3]
> [1,2,6,3,5,4]		[6,3,5]
> [1,2,3,5,6,4]		[5,6,4]
> [1,2,3,4,5,6]
> YES
>
> Input Format:
> The first line contains an integer n, the length of A.
> The next line contains n space-separated integers .
>
> Constraints:
> 3<=n<=1000
> 1<=A[i]<=n
>  
> Output Format:
> print YES if A can be fully sorted. Otherwise, print NO.
>
> Sample Input1:
> 3
> 3 1 2
> Sample Output1:
> YES
>
> Sample Input2:
> 5
> 1 2 3 5 4
> Sample Output2:
> NO
>
> Explanation
>
> Sample #1:
> A=[3,1,2]->rotate->[3,1,2]->A=[1,2,3]
> A is now sorted, so we print YES.
>
> Sample #2:
> No sequence of rotations will result in a sorted . Thus, we print NO.
>
>
> ========= Testcases Program-2 =========
> case =1
> input =12
> 9 6 8 12 3 7 1 11 10 2 5 4
> output =NO
>
> case =2
> input =21
> 17 21 2 1 16 9 12 11 6 18 20 7 14 8 19 10 3 4 13 5 15
> output =YES
>
> case =3
> input =15
> 5 8 13 3 10 4 12 1 2 7 14 6 15 11 9
> output =NO
>
> case =4
> input =13
> 8 10 6 11 7 1 9 12 3 5 13 4 2
> output =YES
>
> case =5
> input =18
> 7 9 15 8 10 16 6 14 5 13 17 12 3 11 4 1 18 2
> output =NO
>
> case =6
> input =3
> 3 1 2
> output =YES
>
> case =7
> input =4
> 1 3 4 2
> output =YES
>
> case =8
> input =5
> 1 2 3 5 4
> output =NO
>
>
> */
>
> import java.io.*;
> import java.util.*;
>
> public class LarryArray {
>
>     public static void main(String[] args) {
>         Scanner scanner = new Scanner(System.in);
>             int[] array = new int[scanner.nextInt()];
>             for (int j = 0; j < array.length; j++) {
>                 array[j] = scanner.nextInt();
>             }
>             if (canSort(array, array.length - 1)) {
>                 System.out.println("YES");
>             } else {
>                 System.out.println("NO");
>             }
>     }
>     
>     public static boolean canSort(int[] array, int end) {
>         if (end == 1) {
>             return (array[end] > array[0]);
>         }
>         int i = 0;
>         while (array[i] < end + 1 && i <= end) {
>             i++;
>         }
>         if (i == 0) {
>             rotate(array, i);
>             i++;
>         }
>         while (i != end) {
>             rotate(array, i - 1);
>             i++;
>         }
>         return canSort(array, end - 1);
>     }
>     
>     public static void rotate(int[] array, int index) {
>         int temp = array[index + 2];
>         array[index + 2] = array[index + 1];
>         array[index + 1] = array[index];
>         array[index] = temp;
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2066%20Solutions/LarryArray.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 66 Solutions/LarryArray.java
