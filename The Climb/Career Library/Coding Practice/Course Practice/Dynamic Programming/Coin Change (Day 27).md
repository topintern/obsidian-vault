---
kind: "coding-problem"
title: "Coin Change (Day 27)"
collection: "Course Practice"
topic: "Dynamic Programming"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 27 Solutions/CoinChange.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Coin Change (Day 27)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

Example 1:

Input: coins = [1, 2, 5], amount = 11
Output: 3 
Explanation: 11 = 5 + 5 + 1
Example 2:

Input: coins = [2], amount = 3
Output: -1
Note:
You may assume that you have an infinite number of each kind of coin.


========TestCases===========
case =1
input =1 2 5
11
output =3

case =2
input =2 4
7
output =-1

case =3
input =1 2 5 7
22
output =4

case =4
input =1 2 5 10
108
output =13

case =5
input =10 12 13
70
output =6

case =6
input =1 2 5 10
216
output =23

case =7
input =10 12 13 40
50
output =2

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · CoinChange.java
> ```java
> /*
>  * 
>  You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.
>
> Example 1:
>
> Input: coins = [1, 2, 5], amount = 11
> Output: 3 
> Explanation: 11 = 5 + 5 + 1
> Example 2:
>
> Input: coins = [2], amount = 3
> Output: -1
> Note:
> You may assume that you have an infinite number of each kind of coin.
>
>
> ========TestCases===========
> case =1
> input =1 2 5
> 11
> output =3
>
> case =2
> input =2 4
> 7
> output =-1
>
> case =3
> input =1 2 5 7
> 22
> output =4
>
> case =4
> input =1 2 5 10
> 108
> output =13
>
> case =5
> input =10 12 13
> 70
> output =6
>
> case =6
> input =1 2 5 10
> 216
> output =23
>
> case =7
> input =10 12 13 40
> 50
> output =2
>
>
>  */
>
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class CoinChange {
>
> 	public static int coinChange(int[] coins, int amount) {
> 	    int max = amount + 1;
> 	    int[] dp = new int[amount + 1];
> 	    Arrays.fill(dp, max);
> 	    dp[0] = 0;
> 	    for (int i = 1; i <= amount; i++) {
> 	      for (int j = 0; j < coins.length; j++) {
> 	        if (coins[j] <= i) {
> 	          dp[i] = Math.min(dp[i], dp[i - coins[j]] + 1);
> 	        }
> 	      }
> 	    }
> 	    return dp[amount] > amount ? -1 : dp[amount];
> 	  }
> 	
> 	public static void main(String args[] ) throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		
> 		String[] numline = str.split(" ");
> 		int[] coins = Arrays.asList(numline).stream().mapToInt(Integer::parseInt).toArray();
> 		int amount=Integer.parseInt( br.readLine());
> 		System.out.println(coinChange(coins,amount));   
> 		
> 		}
> 	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2027%20Solutions/CoinChange.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 27 Solutions/CoinChange.java
