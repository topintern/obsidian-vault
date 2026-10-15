---
kind: "coding-problem"
title: "Next Permutation (Day 122)"
collection: "Course Practice"
topic: "Math and Counting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 122 solutions/NextPermutation.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Next Permutation (Day 122)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You are given a list of digits( 0 to 9) digits[].
A number is formed using the given order of the list.
for example: given list is [1,3,2], then number is 132.

Find the next biggest number in the lexographic order using the same list of digits,
by using the each digit in the list only once,
and print the digit list of such biggest number.

If such biggest number is not possible, print the smallest lexographic order of the digits.

Input Format:
-------------
Line-1 : An integer N, number of digits.
Line-2 : N space separated integers, list of digits.

Output Format:
--------------
Print an integer list.


Sample Input-1:
---------------
4
1 2 4 3

Sample Output-1:
----------------
[1, 3, 2, 4]


Sample Input-2:
---------------
4
4 3 2 1

Sample Output-2:
----------------
[1, 2, 3, 4]

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · NextPermutation.java
> ```java
> /*
> You are given a list of digits( 0 to 9) digits[].
> A number is formed using the given order of the list.
> for example: given list is [1,3,2], then number is 132.
>
> Find the next biggest number in the lexographic order using the same list of digits,
> by using the each digit in the list only once,
> and print the digit list of such biggest number.
>
> If such biggest number is not possible, print the smallest lexographic order of the digits.
>
> Input Format:
> -------------
> Line-1 : An integer N, number of digits.
> Line-2 : N space separated integers, list of digits.
>
> Output Format:
> --------------
> Print an integer list.
>
>
> Sample Input-1:
> ---------------
> 4
> 1 2 4 3
>
> Sample Output-1:
> ----------------
> [1, 3, 2, 4]
>
>
> Sample Input-2:
> ---------------
> 4
> 4 3 2 1
>
> Sample Output-2:
> ----------------
> [1, 2, 3, 4]
>
>
> */
> import java.util.*;
>
> public class NextPermutation {
>     public void nextPermutation(int[] digits) {
>         int i = digits.length - 2;
>         while (i >= 0 && digits[i + 1] <= digits[i]) {
>             i--;
>         }
>         if (i >= 0) {
>             int j = digits.length - 1;
>             while (j >= 0 && digits[j] <= digits[i]) {
>                 j--;
>             }
>             swap(digits, i, j);
>         }
>         reverse(digits, i + 1);
>     }
>
>     private void reverse(int[] digits, int start) {
>         int i = start, j = digits.length - 1;
>         while (i < j) {
>             swap(digits, i, j);
>             i++;
>             j--;
>         }
>     }
>
>     private void swap(int[] digits, int i, int j) {
>         int temp = digits[i];
>         digits[i] = digits[j];
>         digits[j] = temp;
>     }
> 	
> 	public static void main(String[] args) {
> 		Scanner sc = new Scanner(System.in);
> 		int N=sc.nextInt();
> 		int[] digits=new int[N];
> 		for(int i=0;i<N;i++)
> 			digits[i]=sc.nextInt();
> 		new NextPermutation().nextPermutation(digits);
> 		System.out.println(Arrays.toString(digits));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20122%20solutions/NextPermutation.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 122 solutions/NextPermutation.java
