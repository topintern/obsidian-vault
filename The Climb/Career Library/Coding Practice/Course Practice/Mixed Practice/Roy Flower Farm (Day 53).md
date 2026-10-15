---
kind: "coding-problem"
title: "Roy Flower Farm (Day 53)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 53 Solutions/RoyFlowerFarm.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Roy Flower Farm (Day 53)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Roy is the owner of a flower plant farm and sells flower plants for a living.
Now the problem with flower plants is that they wither in a night if not taken care of. 
So at the end of the day, to make flower plants wither-resistant Roy uses special fertilizers.

There are N number of plants not sold on one particular day (say today), 
but Roy can sell them the next day (say tomorrow) if he fertilizes them tonight.
Roy sells a flower plant for Rs. X. Cost of fertilizing a plant is Rs. Y.
Currently Roy has P Rupees with him.

Given the selling price X and fertilizing cost Y of N plants, your task is to find minimum amount A (A ≤ P) 
that he should spend in fertilizing plants such that the total money B he has after selling plants on the next day is maximized. 
Assume that all the fertilized plants are sold on the next day.

Input Format:

First line contains two space separated integers N and P.
Following N lines each contain two space separated integers X and Y.

Output Format:
Print the two space separated integers A and B in a new line. 



### Sample Input 

5 100
100 40
50 40
40 50
60 20
100 50


### Sample Output 

90 210



### Explanation 

Profit for each of the plants is 60, 10, -10, 40, 50 respectively. He has Rs. 100 with him. 
The optimal selection would be fertilize first and last plant. 
So Minimum Amount to spend is Rs. 90 and 
total money he has after selling the plants is 100 - 40 - 50 + 100 + 100 =210


========= TestCases Prog-3 =========

case =1
input =5 100
100 40
50 40
40 50
60 20
100 50
output =90 210

case =2
input =7 100
100 30
134 65
142 23
152 74
125 50
145 26
165 78
output =99 413

case =3
input =4 100
100 70
50 40
40 50
60 20
output =90 170

case =4
input =6 100
100 20
50 40
100 30
40 50
60 20
100 60
output =70 290

case =5
input =10 100
100 20
50 40
100 30
40 50
60 20
100 60
100 70
50 40
40 50
60 20
output =90 330

case =6
input =4 120
100 30
134 65
145 26
165 78
output =104 326

case =7
input =9 150
100 30
134 65
142 23
152 74
125 50
145 26
165 78
100 60
150 65
output =144 543

case =8
input =5 125
100 40
120 58
130 75
90 45
150 60
output =118 277

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · RoyFlowerFarm.java
> ```java
> /*
> Roy is the owner of a flower plant farm and sells flower plants for a living.
> Now the problem with flower plants is that they wither in a night if not taken care of. 
> So at the end of the day, to make flower plants wither-resistant Roy uses special fertilizers.
>
> There are N number of plants not sold on one particular day (say today), 
> but Roy can sell them the next day (say tomorrow) if he fertilizes them tonight.
> Roy sells a flower plant for Rs. X. Cost of fertilizing a plant is Rs. Y.
> Currently Roy has P Rupees with him.
>
> Given the selling price X and fertilizing cost Y of N plants, your task is to find minimum amount A (A ≤ P) 
> that he should spend in fertilizing plants such that the total money B he has after selling plants on the next day is maximized. 
> Assume that all the fertilized plants are sold on the next day.
>
> Input Format:
>
> First line contains two space separated integers N and P.
> Following N lines each contain two space separated integers X and Y.
>
> Output Format:
> Print the two space separated integers A and B in a new line. 
>
>
> Sample Input :
> 5 100
> 100 40
> 50 40
> 40 50
> 60 20
> 100 50
>
> Sample Output :
> 90 210
>
>
> Explanation :
> Profit for each of the plants is 60, 10, -10, 40, 50 respectively. He has Rs. 100 with him. 
> The optimal selection would be fertilize first and last plant. 
> So Minimum Amount to spend is Rs. 90 and 
> total money he has after selling the plants is 100 - 40 - 50 + 100 + 100 =210
>
>
> ========= TestCases Prog-3 =========
>
> case =1
> input =5 100
> 100 40
> 50 40
> 40 50
> 60 20
> 100 50
> output =90 210
>
> case =2
> input =7 100
> 100 30
> 134 65
> 142 23
> 152 74
> 125 50
> 145 26
> 165 78
> output =99 413
>
> case =3
> input =4 100
> 100 70
> 50 40
> 40 50
> 60 20
> output =90 170
>
> case =4
> input =6 100
> 100 20
> 50 40
> 100 30
> 40 50
> 60 20
> 100 60
> output =70 290
>
> case =5
> input =10 100
> 100 20
> 50 40
> 100 30
> 40 50
> 60 20
> 100 60
> 100 70
> 50 40
> 40 50
> 60 20
> output =90 330
>
> case =6
> input =4 120
> 100 30
> 134 65
> 145 26
> 165 78
> output =104 326
>
> case =7
> input =9 150
> 100 30
> 134 65
> 142 23
> 152 74
> 125 50
> 145 26
> 165 78
> 100 60
> 150 65
> output =144 543
>
> case =8
> input =5 125
> 100 40
> 120 58
> 130 75
> 90 45
> 150 60
> output =118 277
>
> */
> import java.util.*;
> class RoyFlowerFarm{
> 	public static void main(String[] args) {
> 		Scanner ob=new Scanner(System.in);
> 			int n=ob.nextInt();
> 			int p=ob.nextInt();
> 			int x[]=new int[n];
> 			int y[]=new int[n];
> 			for(int i=0;i<n;i++){
> 				x[i]=ob.nextInt();
> 				y[i]=ob.nextInt();
> 			}
> 			int dp[][]=new int[n+1][p+1];
> 			for(int i=1;i<=n;i++){
> 				for (int j=1;j<=p;j++){
> 					if(j<y[i-1])
> 						dp[i][j]=dp[i-1][j];
> 					else
> 						dp[i][j]=Math.max(dp[i-1][j],dp[i-1][j-y[i-1]]+x[i-1]);
> 				}
> 			}
> 			int max=0,i,j=0;
> 			for(i=0;i<=p;i++){
> 				if(max<dp[n][i]-i+p){
> 					max=dp[n][i]-i+p;
> 					j=i;
> 				}
> 			}
> 			System.out.println(j+" "+max);
> 		
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2053%20Solutions/RoyFlowerFarm.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 53 Solutions/RoyFlowerFarm.java
