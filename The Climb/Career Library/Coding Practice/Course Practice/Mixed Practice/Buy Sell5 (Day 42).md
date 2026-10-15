---
kind: "coding-problem"
title: "Buy Sell5 (Day 42)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 42 Solutions/Day 42/BuySell5.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Buy Sell5 (Day 42)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

you have an array for which the ith element is the price of a given stock on day i.

write a program to find the maximum profit. 
You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:

You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
After you sell your stock, you cannot buy stock on next day. (ie, notrade 1 day)
Example:

Input: 1 2 3 2 5
Output: 4 
Explanation: transactions = [buy, sell, notrade, buy, sell]

-----TestCases-----------

case=1
input=10 20 30 15 50
output=45

case=2
input=30 40 50 60 1 20 30 75
output=94

case=3
input=30 40 50 60 1 20 30 75 2 20 100
output=174

case=4
input=10 10 10 10 10 10
output=0

case=5
input=100 90 80 70 60 66 77 99 88 110
output=50

case=6
input=100 90 80 70 60 66 0 99 88 110
output=110

case =7
input =763 876 9817 3452 678345 321 4453 763 26372 16526
output =703191

case =8
input =184 234 542 321 642 324 653 43 75 296 742 123 23 451
output =1782

case =9
input =763 276 32 532 1425 3542 34 2344 873 2 765 123 21
output =4466

case =10
input =876 321 3455 3425 45645 6746 3546 7532 56675 626
output =98453

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · BuySell5.txt
> ```java
> /*
>  * 
> you have an array for which the ith element is the price of a given stock on day i.
>
> write a program to find the maximum profit. 
> You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:
>
> You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
> After you sell your stock, you cannot buy stock on next day. (ie, notrade 1 day)
> Example:
>
> Input: 1 2 3 2 5
> Output: 4 
> Explanation: transactions = [buy, sell, notrade, buy, sell]
>
> -----TestCases-----------
>
> case=1
> input=10 20 30 15 50
> output=45
>
> case=2
> input=30 40 50 60 1 20 30 75
> output=94
>
> case=3
> input=30 40 50 60 1 20 30 75 2 20 100
> output=174
>
> case=4
> input=10 10 10 10 10 10
> output=0
>
> case=5
> input=100 90 80 70 60 66 77 99 88 110
> output=50
>
> case=6
> input=100 90 80 70 60 66 0 99 88 110
> output=110
>
> case =7
> input =763 876 9817 3452 678345 321 4453 763 26372 16526
> output =703191
>
> case =8
> input =184 234 542 321 642 324 653 43 75 296 742 123 23 451
> output =1782
>
> case =9
> input =763 276 32 532 1425 3542 34 2344 873 2 765 123 21
> output =4466
>
> case =10
> input =876 321 3455 3425 45645 6746 3546 7532 56675 626
> output =98453
>
>  */
>
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class BestTimeToBuy {
>
> 	
> 	public static int maxProfit(int[] prices) {
> 	    int sell = 0, prev_sell = 0, buy = Integer.MIN_VALUE, prev_buy;
> 	    for (int price : prices) {
> 	        prev_buy = buy;
> 	        buy = Math.max(prev_sell - price, prev_buy);
> 	        prev_sell = sell;
> 	        sell = Math.max(prev_buy + price, prev_sell);
> 	    }
> 	    return sell;
> 	}
> 	
> 	
> 	public static void main(String args[] ) throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		
> 		String[] stockpriceline = str.split(" ");
> 		int[] prices = Arrays.asList(stockpriceline).stream().mapToInt(Integer::parseInt).toArray();
> 		
> 		System.out.println(maxProfit(prices));   
> 		
> 		}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2042%20Solutions/Day%2042/BuySell5.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 42 Solutions/Day 42/BuySell5.txt
