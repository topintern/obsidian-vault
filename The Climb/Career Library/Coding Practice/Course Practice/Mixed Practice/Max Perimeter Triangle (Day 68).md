---
kind: "coding-problem"
title: "Max Perimeter Triangle (Day 68)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 68 Solutions/MaxPerimeterTriangle.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Max Perimeter Triangle (Day 68)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given an array of stick lengths, use 3 of them to construct a non-degenerate triange 
with the maximum possible perimeter. 
Print the lengths of its sides as 3 space-separated integers in non-decreasing order.

If there are several valid triangles having the maximum perimeter:
	- Choose the one with the longest maximum side.
	- If more than one has that maximum, choose from them the one with the longest minimum side.
	- If more than one has that maximum as well, print any one them.
	- If no non-degenerate triangle exists, print -1.

For example, assume there are stick lengths sticks=[1,2,3,4,5,10]. 
The triplet (1,2,3) will not form a triangle. 
Neither will (4,5,10) or (2,3,5), so the problem is reduced to (2,3,4) and (3,4,5). 
The longer perimeter is 3+4+5=12.


### Input Format

	- The first line contains single integer n, the size of array sticks.
	- The second line contains n space-separated integers sticks[i], each a stick length.


### Output Format

	- Print the lengths of the 3 chosen sticks as space-separated integers in non-decreasing order.
	- If no non-degenerate triangle can be formed, print -1.

Sample Input1:
5
1 1 1 3 3
Sample Output1:
1 3 3
Explanation1:
There are 2 possible unique triangles:
	1 1 1
	1 3 3
The second triangle has the largest perimeter, 
so we print its side lengths on a new line in non-decreasing order.

Sample Input2:
3
1 2 3
Sample Output2:
-1
Explanation2:
The triangle (1,2,3) is degenerate and thus can't be constructed, 
so we print -1 on a new line.

Sample Input3:
6
1 1 1 2 3 5
Sample Output3:
1 1 1
Explanation3:
The triangle (1,1,1) is the only valid triangle.


========= Testcases Program-1 =========
case =1
input =5
1 1 1 3 3
output =1 3 3

case =2
input =3
1 2 3
output =-1

case =3
input =8
1 4 7 8 9 15 24 39
output =8 9 15

case =4
input =6
1 1 1 2 3 5
output =1 1 1

case =5
input =7
1 2 4 6 8 11 12
output =8 11 12

case =6
input =10
3 7 9 13 15 28 45 76 103 189
output =45 76 103

case =7
input =6
1 3 5 7 15 24
output =3 5 7

case =8
input =9
7 10 16 27 44 67 112 179 292
output =27 44 67

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MaxPerimeterTriangle.java
> ```java
> /*
>
> Given an array of stick lengths, use 3 of them to construct a non-degenerate triange 
> with the maximum possible perimeter. 
> Print the lengths of its sides as 3 space-separated integers in non-decreasing order.
>
> If there are several valid triangles having the maximum perimeter:
> 	- Choose the one with the longest maximum side.
> 	- If more than one has that maximum, choose from them the one with the longest minimum side.
> 	- If more than one has that maximum as well, print any one them.
> 	- If no non-degenerate triangle exists, print -1.
>
> For example, assume there are stick lengths sticks=[1,2,3,4,5,10]. 
> The triplet (1,2,3) will not form a triangle. 
> Neither will (4,5,10) or (2,3,5), so the problem is reduced to (2,3,4) and (3,4,5). 
> The longer perimeter is 3+4+5=12.
>
> Input Format
> 	- The first line contains single integer n, the size of array sticks.
> 	- The second line contains n space-separated integers sticks[i], each a stick length.
>
> Output Format
> 	- Print the lengths of the 3 chosen sticks as space-separated integers in non-decreasing order.
> 	- If no non-degenerate triangle can be formed, print -1.
>
> Sample Input1:
> 5
> 1 1 1 3 3
> Sample Output1:
> 1 3 3
> Explanation1:
> There are 2 possible unique triangles:
> 	1 1 1
> 	1 3 3
> The second triangle has the largest perimeter, 
> so we print its side lengths on a new line in non-decreasing order.
>
> Sample Input2:
> 3
> 1 2 3
> Sample Output2:
> -1
> Explanation2:
> The triangle (1,2,3) is degenerate and thus can't be constructed, 
> so we print -1 on a new line.
>
> Sample Input3:
> 6
> 1 1 1 2 3 5
> Sample Output3:
> 1 1 1
> Explanation3:
> The triangle (1,1,1) is the only valid triangle.
>
>
> ========= Testcases Program-1 =========
> case =1
> input =5
> 1 1 1 3 3
> output =1 3 3
>
> case =2
> input =3
> 1 2 3
> output =-1
>
> case =3
> input =8
> 1 4 7 8 9 15 24 39
> output =8 9 15
>
> case =4
> input =6
> 1 1 1 2 3 5
> output =1 1 1
>
> case =5
> input =7
> 1 2 4 6 8 11 12
> output =8 11 12
>
> case =6
> input =10
> 3 7 9 13 15 28 45 76 103 189
> output =45 76 103
>
> case =7
> input =6
> 1 3 5 7 15 24
> output =3 5 7
>
> case =8
> input =9
> 7 10 16 27 44 67 112 179 292
> output =27 44 67
>
> */
> import java.io.*;
> import java.util.*;
>
> public class MaxPerimeterTriangle {
>
>     public static void main(String[] args)throws IOException
>     {
>         BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
>         int n=Integer.parseInt(br.readLine());
>         String input[]=br.readLine().split(" ");
>         int a[]=new int[n];
>         for(int i=0;i<n;i++)
>             a[i]=Integer.parseInt(input[i]);
>         
>         Arrays.sort(a);
>         int i=n-1;
>         while(i>1)
>         {
>             if(a[i]<a[i-1]+a[i-2])
>             {
>                 System.out.println(a[i-2]+" "+a[i-1]+" "+a[i]);
>                 break;
>             }
>             i--;
>         }
>         if(i==1)
>             System.out.println(-1);
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2068%20Solutions/MaxPerimeterTriangle.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 68 Solutions/MaxPerimeterTriangle.java
