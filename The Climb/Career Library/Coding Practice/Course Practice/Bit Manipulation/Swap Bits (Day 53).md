---
kind: "coding-problem"
title: "Swap Bits (Day 53)"
collection: "Course Practice"
topic: "Bit Manipulation"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 53 Solutions/SwapBits.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Swap Bits (Day 53)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Write a program to swap odd and even bits in an integer with as few instructions as
possible (e.g., bit 0 and bit 1 are swapped, bit 2 and bit 3 are swapped, etc)


### Sample Input: 

23
Output: 
43


### Explanation

Binary Representation of 23 is  = 0 0 0 1 0 1 1 1
Binary Representation of 43 is  = 0 0 1 0 1 0 1 1
Before swap (0 0) (0 1) (0 1) (1 1)
After swap  (0 0) (1 0) (1 0) (1 1) is equal to 43.


### Sample Input: 

256
Output: 
512


### Explanation

Binary Representation of 256 is  = 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0
Binary Representation of 512 is  = 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 0


========= TestCases Prog-1 =========
case =1
input =256
output =512

case =2
input =23
output =43

case =3
input =32
output =16

case =4
input =143
output =79

case =5
input =225
output =210

case =6
input =10232
output =7156

case =7
input =5434567
output =10607819

case =8
input =9872
output =6496

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SwapBits.java
> ```java
> /*
>  * 
> Write a program to swap odd and even bits in an integer with as few instructions as
> possible (e.g., bit 0 and bit 1 are swapped, bit 2 and bit 3 are swapped, etc)
>
> Sample Input: 
> 23
> Output: 
> 43
>
> Explanation:
> Binary Representation of 23 is  = 0 0 0 1 0 1 1 1
> Binary Representation of 43 is  = 0 0 1 0 1 0 1 1
> Before swap (0 0) (0 1) (0 1) (1 1)
> After swap  (0 0) (1 0) (1 0) (1 1) is equal to 43.
>
> Sample Input: 
> 256
> Output: 
> 512
>
> Explanation:
> Binary Representation of 256 is  = 0 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0
> Binary Representation of 512 is  = 0 0 0 0 0 0 1 0 0 0 0 0 0 0 0 0
>
>
> ========= TestCases Prog-1 =========
> case =1
> input =256
> output =512
>
> case =2
> input =23
> output =43
>
> case =3
> input =32
> output =16
>
> case =4
> input =143
> output =79
>
> case =5
> input =225
> output =210
>
> case =6
> input =10232
> output =7156
>
> case =7
> input =5434567
> output =10607819
>
> case =8
> input =9872
> output =6496
>
>  * 
>  */
>
> import java.util.Scanner;
>
> public class SwapBits {
>
>     // Function to swap even  and odd bits 
>     static int swapBits(int x) 
>     { 
>         // Get all even bits of x 
>         int even_bits = x & 0xAAAAAAAA;  
>       
>         // Get all odd bits of x 
>         int odd_bits = x & 0x55555555;  
>       
>         // Right shift even bits 
>         even_bits >>= 1;  
>           
>         // Left shift even bits 
>         odd_bits <<= 1;  
>           
>         // Combine even and odd bits 
>         return (even_bits | odd_bits);  
>     } 
>       
>    
>     public static void main(String[] args) 
>     { 
>     	Scanner sc = new Scanner(System.in);
>         int x = sc.nextInt();
>         System.out.println(swapBits(x)); 
>     } 
>
>     
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2053%20Solutions/SwapBits.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 53 Solutions/SwapBits.java
