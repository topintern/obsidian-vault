---
kind: "coding-problem"
title: "Buy Sell6 (Day 42)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 42 Solutions/Day 42/BuySell6.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Buy Sell6 (Day 42)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Your are given an array of integers prices, 
for which the i-th element is the price of a given stock on day i; 
and a non-negative integer fee representing a transaction fee.

You may complete as many transactions as you like, 
but you need to pay the transaction fee for each transaction. 
You may not buy more than 1 share of a stock at a time 
(ie. you must sell the stock share before you buy again.)

Return the maximum profit you can make.

Example 1:
    Input:  1 3 2 8 4 9
            2
    Output: 8
    Explanation:The maximum profit can be achieved by:
                Buying at prices[0] = 1
                Selling at prices[3] = 8
                Buying at prices[4] = 4
                Selling at prices[5] = 9
                The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.
                

Example 2:
    Input:  1 9 8 3 5 2 6 7 8 13 2 8 1 15                                                                                           
            6                                                                                                                       
    Output: 15
    Explanation:The maximum profit can be achieved by:
                Buying at prices[0] = 1
                Selling at prices[1] = 9
                Buying at prices[5] = 2
                Selling at prices[9] = 13
                Buying at prices[12] = 1
                Selling at prices[13] = 15
                The total profit is ((9 - 1) - 6) + ((13 - 2) - 6) + ((15 - 1) - 6) = 15

---------TestCases-------

case =1
input =91 2 53 65 72 31 108 32 74 1 102 
4
output =274

case =2
input =5 102 4 104 3 103 4 107 1 108 2 110
10
output =555

case =3
input =99 76 53 24 79 34 65 97 46 99 100 86 78
8
output =148

case =4
input =99 87 65 34 25 24 21 19 17 16 12 9 8 5 3 2 1
5
output =0

case =5
input =33 10 15 18 11 22 33 10 15 18 17 4 5 33 10 15 18
9
output =34

case =6
input =10 20 30 3 3 5 0 0 3 1 4 15 20 30 60 867 76 75 67 7 5 6 565 667 6775 76 7 17 76 76 56 456 56 67 23 12 132 5456 767 21 3421 241 23 345 532
13
output =17375

case =7
input =763 876 9817 3452 678345 321 4453 763 26372 16526
371
output =712204

case =8
input =184 234 542 321 642 324 653 43 75 296 742 123 23 451
256
output =890

case =9
input =763 276 32 532 1425 3542 34 2344 873 2 765 123 21
102
output =6277

case =10
input =876 321 3455 3425 45645 6746 3546 7532 56675 626
111
output =98231

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · BuySell6.txt
> ```java
> /*
>
> Your are given an array of integers prices, 
> for which the i-th element is the price of a given stock on day i; 
> and a non-negative integer fee representing a transaction fee.
>
> You may complete as many transactions as you like, 
> but you need to pay the transaction fee for each transaction. 
> You may not buy more than 1 share of a stock at a time 
> (ie. you must sell the stock share before you buy again.)
>
> Return the maximum profit you can make.
>
> Example 1:
>     Input:  1 3 2 8 4 9
>             2
>     Output: 8
>     Explanation:The maximum profit can be achieved by:
>                 Buying at prices[0] = 1
>                 Selling at prices[3] = 8
>                 Buying at prices[4] = 4
>                 Selling at prices[5] = 9
>                 The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.
>                 
>
> Example 2:
>     Input:  1 9 8 3 5 2 6 7 8 13 2 8 1 15                                                                                           
>             6                                                                                                                       
>     Output: 15
>     Explanation:The maximum profit can be achieved by:
>                 Buying at prices[0] = 1
>                 Selling at prices[1] = 9
>                 Buying at prices[5] = 2
>                 Selling at prices[9] = 13
>                 Buying at prices[12] = 1
>                 Selling at prices[13] = 15
>                 The total profit is ((9 - 1) - 6) + ((13 - 2) - 6) + ((15 - 1) - 6) = 15
>
> ---------TestCases-------
>
> case =1
> input =91 2 53 65 72 31 108 32 74 1 102 
> 4
> output =274
>
> case =2
> input =5 102 4 104 3 103 4 107 1 108 2 110
> 10
> output =555
>
> case =3
> input =99 76 53 24 79 34 65 97 46 99 100 86 78
> 8
> output =148
>
> case =4
> input =99 87 65 34 25 24 21 19 17 16 12 9 8 5 3 2 1
> 5
> output =0
>
> case =5
> input =33 10 15 18 11 22 33 10 15 18 17 4 5 33 10 15 18
> 9
> output =34
>
> case =6
> input =10 20 30 3 3 5 0 0 3 1 4 15 20 30 60 867 76 75 67 7 5 6 565 667 6775 76 7 17 76 76 56 456 56 67 23 12 132 5456 767 21 3421 241 23 345 532
> 13
> output =17375
>
> case =7
> input =763 876 9817 3452 678345 321 4453 763 26372 16526
> 371
> output =712204
>
> case =8
> input =184 234 542 321 642 324 653 43 75 296 742 123 23 451
> 256
> output =890
>
> case =9
> input =763 276 32 532 1425 3542 34 2344 873 2 765 123 21
> 102
> output =6277
>
> case =10
> input =876 321 3455 3425 45645 6746 3546 7532 56675 626
> 111
> output =98231
>
> */
> import java.io.*;
> import java.util.*;
> public class BuySell6 {
>
>     public static int maxProfit(int prices[],int fee) {
>         int cash = 0, hold = -prices[0];
>         for (int i = 1; i < prices.length; i++) {
>             cash = Math.max(cash, hold + prices[i] - fee);
>             hold = Math.max(hold, cash - prices[i]);
>         }
>         return cash;
>     }
>     
> 	public static void main(String args[] ) throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		String[] numberline = str.split(" ");
> 		int[] nums = Arrays.asList(numberline).stream().mapToInt(Integer::parseInt).toArray();
>         int fee=Integer.parseInt(br.readLine());
> 		System.out.println(maxProfit(nums,fee));   
> 		
> 		}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2042%20Solutions/Day%2042/BuySell6.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 42 Solutions/Day 42/BuySell6.txt
