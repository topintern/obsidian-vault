---
kind: "coding-problem"
title: "alice-and-bobs-silly-game (Day 86)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/_Day 86 Solutions/alice-and-bobs-silly-game-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/_Day 86 Solutions/AliceBob.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# alice-and-bobs-silly-game (Day 86)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

*******Testcases*********
case =1
input =2
output ="RAM"

case =2
input =7
output ="NAG"

case =3
input =20
output ="NAG"

case =4
input =100
output ="RAM"

case =5
input =300
output ="NAG"

case =6
input =10000
output ="RAM"

case =7
input =25689
output =RAM

case =8
input =35000
output ="NAG"

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · AliceBob.java
> ```java
> /*
> ********Testcases*********
> case =1
> input =2
> output ="RAM"
>
> case =2
> input =7
> output ="NAG"
>
> case =3
> input =20
> output ="NAG"
>
> case =4
> input =100
> output ="RAM"
>
> case =5
> input =300
> output ="NAG"
>
> case =6
> input =10000
> output ="RAM"
>
> case =7
> input =25689
> output =RAM
>
> case =8
> input =35000
> output ="NAG"
>
>
> */
>
> import java.io.*;
> import java.util.*;
> import java.text.*;
> import java.math.*;
> import java.util.regex.*;
>
> public class AliceBob {
>     public static boolean[] bS(int n){
>          
>         boolean[] isPrime = new boolean[n+1];
>         for (int i = 2; i <= n; i++) {
>             isPrime[i] = true;
>         }
>         for (int factor = 2; factor*factor <= n; factor++) {
>             if (isPrime[factor]) {
>                 for (int j = factor; factor*j <= n; j++) {
>                     isPrime[factor*j] = false;
>                 }
>             }
>         }
>         return isPrime;
>     }
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         int g = in.nextInt();
>         boolean[] s  = bS(100000);
>         for(int a0 = 0; a0 < g; a0++){
>             int n = in.nextInt();
>             int count =0;
>             for(int i = n;i>0;i--){
>                 if(s[i])count++;
>             }
>             if(count%2==0){
>                 System.out.println("NAG");
>             }
>             else{
>                 System.out.println("RAM");                
>             }
>         }
>     }
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/alice-and-bobs-silly-game-English-68031066.pdf|alice-and-bobs-silly-game-English-68031066.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/alice-and-bobs-silly-game-English-68031066.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/_Day%2086%20Solutions/alice-and-bobs-silly-game-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/_Day 86 Solutions/alice-and-bobs-silly-game-English.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/_Day%2086%20Solutions/AliceBob.java) · CODING RESOURCES/ELITE FS COMPLETE/_Day 86 Solutions/AliceBob.java
