---
kind: "coding-problem"
title: "Zigzag String Concat (Day 39)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 39 Solutions/ZigzagStringConcat.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Zigzag String Concat (Day 39)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a string and number of rows 'n'. 
Print the string formed by concatenating n rows when input string is 
written in row-wise Zig-Zag fashion.


### Sample Input

ABCDEFGHIJKLM
3

### Sample Output: 

AEIMBDFHJLCGK

Explanation: Let us write input string in Zig-Zag fashion
             in 3 rows.
A       E       I       M
  B   D   F   H   J   L
    C       G       K
Now concatenate the two rows and ignore spaces 
in every row. We get "AEIMBDFHJLCGK"

======testCases=========
case=1
input=NGITKMIT
1
output=NGITKMIT

case=2
input=FINISHING SCHOOL
3
output=FSGHIIHN COLNISO

case=3
input=SONETFINISHING
8
output=SOGNNEITHFSIIN

case=4
input=SONETFINISHING
13
output=SONETFINISHIGN

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ZigzagStringConcat.txt
> ```java
> /*
>  * 
>
> Given a string and number of rows 'n'. 
> Print the string formed by concatenating n rows when input string is 
> written in row-wise Zig-Zag fashion.
>
> Sample Input:
> ABCDEFGHIJKLM
> 3
> Sample Output: 
> AEIMBDFHJLCGK
>
> Explanation: Let us write input string in Zig-Zag fashion
>              in 3 rows.
> A       E       I       M
>   B   D   F   H   J   L
>     C       G       K
> Now concatenate the two rows and ignore spaces 
> in every row. We get "AEIMBDFHJLCGK"
>
> ======testCases=========
> case=1
> input=NGITKMIT
> 1
> output=NGITKMIT
>
> case=2
> input=FINISHING SCHOOL
> 3
> output=FSGHIIHN COLNISO
>
> case=3
> input=SONETFINISHING
> 8
> output=SOGNNEITHFSIIN
>
> case=4
> input=SONETFINISHING
> 13
> output=SONETFINISHIGN
>  * 
>  */
> package Elite2020;
> import java.util.Arrays;
> import java.util.Scanner;
>
> class ZigzagStringConcat {
>
> 	// Prints concatenation
> 	// of all rows of str's
> 	// Zig-Zag fasion
> 	static void printZigZagConcat(String str, int n) {
>
> 		// Corner Case (Only one row)
> 		if (n == 1) {
> 			System.out.print(str);
> 			return;
> 		}
> 		char[] str1 = str.toCharArray();
>
> 		// Find length of string
> 		int len = str.length();
>
> 		// Create an array of
> 		// strings for all n rows
> 		String[] arr = new String[n];
> 		Arrays.fill(arr, "");
>
> 		// Initialize index for
> 		// array of strings arr[]
> 		int row = 0;
> 		boolean down = true; // True if we are moving
> 		// down in rows, else false
>
> 		// Travers through given string
> 		for (int i = 0; i < len; ++i) {
> 			// append current character
> 			// to current row
> 			
> 			arr[row] += (str1[i]);
>
> 			// If last row is reached,
> 			// change direction to 'up'
> 			if (row == n - 1) {
> 				down = false;
> 			}
>
> 			// If 1st row is reached,
> 			// change direction to 'down'
> 			else if (row == 0) {
> 				down = true;
> 			}
>
> 			// If direction is down,
> 			// increment, else decrement
> 			if (down) {
> 				row++;
> 			} else {
> 				row--;
> 			}
> 		}
>
> 		// Print concatenation of all rows
> 		for (int i = 0; i < n; ++i) {
> 			System.out.print(arr[i]);
> 		}
> 	}
>
> 	public static void main(String[] args) {
> 		Scanner sc = new Scanner(System.in);
>
> 		String str = sc.nextLine();
> 		int n = sc.nextInt();
> 		printZigZagConcat(str, n);
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2039%20Solutions/ZigzagStringConcat.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 39 Solutions/ZigzagStringConcat.txt
