---
kind: "coding-problem"
title: "Buy Sell1 (Day 42)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 42 Solutions/Day 42/BuySell1.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Buy Sell1 (Day 42)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

In a market, there is a list of price of 'N' days of an item.
i-th day price is listed as price[i]. 


A Street Seller wants to get the maximum profit by buying and selling the item.
He has permission to complete at most one transaction ,(ie, buy one item and sell one item) 
with the following rules:

Note that he cannot sell an item before he buys one.

Example 1:
    Input: 7 1 5 3 6 4
    Output: 5
    Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
                 Not 7-1 = 6, as selling price needs to be larger than buying price.

Example 2:
    Input: 7 6 4 3 1
    Output: 0
    Explanation: In this case, no transaction is done, i.e. max profit = 0

--------TestCases----------

case =1
input =1 9 8 3 5 2 6 7 8 13 2 8 1 15
output =14

case =2
input =7 6 5 4 3 2 18 9 10 11 12 13
output =16

case =3
input =91 2 53 65 72 31 108 32 74 1 102 
output =106

case =4
input =5 102 4 104 3 103 4 107 1 108 2 110
output =109

case =5
input =99 76 53 24 79 34 65 97 46 99 100 86 78
output =76

case =6
input =99 87 65 34 25 24 21 19 17 16 12 9 8 5 3 2 1
output =0

case =7
input =7 1 5 3 6 4
output =5

case =8
input =7 6 4 3 1 2
output =1

case =9
input =154 458 765 123 245 187 567 198 357 234 615 
output =611

case =10
input =32 76 98 24 91 28 90 30 84
output =67

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · BuySell1.txt
> ```java
> /*
>
> In a market, there is a list of price of 'N' days of an item.
> i-th day price is listed as price[i]. 
>
>
> A Street Seller wants to get the maximum profit by buying and selling the item.
> He has permission to complete at most one transaction ,(ie, buy one item and sell one item) 
> with the following rules:
>
> Note that he cannot sell an item before he buys one.
>
> Example 1:
>     Input: 7 1 5 3 6 4
>     Output: 5
>     Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
>                  Not 7-1 = 6, as selling price needs to be larger than buying price.
>
> Example 2:
>     Input: 7 6 4 3 1
>     Output: 0
>     Explanation: In this case, no transaction is done, i.e. max profit = 0
>
> --------TestCases----------
>
> case =1
> input =1 9 8 3 5 2 6 7 8 13 2 8 1 15
> output =14
>
> case =2
> input =7 6 5 4 3 2 18 9 10 11 12 13
> output =16
>
> case =3
> input =91 2 53 65 72 31 108 32 74 1 102 
> output =106
>
> case =4
> input =5 102 4 104 3 103 4 107 1 108 2 110
> output =109
>
> case =5
> input =99 76 53 24 79 34 65 97 46 99 100 86 78
> output =76
>
> case =6
> input =99 87 65 34 25 24 21 19 17 16 12 9 8 5 3 2 1
> output =0
>
> case =7
> input =7 1 5 3 6 4
> output =5
>
> case =8
> input =7 6 4 3 1 2
> output =1
>
> case =9
> input =154 458 765 123 245 187 567 198 357 234 615 
> output =611
>
> case =10
> input =32 76 98 24 91 28 90 30 84
> output =67
>
> */
> import java.io.*;
> import java.util.*;
> public class BestTimeToSell1 {
>
>     
>     public static int maxProfit(int prices[]) {
>         int T_i10 = 0, T_i11 = Integer.MIN_VALUE;
>         
>         for (int price : prices) {
>             T_i10 = Math.max(T_i10, T_i11 + price);
>             T_i11 = Math.max(T_i11, -price);
>         }
>     
>         return T_i10;
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

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2042%20Solutions/Day%2042/BuySell1.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 42 Solutions/Day 42/BuySell1.txt
