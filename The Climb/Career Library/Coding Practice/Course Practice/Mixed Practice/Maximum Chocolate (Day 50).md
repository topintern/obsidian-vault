---
kind: "coding-problem"
title: "Maximum Chocolate (Day 50)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 50 Solutions/MaximumChocolate.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Maximum Chocolate (Day 50)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Bharat is chocoholic. He found a chocolate factory of N floors ,
but the factory has N*N rooms where in each room specific number of chocolate 
is present. Now, Bharat starts collecting chocolate from ground floor. 
He can only collect chocolate from one room in a floor. Bharat can only 
move to upper room or upper-right room or upper-left room .

He want to collect maximum number of chocolate possible. Help him in 
finding maximum number of chocolate.


### Input Format

------------
First line contains a value of N. 
Next N lines contains N space separated integer.


### Output Format

-------------
Output a single integer denoting the maximum number of chocolate Bharat can collect.



### Sample Input

5
1 2 3 4 5
1 2 3 4 5
1 2 3 4 5
1 2 3 4 5
100 2 3 4 5


### Sample Output

114

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MaximumChocolate.java
> ```java
> /*
>  * 
> Bharat is chocoholic. He found a chocolate factory of N floors ,
> but the factory has N*N rooms where in each room specific number of chocolate 
> is present. Now, Bharat starts collecting chocolate from ground floor. 
> He can only collect chocolate from one room in a floor. Bharat can only 
> move to upper room or upper-right room or upper-left room .
>
> He want to collect maximum number of chocolate possible. Help him in 
> finding maximum number of chocolate.
>
> Input Format
> ------------
> First line contains a value of N. 
> Next N lines contains N space separated integer.
>
> Output Format
> -------------
> Output a single integer denoting the maximum number of chocolate Bharat can collect.
>
>
> Sample Input:
> 5
> 1 2 3 4 5
> 1 2 3 4 5
> 1 2 3 4 5
> 1 2 3 4 5
> 100 2 3 4 5
>
> Sample Output:
> 114
>
>
>  * 
>  */
> import java.util.*;
>
> class MaximumChocolate {
> 	public static void main(String[] args) {
> 		Scanner sc = new Scanner(System.in);
> 		int n = sc.nextInt();
> 		int a[][] = new int[n][n];
> 		for (int i = 0; i < n; i++) {
> 			for (int j = 0; j < n; j++) {
> 				a[i][j] = sc.nextInt();
> 			}
> 		}
> 		for (int i = n - 2; i >= 0; i--) {
> 			for (int j = 0; j < n; j++) {
> 				int x = 0;
> 				// it checks for lower left room of current room
> 				if (j > 0) {
> 					x = Math.max(x, a[i + 1][j - 1]);
> 				}
>
> 				if (j < n - 1)
> 					x = Math.max(x, a[i + 1][j + 1]);// checks for lower right room of current room
> 				x = Math.max(x, a[i + 1][j]);// checks for lower room of current room
>
> 				a[i][j] += x;// updates cumulative sum of chocolates which he collects in this position
> 			}
> 		}
>
> 		
> 		int max = 0;
> 		for (int i = 0; i < n; i++)
> 			if (a[0][i] > max)// so, the maximum values will be in last row. get max value
> 				max = a[0][i];
> 		System.out.println(max);
> 	}
> }
>
>
> /*
> ========= Testcases Program-1 =========
> case =1
> input =5
> 1 2 3 4 5
> 1 2 3 4 5
> 1 2 3 4 5
> 1 2 3 4 5
> 100 2 3 4 5
> output =114
>
> case =2
> input =5
> 285 140 76 66 30
> 133 272 401 47 3
> 42 127 18 442 468
> 10 266 115 273 290
> 57 73 385 108 89
> output =1641
>
> case =3
> input =6
> 356 255 320 410 427 344
> 418 59 453 452 270 395
> 23 151 2 315 460 189
> 258 109 444 126 483 180
> 146 349 396 315 435 454
> 238 34 194 146 140 366
> output =2642
>
> case =4
> input =6
> 48 165 96 164 79 68
> 181 51 186 39 102 101
> 118 242 238 171 120 132
> 78 171 163 109 204 182
> 156 73 145 230 80 198
> 228 4 191 75 122  38
> output =1177
>
> case =5
> input =7
> 129 133 129 122 128 131 128
> 128 132 133 122 127 128 129
> 125 129 127 130 135 131 124
> 135 128 128 126 122 134 126
> 122 131 125 130 122 126 123
> 129 132 135 135 123 120 120
> 130 128 135 125 123 131 121
> output =931
>
> case =6
> input =8
> 82 53 81 68 51 87 62 97
> 97 53 58 88 80 79 65 53
> 81 94 85 79 92 78 55 50
> 80 98 85 53 59 91 70 90
> 80 58 99 94 72 61 79 64
> 72 51 78 57 64 86 80 83
> 62 59 76 60 76 91 95 87
> 87 62 63 85 78 68 62 50
> output =709
>
> case =7
> input =9
> 517 129 698 825 801 138 926 617 934
> 297 486 550 374 793 825 199 850 512
> 555 397 235 790 121 767 650 174 846
> 789 550 291 588 981 589 219 286 575
> 421 873 923 766 793 284 931 145 352
> 195 854 210 415 828 947 927 219 858
> 837 902 994 381 701 172 395 369 558
> 396 129 994 838 841 929 780 188 609
> 685 525 206 560 770 930 548 886 250
> output =7799
>
> case =8
> input =10
> 8081 2220 6459 9003 8425 4906 8342 6562 5077 4904
> 3030 5876 8092 8299 1173 9854 9384 7546 8847 7100
> 3606 9412 4753 6395 7680 6276 4468 7617 4477 6691
> 8684 5180 7735 4705 9326 3074 9788 4169 2780 4666
> 2307 4149 5220 3030 9168 9452 3231 2020 3986 1100
> 2756 3543 6828 3092 9723 8041 1736 9950 6231 3864
> 6944 5655 3259 1163 1669 8867 5073 2859 7812 7922
> 6801 7944 6521 3632 4289 3985 1719 2361 4221 3531
> 4362 6478 4188 5173 7938 6715 4110 3608 5552 1187
> 4922 4277 1211 8364 7099 8806 4665 3256 1603 8415
> output =84360
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2050%20Solutions/MaximumChocolate.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 50 Solutions/MaximumChocolate.java
