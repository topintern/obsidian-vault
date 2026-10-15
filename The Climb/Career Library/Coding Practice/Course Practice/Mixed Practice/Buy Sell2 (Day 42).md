---
kind: "coding-problem"
title: "Buy Sell2 (Day 42)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 42 Solutions/Day 42/BuySell2.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Buy Sell2 (Day 42)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

In a market, there is a list of price of 'N' days of an item.
i-th day price is listed as price[i]. 


A Street Seller wants to get the maximum profit by buying and selling the item.
He can do as many transactions as he want ,(i.e., buy one item and sell one item multiple times) 
with the following rules:

Note that he cannot buy and sell an item on same day(He must sell the item before he buy again).

Example 1:
    Input: 7 1 5 3 6 4
    Output: 7
    Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
                 Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.

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

-------TestCases--------

case =1
input =1 2 3 4 5 6 7 8 9 10
output =9

case =2
input =7 4 2 5 3 8 1 9 10 6
output =17

case =3
input =331 224 325 346 231 453 672 321 764
output =1006

case =4
input =1 2 3 4 5 2 4 5 6 3 4 5 6 4 5 6 5 6
output =14

case =5
input =7 21 34 56 3 76 87 34 76 123
output =222

case =6
input =98 65 74 32 75 93 54 34 21 76
output =125

case =7
input =763 876 9817 3452 678345 321 4453 763 26372 16526
output =713688

case =8
input =184 234 542 321 642 324 653 43 75 296 742 123 23 451
output =2135

case =9
input =763 276 32 532 1425 3542 34 2344 873 2 765 123 21
output =6583

case =10
input =876 321 3455 3425 45645 6746 3546 7532 56675 626
output =98483

case =11
input =1 20 2 27 3 32 34 97 48 121
output =211

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · BuySell2.txt
> ```java
> /*
> In a market, there is a list of price of 'N' days of an item.
> i-th day price is listed as price[i]. 
>
>
> A Street Seller wants to get the maximum profit by buying and selling the item.
> He can do as many transactions as he want ,(i.e., buy one item and sell one item multiple times) 
> with the following rules:
>
> Note that he cannot buy and sell an item on same day(He must sell the item before he buy again).
>
> Example 1:
>     Input: 7 1 5 3 6 4
>     Output: 7
>     Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
>                  Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
>
> Example 2:
>     Input: 1 2 3 4 5 
>     Output: 4
>     Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
>                  Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
>                  engaging multiple transactions at the same time. You must sell before buying again.
>
> Example 3:
>     Input: 7 6 4 3 1
>     Output: 0
>     Explanation: In this case, no transaction is done, i.e. max profit = 0.
>
> -------TestCases--------
>
> case =1
> input =1 2 3 4 5 6 7 8 9 10
> output =9
>
> case =2
> input =7 4 2 5 3 8 1 9 10 6
> output =17
>
> case =3
> input =331 224 325 346 231 453 672 321 764
> output =1006
>
> case =4
> input =1 2 3 4 5 2 4 5 6 3 4 5 6 4 5 6 5 6
> output =14
>
> case =5
> input =7 21 34 56 3 76 87 34 76 123
> output =222
>
> case =6
> input =98 65 74 32 75 93 54 34 21 76
> output =125
>
> case =7
> input =763 876 9817 3452 678345 321 4453 763 26372 16526
> output =713688
>
> case =8
> input =184 234 542 321 642 324 653 43 75 296 742 123 23 451
> output =2135
>
> case =9
> input =763 276 32 532 1425 3542 34 2344 873 2 765 123 21
> output =6583
>
> case =10
> input =876 321 3455 3425 45645 6746 3546 7532 56675 626
> output =98483
>
> case =11
> input =1 20 2 27 3 32 34 97 48 121
> output =211
>
>
> */
> import java.io.*;
> import java.util.*;
>
> public class BestTimeToSell2 {
>     public static  int maxProfit(int[] prices) {
>         int T_ik0 = 0, T_ik1 = Integer.MIN_VALUE;
>     
>         for (int price : prices) {
>             int T_ik0_old = T_ik0;
>             T_ik0 = Math.max(T_ik0, T_ik1 + price);
>             T_ik1 = Math.max(T_ik1, T_ik0_old - price);
>         }
>     
>         return T_ik0;
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

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2042%20Solutions/Day%2042/BuySell2.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 42 Solutions/Day 42/BuySell2.txt
