---
kind: "coding-problem"
title: "stockmax (Day 86)"
collection: "Course Practice"
topic: "Dynamic Programming"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/_Day 86 Solutions/stockmax-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/_Day 86 Solutions/StockMaximize.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# stockmax (Day 86)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

*******Testcases*********
case =1
input =3
5 3 2
output =0

case =2
input =3
1 2 100
output =197

case =3
input =4
1 3 1 2
output =3

case =4
input =4
1 2 1 3
output =5

case =5
input =5
5 4 3 4 5
output =4

case =6
input =4
1 2 3 4
output =6

case =7
input =7
2 9 4 1 5 17 19
output =76

case =8
input =8
23 6 8 76 3 67 2 5
output =258

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · StockMaximize.java
> ```java
> /*
> ********Testcases*********
> case =1
> input =3
> 5 3 2
> output =0
>
> case =2
> input =3
> 1 2 100
> output =197
>
> case =3
> input =4
> 1 3 1 2
> output =3
>
> case =4
> input =4
> 1 2 1 3
> output =5
>
> case =5
> input =5
> 5 4 3 4 5
> output =4
>
> case =6
> input =4
> 1 2 3 4
> output =6
>
> case =7
> input =7
> 2 9 4 1 5 17 19
> output =76
>
> case =8
> input =8
> 23 6 8 76 3 67 2 5
> output =258
>
>
> */
>
> import java.util.*;
> public class StockMaximize {
>
>     public static void main(String[] args) {
>         Scanner scanner = new Scanner(System.in);
>         int size = scanner.nextInt();
>
>         for (int i = 0; i < size; i++) {
>             int numOfDays = scanner.nextInt();
>             int[] prices = new int[numOfDays];
>             for (int j = 0; j < numOfDays; j++) {
>                 prices[j] = scanner.nextInt();
>             }
>             System.out.println(getMaxProfit(prices));
>         }
>     }
>
>     public static long getMaxProfit(int[] prices) {
>         long profit = 0L;
>         int maxSoFar = 0;
>         for (int i = prices.length - 1; i > -1 ; i--) {
>             if (prices[i] >= maxSoFar) {
>                 maxSoFar = prices[i];
>             }
>             profit += maxSoFar - prices[i];
>         }
>         return profit;
>     }
>     
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/stockmax-English-17c55a33.pdf|stockmax-English-17c55a33.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/stockmax-English-17c55a33.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/_Day%2086%20Solutions/stockmax-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/_Day 86 Solutions/stockmax-English.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/_Day%2086%20Solutions/StockMaximize.java) · CODING RESOURCES/ELITE FS COMPLETE/_Day 86 Solutions/StockMaximize.java
