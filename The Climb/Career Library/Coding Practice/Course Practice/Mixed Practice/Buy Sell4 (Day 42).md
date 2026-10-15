---
kind: "coding-problem"
title: "Buy Sell4 (Day 42)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 42 Solutions/Day 42/BuySell4.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Buy Sell4 (Day 42)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

In a market, there is a list of price of 'N' days of an item.
i-th day price is listed as price[i]. 


A Street Seller wants to get the maximum profit by buying and selling the items.
He can do at most 'T' transactions  ,(i.e., buy one item and sell one item for 'T' times) 

Note that he cannot buy and sell an item on same day(He must sell the item before he buy again).

Example 1:
    Input:  2 4 1
            2
    Output: 2
    Explanation: Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4-2 = 2.

Example 2:
    Input:  3 2 6 5 0 3
            2
    Output: 7
    Explanation: Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6-2 = 4.
                 Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.

------TestCases------------

case =1
input =3 3 5 0 0 3 1 4
2
output =6

case =2
input =1 2 3 4 5
2
output =4

case =3
input =7 6 4 3 1
2
output =0

case =4
input =10 20 30 3 3 5 0 0 3 1 4 15 20 30 60 867 76 75 67 7 5 6 565 667 6775 76 7 17 76 76 56 456 56 67 23 12 132 5456 767 21 3421 241 23 345 532
14
output =17494

case =5
input =11 22 33 10 15 18 17 4 5
10
output =31

case =6
input =1 2 3 4 5 6 7 6 4 3 1 10 15 18 7 9 10
6
output =26

case =7
input =33 10 15 18 11 22 33 10 15 18 17 4 5 33 10 15 18
4
output =68

case =8
input =10 20 1 4 15 20 30 60
4
output =69

case =9
input =33 10 15 18 11 22 33 10 15 18 17 4 5 33 10 15 18
3
output =60

case =10
input =22 33 1 2 3 6 7 6 4 32 25 18 7 9 10 10 15 18
7
output =56

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · BuySell4.txt
> ```java
> /*
>
> In a market, there is a list of price of 'N' days of an item.
> i-th day price is listed as price[i]. 
>
>
> A Street Seller wants to get the maximum profit by buying and selling the items.
> He can do at most 'T' transactions  ,(i.e., buy one item and sell one item for 'T' times) 
>
> Note that he cannot buy and sell an item on same day(He must sell the item before he buy again).
>
> Example 1:
>     Input:  2 4 1
>             2
>     Output: 2
>     Explanation: Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4-2 = 2.
>
> Example 2:
>     Input:  3 2 6 5 0 3
>             2
>     Output: 7
>     Explanation: Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6-2 = 4.
>                  Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
>
> ------TestCases------------
>
> case =1
> input =3 3 5 0 0 3 1 4
> 2
> output =6
>
> case =2
> input =1 2 3 4 5
> 2
> output =4
>
> case =3
> input =7 6 4 3 1
> 2
> output =0
>
> case =4
> input =10 20 30 3 3 5 0 0 3 1 4 15 20 30 60 867 76 75 67 7 5 6 565 667 6775 76 7 17 76 76 56 456 56 67 23 12 132 5456 767 21 3421 241 23 345 532
> 14
> output =17494
>
> case =5
> input =11 22 33 10 15 18 17 4 5
> 10
> output =31
>
> case =6
> input =1 2 3 4 5 6 7 6 4 3 1 10 15 18 7 9 10
> 6
> output =26
>
> case =7
> input =33 10 15 18 11 22 33 10 15 18 17 4 5 33 10 15 18
> 4
> output =68
>
> case =8
> input =10 20 1 4 15 20 30 60
> 4
> output =69
>
> case =9
> input =33 10 15 18 11 22 33 10 15 18 17 4 5 33 10 15 18
> 3
> output =60
>
> case =10
> input =22 33 1 2 3 6 7 6 4 32 25 18 7 9 10 10 15 18
> 7
> output =56
>
> */
>
> import java.io.*;
> import java.util.*;
> public class BuySell4 {
>
>     
>     public static int maxProfit(int T, int prices[]) {
>         if (T >= prices.length >>> 1) {
>             int T_ik0 = 0, T_ik1 = Integer.MIN_VALUE;
>         
>             for (int price : prices) {
>                 int T_ik0_old = T_ik0;
>                 T_ik0 = Math.max(T_ik0, T_ik1 + price);
>                 T_ik1 = Math.max(T_ik1, T_ik0_old - price);
>             }
>         
>             return T_ik0;
>         }
>             
>         int[] T_ik0 = new int[T + 1];
>         int[] T_ik1 = new int[T + 1];
>         Arrays.fill(T_ik1, Integer.MIN_VALUE);
>             
>         for (int price : prices) {
>             for (int j = T; j > 0; j--) {
>                 T_ik0[j] = Math.max(T_ik0[j], T_ik1[j] + price);
>                 T_ik1[j] = Math.max(T_ik1[j], T_ik0[j - 1] - price);
>             }
>         }
>             
>         return T_ik0[T];
>     }
>     
> 	public static void main(String args[] ) throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		String[] numberline = str.split(" ");
> 		int[] nums = Arrays.asList(numberline).stream().mapToInt(Integer::parseInt).toArray();
>         int T=Integer.parseInt(br.readLine());
> 		System.out.println(maxProfit(T,nums));   
> 		
> 		}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2042%20Solutions/Day%2042/BuySell4.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 42 Solutions/Day 42/BuySell4.txt
