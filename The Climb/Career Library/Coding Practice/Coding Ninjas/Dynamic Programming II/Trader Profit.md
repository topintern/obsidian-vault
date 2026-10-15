---
kind: "coding-problem"
title: "Trader Profit"
collection: "Coding Ninjas"
topic: "Dynamic Programming II"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/coding ninjas/Dp-2/trader profit q.txt","CODING RESOURCES/coding ninjas/Dp-2/trader profit s.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "source-folder"
tags: ["career/library","coding/practice"]
---

# Trader Profit

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Coding Ninjas/Coding Ninjas]]

## Problem

Mike is a stock trader and makes a profit by buying and selling stocks. He buys a stock at a lower price and sells it at a higher price to book a profit. He has come to know the stock prices of a particular stock for n upcoming days in future and wants to calculate the maximum profit by doing the right transactions (single transaction = buying + selling). Can you help him maximize his profit?
Note: A transaction starts after the previous transaction has ended. Two transactions can't overlap or run in parallel.
The stock prices are given in the form of an array A for n days.
Given the stock prices and a positive integer k, find and print the maximum profit Mike can make in at most k transactions.

### Input Format

The first line of input contains an integer q denoting the number of queries.

The first line of each test case contains a positive integer k, denoting the number of transactions. 

The second line of each test case contains a positive integer n, denoting the length of the array A.

The third line of each test case contains n space-separated positive integers, denoting the prices of each day in the array A.

### Constraints

1<=q<=100

0<k<10

2<=n<=30

0<=elements of array A<=1000

### Output Format

For each query print the maximum profit earned by Mike on a new line. 

### Sample Input

```text
3
2
6
10 22 5 75 65 80
3
4
20 580 420 900
1
5
100 90 80 50 25
```

### Sample Output

```text
87
1040
0
```

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · trader profit s.txt
> ```cpp
> #include <iostream>
> #include <cstring>
> using namespace std;
>
> int f(int * a, int k, int n, int isongoing, int dp[][10][2]) {
> 	if (n == 0) {
> 		return 0;
> 	}
> 	if (dp[n][k][isongoing] > -1) {
> 		return dp[n][k][isongoing];
> 	}
> 	int ans = f(a + 1, k , n - 1, isongoing, dp);
> 	
> 	if (isongoing) {
> 		int option = f(a + 1, k - 1, n - 1, 0, dp) + a[0];
> 		ans = max(ans, option);
> 	} else {
> 		if (k == 0) {
> 			ans = 0;
> 		} else {
> 			int option = f(a + 1, k, n - 1, 1, dp) - a[0];
> 			ans = max(ans, option);
> 		}
> 	}
> 	dp[n][k][isongoing] = ans;
> 	return ans;
> }
>
> int main() {
> 	int q;
> 	cin >> q;
> 	for (int i = 0; i < q; i++) {
> 		int k, n;
> 		cin >> k >> n;
> 		int a[31];
> 		for (int j = 0; j < n; j++) {
> 			cin >> a[j];
> 		}
> 		int dp[31][10][2];
> 		for (int j = 0; j < 31; j++) {
> 			for (int l = 0; l < 10; l++) {
> 				dp[j][l][0] = -1;
> 				dp[j][l][1] = -1;
> 			}
> 		}
> 		int ans = f(a, k, n, 0, dp);
> 		cout << ans << endl;
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/trader%20profit%20q.txt) · CODING RESOURCES/coding ninjas/Dp-2/trader profit q.txt
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/coding%20ninjas/Dp-2/trader%20profit%20s.txt) · CODING RESOURCES/coding ninjas/Dp-2/trader profit s.txt
