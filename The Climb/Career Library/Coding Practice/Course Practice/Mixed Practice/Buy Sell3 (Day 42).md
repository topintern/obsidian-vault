---
kind: "coding-problem"
title: "Buy Sell3 (Day 42)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 42 Solutions/Day 42/BuySell3.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Buy Sell3 (Day 42)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

Note: You may not engage in multiple transactions at the same time
(i.e., you must sell the stock before you buy again).

Example 1:

Input: 3 3 5 0 0 3 1 4
Output: 6
Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
             Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
Example 2:

Input: 1 2 3 4 5
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.
Example 3:

Input: 7 6 4 3 1
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.

-----------TestCases-----------
case =1
input =3 3 5 0 0 3 1 4
output =6

case =2
input =1 2 3 4 5
output =4

case =3
input =7 6 4 3 1
output =0


case =4
input =10 20 30 3 3 5 0 0 3 1 4 15 20 30 60
output =80

case =5
input =11 22 33 10 15 18 17 4 5
output =30

case =6
input =1 2 3 4 5 6 7 6 4 3 1 10 15 18 7 9 10
output =23


case =7
input =7 6 4 3 1 7 6 4 3 1
output =6


case =8
input =10 20 1 4 15 20 30 60
output =69

case =9
input =33 10 15 18 11 22 33 10 15 18 17 4 5 33 10 15 18
output =52

case =10
input =22 33 1 2 3 6 7 6 4 32 25 18 7 9 10 10 15 18
output =42

case =11
input =1 20 2 27 3 32 34 97 48 121
output =169

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · BuySell3.txt
> ```java
> /*
>
> Say you have an array for which the ith element is the price of a given stock on day i.
>
> Design an algorithm to find the maximum profit. You may complete at most two transactions.
>
> Note: You may not engage in multiple transactions at the same time
> (i.e., you must sell the stock before you buy again).
>
> Example 1:
>
> Input: 3 3 5 0 0 3 1 4
> Output: 6
> Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
>              Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
> Example 2:
>
> Input: 1 2 3 4 5
> Output: 4
> Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
>              Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
>              engaging multiple transactions at the same time. You must sell before buying again.
> Example 3:
>
> Input: 7 6 4 3 1
> Output: 0
> Explanation: In this case, no transaction is done, i.e. max profit = 0.
>
> -----------TestCases-----------
> case =1
> input =3 3 5 0 0 3 1 4
> output =6
>
> case =2
> input =1 2 3 4 5
> output =4
>
> case =3
> input =7 6 4 3 1
> output =0
>
>
> case =4
> input =10 20 30 3 3 5 0 0 3 1 4 15 20 30 60
> output =80
>
> case =5
> input =11 22 33 10 15 18 17 4 5
> output =30
>
> case =6
> input =1 2 3 4 5 6 7 6 4 3 1 10 15 18 7 9 10
> output =23
>
>
> case =7
> input =7 6 4 3 1 7 6 4 3 1
> output =6
>
>
> case =8
> input =10 20 1 4 15 20 30 60
> output =69
>
> case =9
> input =33 10 15 18 11 22 33 10 15 18 17 4 5 33 10 15 18
> output =52
>
> case =10
> input =22 33 1 2 3 6 7 6 4 32 25 18 7 9 10 10 15 18
> output =42
>
> case =11
> input =1 20 2 27 3 32 34 97 48 121
> output =169
>
> */
>
> import java.io.*;
> import java.util.*;
>
> public class BuySell3 {
>
>        public static int maxProfit(int[] prices) {
>         int T_i10 = 0, T_i11 = Integer.MIN_VALUE, T_i20 = 0, T_i21 = Integer.MIN_VALUE;
>             
>         for (int price : prices) {
>             T_i20 = Math.max(T_i20, T_i21 + price);
>             T_i21 = Math.max(T_i21, T_i10 - price);
>             T_i10 = Math.max(T_i10, T_i11 + price);
>             T_i11 = Math.max(T_i11, -price);
>         }
>             
>         return T_i20;
>     }
>     
> 	public static void main(String args[] ) throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		String[] numberline = str.split(" ");
> 		int[] nums = Arrays.asList(numberline).stream().mapToInt(Integer::parseInt).toArray();
>
> 		System.out.println(maxProfit(nums));   
> 		
> 		}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2042%20Solutions/Day%2042/BuySell3.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 42 Solutions/Day 42/BuySell3.txt
