---
kind: "coding-problem"
title: "fibonacci-modified (Day 86)"
collection: "Course Practice"
topic: "Dynamic Programming"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/_Day 86 Solutions/fibonacci-modified-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/_Day 86 Solutions/FibonacciNew.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# fibonacci-modified (Day 86)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

*******Testcases*********
case =1
input =0 1 5
output =5

case =2
input =2 3 7
output =56055246933386836

case =3
input =3 4 5
output =133244

case =4
input =1 2 8
output =84266613096281243382112

case =5
input =2 3 6
output =236759893

case =6
input =1 2 10
output =50422242317787290639189291009890702507917377925161079229314384058371278254659634544914784801

case =7
input =2 4 6
output =11578190732

case =8
input =1 3 7
output =12715553707944315

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · FibonacciNew.java
> ```java
> /*
> ********Testcases*********
> case =1
> input =0 1 5
> output =5
>
> case =2
> input =2 3 7
> output =56055246933386836
>
> case =3
> input =3 4 5
> output =133244
>
> case =4
> input =1 2 8
> output =84266613096281243382112
>
> case =5
> input =2 3 6
> output =236759893
>
> case =6
> input =1 2 10
> output =50422242317787290639189291009890702507917377925161079229314384058371278254659634544914784801
>
> case =7
> input =2 4 6
> output =11578190732
>
> case =8
> input =1 3 7
> output =12715553707944315
>
> */
>
> import java.util.*;
> import java.math.*;
>
> public class FibonacciNew {
>
>     public static void main(String[] args) {
>         Scanner scan = new Scanner(System.in);
>         BigInteger first = new BigInteger(scan.next());
>         BigInteger second = new BigInteger(scan.next());
>         int n = scan.nextInt();
>         BigInteger third = new BigInteger("0");
>         
>         for(int i = 2; i < n; i++) {
>             third = first.add(second.multiply(second));
>             first = second;
>             second = third;
>         }
>         scan.close();
>         System.out.println(third);
>     }
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/fibonacci-modified-English-52b54c73.pdf|fibonacci-modified-English-52b54c73.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/fibonacci-modified-English-52b54c73.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/_Day%2086%20Solutions/fibonacci-modified-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/_Day 86 Solutions/fibonacci-modified-English.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/_Day%2086%20Solutions/FibonacciNew.java) · CODING RESOURCES/ELITE FS COMPLETE/_Day 86 Solutions/FibonacciNew.java
