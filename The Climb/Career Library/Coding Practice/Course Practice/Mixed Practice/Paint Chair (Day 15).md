---
kind: "coding-problem"
title: "Paint Chair (Day 15)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 15 Solutions/PaintChair.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Paint Chair (Day 15)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

There are a row of n chairs, each chair can be painted with one of the three colors: red, blue or green. 
The cost of painting each chair with a certain color is different. 
You have to paint all the chairs such that no two adjacent chairs have the same color.

The cost of painting each chair with a certain color is represented by a n x 3 cost matrix. 
For example, costs[0][0] is the cost of painting chair 0 with color red; 
costs[1][2] is the cost of painting chair 1 with color green, and so on... 
Find the minimum cost to paint all chairs.

Note:
All costs are positive integers.

Example:

Input=	3
			17 2 17
			16 16 5
			14 3 19
Output= 10
Explanation: Paint chair 0 into blue, paint chair 1 into green, paint chair 2 into blue. 
 Minimum cost: 2 + 5 + 3 = 10.
 
 ======TestCases========
 case =1
input =4
12 6 18
17 19 20
13 15 3
7 2 8
output =28

case =2
input =7
19 3 7
38 5 7
1 2 3
4 5 6
6 7 8
3 6 9
2 4 6
output =30

case =3
input =5
19 3 7
38 5 7
1 2 3
4 5 6
6 7 8
output =22

case =4
input =9
30 14 78
92 45 76
19 3 7
38 5 7
1 2 3
4 5 6
6 7 8
3 6 9
2 4 6
output =107

case =5
input =12
98 107 45
39 82 65
37 19 49
30 14 78
92 45 76
19 3 7
38 5 7
1 2 3
4 5 6
6 7 8
3 6 9
2 4 6
output =210

case =6
input =6
98 107 45
39 82 65
37 19 49
30 14 78
92 45 76
19 3 7
output =185

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · PaintChair.java
> ```java
> /*
> There are a row of n chairs, each chair can be painted with one of the three colors: red, blue or green. 
> The cost of painting each chair with a certain color is different. 
> You have to paint all the chairs such that no two adjacent chairs have the same color.
>
> The cost of painting each chair with a certain color is represented by a n x 3 cost matrix. 
> For example, costs[0][0] is the cost of painting chair 0 with color red; 
> costs[1][2] is the cost of painting chair 1 with color green, and so on... 
> Find the minimum cost to paint all chairs.
>
> Note:
> All costs are positive integers.
>
> Example:
>
> Input=	3
> 			17 2 17
> 			16 16 5
> 			14 3 19
> Output= 10
> Explanation: Paint chair 0 into blue, paint chair 1 into green, paint chair 2 into blue. 
>  Minimum cost: 2 + 5 + 3 = 10.
>  
>  ======TestCases========
>  case =1
> input =4
> 12 6 18
> 17 19 20
> 13 15 3
> 7 2 8
> output =28
>
> case =2
> input =7
> 19 3 7
> 38 5 7
> 1 2 3
> 4 5 6
> 6 7 8
> 3 6 9
> 2 4 6
> output =30
>
> case =3
> input =5
> 19 3 7
> 38 5 7
> 1 2 3
> 4 5 6
> 6 7 8
> output =22
>
> case =4
> input =9
> 30 14 78
> 92 45 76
> 19 3 7
> 38 5 7
> 1 2 3
> 4 5 6
> 6 7 8
> 3 6 9
> 2 4 6
> output =107
>
> case =5
> input =12
> 98 107 45
> 39 82 65
> 37 19 49
> 30 14 78
> 92 45 76
> 19 3 7
> 38 5 7
> 1 2 3
> 4 5 6
> 6 7 8
> 3 6 9
> 2 4 6
> output =210
>
> case =6
> input =6
> 98 107 45
> 39 82 65
> 37 19 49
> 30 14 78
> 92 45 76
> 19 3 7
> output =185
>
>  */
>
> import java.util.Scanner;
>
> public class Paintchair {
> 	public static int minCost(int[][] costs) {
> 	    if(costs==null||costs.length==0){
> 	        return 0;
> 	    }
> 	    for(int i=1; i<costs.length; i++){
> 	        costs[i][0] += Math.min(costs[i-1][1],costs[i-1][2]);
> 	        costs[i][1] += Math.min(costs[i-1][0],costs[i-1][2]);
> 	        costs[i][2] += Math.min(costs[i-1][1],costs[i-1][0]);
> 	    }
> 	    int n = costs.length-1;
> 	    return Math.min(Math.min(costs[n][0], costs[n][1]), costs[n][2]);
> 	}
> 	
> 	public static void main(String args[] ) {
> 		 Scanner scan = new Scanner(System.in);
> 			int n=scan.nextInt();
>
> 			int[][] chaircolors=new int[n][3];
> 		       for(int i=0; i<n; i++)
> 		       {
> 		           for(int j=0; j<3; j++)
> 		           {
> 		        	   chaircolors[i][j] = scan.nextInt();
> 		           }
> 		       }
> 		       System.out.println(minCost(chaircolors));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2015%20Solutions/PaintChair.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 15 Solutions/PaintChair.java
