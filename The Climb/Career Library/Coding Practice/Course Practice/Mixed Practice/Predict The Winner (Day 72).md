---
kind: "coding-problem"
title: "Predict The Winner (Day 72)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 72 Solutions/PredictTheWinner.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Predict The Winner (Day 72)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given an array of scores that are non-negative integers. 
Player 1 picks one of the numbers from either end of the array followed by 
the player 2 and then player 1 and so on. Each time a player picks a number,
that number will not be available for the next player. 
This continues until all the scores have been chosen. 
The player with the maximum score wins.

Given an array of scores, predict whether player 1 is the winner. 
You can assume each player plays to maximize his score.


### Sample Input: 

1 5 2


### Sample Output: 

false

Explanation: Initially, player 1 can choose between 1 and 2. 
If he chooses 2 (or 1), then player 2 can choose from 1 (or 2) and 5. 
If player 2 chooses 5, then player 1 will be left with 1 (or 2). 
So, final score of player 1 is 1 + 2 = 3, and player 2 is 5. 
Hence, player 1 will never be the winner and you need to return False.


### Sample Input: 

1 5 233 7

Output: 
true

Explanation: Player 1 first chooses 1. Then player 2 have to choose between 5 and 7. 
No matter which number player 2 choose, player 1 can choose 233.
Finally, player 1 has more score (234) than player 2 (12), so you need to return True representing player1 can win.


========= Testcases Program-2 =========
case =1
input =2 6 3
output ="false"

case =2
input =2 6 50 7
output ="true"

case =3
input =2 6 3 8 7 6 5 9 15
output ="true"

case =4
input =10 5 15 20 18 19 12 13 14
output ="true"

case =5
input =1 20 5 50 10
output ="false"

case =6
input =1 50 10 60 14
output ="false"

case =7
input =4 50 10 60 14 20 5 50 10
output ="false"

case =8
input =10 5 15 20 18 19 12 13 14 20 30 40 50 60
output ="true"

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · PredictTheWinner.java
> ```java
> /*
>  * 
> Given an array of scores that are non-negative integers. 
> Player 1 picks one of the numbers from either end of the array followed by 
> the player 2 and then player 1 and so on. Each time a player picks a number,
> that number will not be available for the next player. 
> This continues until all the scores have been chosen. 
> The player with the maximum score wins.
>
> Given an array of scores, predict whether player 1 is the winner. 
> You can assume each player plays to maximize his score.
>
> Sample Input: 
> 1 5 2
>
> Sample Output: 
> false
>
> Explanation: Initially, player 1 can choose between 1 and 2. 
> If he chooses 2 (or 1), then player 2 can choose from 1 (or 2) and 5. 
> If player 2 chooses 5, then player 1 will be left with 1 (or 2). 
> So, final score of player 1 is 1 + 2 = 3, and player 2 is 5. 
> Hence, player 1 will never be the winner and you need to return False.
>
> Sample Input: 
> 1 5 233 7
>
> Output: 
> true
>
> Explanation: Player 1 first chooses 1. Then player 2 have to choose between 5 and 7. 
> No matter which number player 2 choose, player 1 can choose 233.
> Finally, player 1 has more score (234) than player 2 (12), so you need to return True representing player1 can win.
>
>
> ========= Testcases Program-2 =========
> case =1
> input =2 6 3
> output ="false"
>
> case =2
> input =2 6 50 7
> output ="true"
>
> case =3
> input =2 6 3 8 7 6 5 9 15
> output ="true"
>
> case =4
> input =10 5 15 20 18 19 12 13 14
> output ="true"
>
> case =5
> input =1 20 5 50 10
> output ="false"
>
> case =6
> input =1 50 10 60 14
> output ="false"
>
> case =7
> input =4 50 10 60 14 20 5 50 10
> output ="false"
>
> case =8
> input =10 5 15 20 18 19 12 13 14 20 30 40 50 60
> output ="true"
>
>
>  * 
>  */
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class PredictTheWinner {
>
> 	public static boolean PredictTheWinner(int[] nums) {
> 		int sum = getSum(nums);
> 		int maxScore = getMaxScore(nums, 0, nums.length - 1, sum, new Integer[nums.length][nums.length]);
> 		return maxScore >= sum / 2.0;
> 	}
>
> 	public static int getMaxScore(int[] nums, int s, int e, int maxSum, Integer[][] cache) {
> 		if (s > e) {
> 			return 0;
> 		}
> 		if (s == e) {
> 			return nums[s];
> 		}
> 		if (cache[s][e] != null) {
> 			return cache[s][e];
> 		}
> 		int maxPickS = maxSum - getMaxScore(nums, s + 1, e, maxSum - nums[s], cache);
> 		int maxPickE = maxSum - getMaxScore(nums, s, e - 1, maxSum - nums[e], cache);
> 		cache[s][e] = Math.max(maxPickS, maxPickE);
> 		return cache[s][e];
> 	}
>
> 	public static int getSum(int[] nums) {
> 		int sum = 0;
> 		for (int num : nums) {
> 			sum += num;
> 		}
> 		return sum;
> 	}
>
> 	public static void main(String args[]) throws IOException {
>
> 		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 		String str = br.readLine();
> 		String[] numbers = str.split(" ");
> 		int[] nums = Arrays.asList(numbers).stream().mapToInt(Integer::parseInt).toArray();
> 		System.out.println(PredictTheWinner(nums));
>
> 	}
>
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2072%20Solutions/PredictTheWinner.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 72 Solutions/PredictTheWinner.java
