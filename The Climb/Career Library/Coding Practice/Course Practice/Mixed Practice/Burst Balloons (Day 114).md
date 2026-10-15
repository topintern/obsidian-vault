---
kind: "coding-problem"
title: "Burst Balloons (Day 114)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 114 Solutions/BurstBalloons.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Burst Balloons (Day 114)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You are playing a shooting game.
There are N bottles hanging to a rod, i-th bottle numbered bottle[i].

If you shoot i-th bottle, you will get bottle[i-1]*bottle[i]*bottle[i+1] points.
The more points you score, the more rewards you can win.

Your task is to score the maximum points by shooting all the ballons wisely.

Note: After you shoot bottle at i-th index, bottles at i-1 and i+1 positions
become adjacent. if there is no existing 'i-1' or 'i+1' positions for selected bottle.
you can assume that bottle[i-1] = bottle[i+1] = 1.

Input Format:
-------------
N space separated integers bottles[].

Output Format:
--------------
Print an integer, maximum points you can get.



### Sample Input

---------------
3 1 5 8


### Sample Output

----------------
167


### Explanation

------------
Given bottles = [3, 1, 5, 8] 
position 	points
--------------------
1				3*1*5
5				3*5*8
3				1*3*8
8				1*8*1
--------------------
Total = 167



### Sample Input

---------------
2 1 3 5 4


### Sample Output

----------------
102


### Explanation

------------
Given bottles = [3, 1, 5, 8] 
position 	points
--------------------
5				3*5*4
1				2*1*3
3				2*3*4
2				1*2*4
4				1*4*1
--------------------
Total = 102

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · BurstBalloons.java
> ```java
> /*
> You are playing a shooting game.
> There are N bottles hanging to a rod, i-th bottle numbered bottle[i].
>
> If you shoot i-th bottle, you will get bottle[i-1]*bottle[i]*bottle[i+1] points.
> The more points you score, the more rewards you can win.
>
> Your task is to score the maximum points by shooting all the ballons wisely.
>
> Note: After you shoot bottle at i-th index, bottles at i-1 and i+1 positions
> become adjacent. if there is no existing 'i-1' or 'i+1' positions for selected bottle.
> you can assume that bottle[i-1] = bottle[i+1] = 1.
>
> Input Format:
> -------------
> N space separated integers bottles[].
>
> Output Format:
> --------------
> Print an integer, maximum points you can get.
>
>
> Sample Input:
> ---------------
> 3 1 5 8
>
> Sample Output:
> ----------------
> 167
>
> Explanation:
> ------------
> Given bottles = [3, 1, 5, 8] 
> position 	points
> --------------------
> 1				3*1*5
> 5				3*5*8
> 3				1*3*8
> 8				1*8*1
> --------------------
> Total = 167
>
>
> Sample Input:
> ---------------
> 2 1 3 5 4
>
> Sample Output:
> ----------------
> 102
>
> Explanation:
> ------------
> Given bottles = [3, 1, 5, 8] 
> position 	points
> --------------------
> 5				3*5*4
> 1				2*1*3
> 3				2*3*4
> 2				1*2*4
> 4				1*4*1
> --------------------
> Total = 102
>
> */
>
> import java.util.*;
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
>
> class BurstBalloons {
> 	//DP SOLUTION
>     public int maxCoins(int[] iNums) {
> 		int[] nums = new int[iNums.length + 2];
> 		int n = 1;
> 		for (int x : iNums) if (x > 0) nums[n++] = x;
> 		nums[0] = nums[n++] = 1;
>
>
> 		int[][] dp = new int[n][n];
> 		for (int k = 2; k < n; ++k)
> 			for (int left = 0; left < n - k; ++left) {
> 				int right = left + k;
> 				for (int i = left + 1; i < right; ++i)
> 					dp[left][right] = Math.max(dp[left][right], 
> 					nums[left] * nums[i] * nums[right] + dp[left][i] + dp[i][right]);
> 			}
>
> 		return dp[0][n - 1];
> 	}
>
> 	public static void main(String args[] ) throws IOException {
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		String[] numberline = str.split(" ");
> 		int[] nums = Arrays.asList(numberline).stream().mapToInt(Integer::parseInt).toArray();
> 		System.out.print( new BurstBalloons().maxCoins(nums));   
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20114%20Solutions/BurstBalloons.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 114 Solutions/BurstBalloons.java
