---
kind: "coding-problem"
title: "XPattern (Day 43)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 43 Solutions/XPattern.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# XPattern (Day 43)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a string of odd length, print the string X format.


### Sample Input: 

abcde


### Sample Output

a   e
 b d
  c
 b d
a   e 
NOTE: If it is not possible to print X pattern, print -1. 
			Read the string using nextLine or readLine method.


----------TestCases-----------
case =1
input =am fg
output =a   g
 m f
  
 m f
a   g

case =2
input =abc
output =a c
 b
a c

case =3
input =abcdefg
output =a     g
 b   f
  c e
   d
  c e
 b   f
a     g

case =4
input =xlwrt
output =x   t
 l r
  w
 l r
x   t

case =5
input =1234567
output =1     7
 2   6
  3 5
   4
  3 5
 2   6
1     7

case =6
input =a c e
output =a   e
 
  c
  
a   e

case =7
input =xlmc 2rt4
output =x       4
 l     t
  m   r
   c 2
    
   c 2
  m   r
 l     t
x       4

case =8
input =abcde
output =a   e
 b d
  c
 b d
a   e

case =9
input =abc cba
output =a     a
 b   b
  c c
   
  c c
 b   b
a     a

case =10
input =a
output =-1

case =11
input =a 123  bre
output =-1

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · XPattern.txt
> ```java
> /*
>  * 
> Given a string of odd length, print the string X format.
>
> Sample Input: 
> abcde
>
> Sample Output:
> a   e
>  b d
>   c
>  b d
> a   e 
> NOTE: If it is not possible to print X pattern, print -1. 
> 			Read the string using nextLine or readLine method.
>
>
> ----------TestCases-----------
> case =1
> input =am fg
> output =a   g
>  m f
>   
>  m f
> a   g
>
> case =2
> input =abc
> output =a c
>  b
> a c
>
> case =3
> input =abcdefg
> output =a     g
>  b   f
>   c e
>    d
>   c e
>  b   f
> a     g
>
> case =4
> input =xlwrt
> output =x   t
>  l r
>   w
>  l r
> x   t
>
> case =5
> input =1234567
> output =1     7
>  2   6
>   3 5
>    4
>   3 5
>  2   6
> 1     7
>
> case =6
> input =a c e
> output =a   e
>  
>   c
>   
> a   e
>
> case =7
> input =xlmc 2rt4
> output =x       4
>  l     t
>   m   r
>    c 2
>     
>    c 2
>   m   r
>  l     t
> x       4
>
> case =8
> input =abcde
> output =a   e
>  b d
>   c
>  b d
> a   e
>
> case =9
> input =abc cba
> output =a     a
>  b   b
>   c c
>    
>   c c
>  b   b
> a     a
>
> case =10
> input =a
> output =-1
>
> case =11
> input =a 123  bre
> output =-1
>
>  * 
>  */
>
> import java.util.Scanner;
> public class XPattern {
>
> 	// Function to print given
> 	// string in cross pattern
> 	static void pattern(String str, int len) {
> 			if(str.length()==1 ||  str.length()%2==0)
> 			{
> 					System.out.print("-1");
> 					return;
> 			}
> 		// i and j are the indexes
> 		// of characters to be
> 		// displayed in the ith
> 		// iteration i = 0 intially
> 		// and go upto length of string
> 		// j = length of string initially
> 		// in each iteration of i,
> 		// we increment i and decrement j,
> 		// we print character only
> 		// of k==i or k==j
> 		for (int i = 0; i < len; i++) {
> 			int j = len - 1 - i;
> 			for (int k = 0; k < len; k++) {
> 				if (k == i || k == j)
> 					System.out.print(str.charAt(k));
> 				else
> 					System.out.print(" ");
> 			}
> 			System.out.println("");
> 		}
> 	}
> 	// main function
> 		public static void main(String[] args) {
>
> 			Scanner sc = new Scanner(System.in);
>
> 			
> 			String str = sc.nextLine();
> 			int n = str.length();
>
> 			pattern(str, n);
>
> 		}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2043%20Solutions/XPattern.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 43 Solutions/XPattern.txt
