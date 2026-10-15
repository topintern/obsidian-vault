---
kind: "coding-problem"
title: "counter-game (Day 86)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/_Day 86 Solutions/counter-game-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/_Day 86 Solutions/CounterGame.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# counter-game (Day 86)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

*******Testcases*********
case =1
input =9876786
output ="Riya"

case =2
input =1234567
output ="Riya"

case =3
input =10235
output ="Riya"

case =4
input =87
output ="Riya"

case =5
input =356
output ="Laya"

case =6
input =123456
output ="Laya"

case =7
input =512
output ="Laya"

case =8
input =132
output ="Laya"

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · CounterGame.java
> ```java
> /*
> ********Testcases*********
> case =1
> input =9876786
> output ="Riya"
>
> case =2
> input =1234567
> output ="Riya"
>
> case =3
> input =10235
> output ="Riya"
>
> case =4
> input =87
> output ="Riya"
>
> case =5
> input =356
> output ="Laya"
>
> case =6
> input =123456
> output ="Laya"
>
> case =7
> input =512
> output ="Laya"
>
> case =8
> input =132
> output ="Laya"
>
>
> */
>
> import java.math.BigInteger;
> import java.util.Scanner;
>
> public class CounterGame {
>
> 	public static void main(String[] args) {
> 		Scanner sc = new Scanner(System.in);
> 		int t = sc.nextInt();
> 		for(int i = 0; i < t; ++i) {
> 			BigInteger n = new BigInteger(sc.next());
> 			int cnt = 0;
> 			while (n.compareTo(BigInteger.ONE) == 1) {
> 				BigInteger x = BigInteger.ONE;
> 				while (x.shiftLeft(1).compareTo(n) < 0) {
> 					x = x.shiftLeft(1);
> 				}
> 				++cnt;
> 				n = n.subtract(x);
> 			}
> 			System.out.println(cnt % 2 == 0 ? "Riya" : "Laya");
> 		}
> 		System.out.flush();
>
> 	}
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/counter-game-English-ac87b046.pdf|counter-game-English-ac87b046.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/counter-game-English-ac87b046.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/_Day%2086%20Solutions/counter-game-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/_Day 86 Solutions/counter-game-English.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/_Day%2086%20Solutions/CounterGame.java) · CODING RESOURCES/ELITE FS COMPLETE/_Day 86 Solutions/CounterGame.java
