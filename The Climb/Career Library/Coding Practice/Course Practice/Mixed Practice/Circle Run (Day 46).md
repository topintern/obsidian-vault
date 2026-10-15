---
kind: "coding-problem"
title: "Circle Run (Day 46)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 46 Solutions/CircleRun.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Circle Run (Day 46)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Alice likes to play with graphs a lot. Today he created a graph in the following way. 
He first lays down N nodes in a circle. The nodes are numbered from 1 to N, 
in the clockwise order, i.e. the node 2 is followed by 1, 3 is followed by 2, 
and 1 is followed by N. Two vertices are said to be adjacent if they don't have 
an intermediate vertex placed between them. There is an edge between 
each adjacent pair of vertices, so there are total N such edges. 
Each edge has an integer associated with it (may be negative).

Alice wants to find a walk from node start to node end using the above described edges. 
Alice has to pay cost for each edge in the walk equal to the integer associated with the edge. 
He wants to minimize the total cost he will incur. 
Also, Alice does not like to move through an edge more than twice. 
Note that a walk from a node u to v can contain repeated vertices in it.

Find out minimum cost that Alice has to pay.



### Input Format

------------
The first line contains a single integer N denoting the number of nodes.

The second line contains N space-separated integers R1, R2, ..., RN 
denoting the integer of the rib from node i to node (i % N) + 1. 
Note that RN is an integer on a rib from node N to node 1.

The third line contains two integers start and end 
denoting the first and the last node of the walk. 


### Output Format

------------
output a single line containing the minimal possible cost Alice need to pay.


Sample -1:
	Input:
	4
	1 2 1 1
	1 3
	Output:
	2

Explanation 1:

Alice's walk starts with node 1. He goes to node 4 by incurring a cost of 1. 
Then from node 4, he goes to node 3 by incurring a cost of 1 more. 
Total cost incurred is 2.

Sample Input 2:
5
-5 100 100 100 2
1 5

Sample Output 2:
-8

Explanation 2:

Alice goes from 1 to 2 by incurring a cost of -5. 
Then from 2 to 1 using the edge 2nd time and incurring cost of -5 again. 
Now, he can not use the edge between 1 and 2 again, as he has traversed the edge already twice. 
Now he will go from node 1 to node 4 by paying a cost of 2. 
Total sum of costs incurred is -5 + -5 + 2 = -8. 
This is the minimum possible cost that Alice can have.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · CircleRun.java
> ```java
> /*
> Alice likes to play with graphs a lot. Today he created a graph in the following way. 
> He first lays down N nodes in a circle. The nodes are numbered from 1 to N, 
> in the clockwise order, i.e. the node 2 is followed by 1, 3 is followed by 2, 
> and 1 is followed by N. Two vertices are said to be adjacent if they don't have 
> an intermediate vertex placed between them. There is an edge between 
> each adjacent pair of vertices, so there are total N such edges. 
> Each edge has an integer associated with it (may be negative).
>
> Alice wants to find a walk from node start to node end using the above described edges. 
> Alice has to pay cost for each edge in the walk equal to the integer associated with the edge. 
> He wants to minimize the total cost he will incur. 
> Also, Alice does not like to move through an edge more than twice. 
> Note that a walk from a node u to v can contain repeated vertices in it.
>
> Find out minimum cost that Alice has to pay.
>
>
> Input Format
> ------------
> The first line contains a single integer N denoting the number of nodes.
>
> The second line contains N space-separated integers R1, R2, ..., RN 
> denoting the integer of the rib from node i to node (i % N) + 1. 
> Note that RN is an integer on a rib from node N to node 1.
>
> The third line contains two integers start and end 
> denoting the first and the last node of the walk. 
>
> Output Format
> ------------
> output a single line containing the minimal possible cost Alice need to pay.
>
>
> Sample -1:
> 	Input:
> 	4
> 	1 2 1 1
> 	1 3
> 	Output:
> 	2
>
> Explanation 1:
>
> Alice's walk starts with node 1. He goes to node 4 by incurring a cost of 1. 
> Then from node 4, he goes to node 3 by incurring a cost of 1 more. 
> Total cost incurred is 2.
>
> Sample Input 2:
> 5
> -5 100 100 100 2
> 1 5
>
> Sample Output 2:
> -8
>
> Explanation 2:
>
> Alice goes from 1 to 2 by incurring a cost of -5. 
> Then from 2 to 1 using the edge 2nd time and incurring cost of -5 again. 
> Now, he can not use the edge between 1 and 2 again, as he has traversed the edge already twice. 
> Now he will go from node 1 to node 4 by paying a cost of 2. 
> Total sum of costs incurred is -5 + -5 + 2 = -8. 
> This is the minimum possible cost that Alice can have.
>
>
>
>
>
>
>  * 
>  */
>
> import java.util.*;
>
> public class CircleRun {
> 	
> 	private static long findMinCost(ArrayList<Integer> left,ArrayList<Integer> right) {
> 		long suml=0,sumr=0,maxl=0,sumsofar=0;
> 		//calculate total left side distance, from start to end
> 		// and , maximum left side distance from start to end
>         for(int i=0;i<left.size();i++){
>              suml+=left.get(i);
>              sumsofar=Math.max(sumsofar+left.get(i),left.get(i));
>              maxl=Math.max(maxl,sumsofar);
>         }
>       //calculate total right side distance, from start to end
>       // and , maximum right side distance from start to end
>         long maxr=0;sumsofar=0;
>         for(int i=0;i<right.size();i++){
>              sumr+=right.get(i);
>              sumsofar=Math.max(sumsofar+right.get(i),right.get(i));
>              maxr=Math.max(maxr,sumsofar);
>         }
>         //calculate the cost for left side path and right side path
>         long path1 = suml+2*(sumr-maxr);
>         long path2 = sumr+2*(suml-maxl);
>         
> 		//find the minimum cost between two paths and return
> 		return Math.min(path1, path2);
> 	}
> 	
>     public static void main(String[] args) {
>         
>         	Scanner sc = new Scanner(System.in);
>         	int N = sc.nextInt();
>         	int R[] = new int[N];
>         	for(int i=0; i<N; i++) {
>         		R[i] = sc.nextInt();
>         	}
>         	int start = sc.nextInt()-1;
>         	int end = sc.nextInt()-1;
>         	
>         	ArrayList<Integer> left=new ArrayList<Integer>();
>             ArrayList<Integer> right=new ArrayList<Integer>();
>             //left side index of an edge
>             for(int i=start;i<end;i++){
>                 left.add(R[i]);
>             }
>             //right side index of an edge
>             for(int i=end;;i=(i+1)%N){
>                 if(i==start)break;
>                 right.add(R[i]);
>             }
>             
>         	System.out.println(findMinCost(left, right));
>         
>     }
> }
>
> /*
> ======TestCases======
> case =1
> input =4
> 1 2 1 1
> 1 3
> output =2
>
> case =2
> input =5
> -5 100 100 100 2
> 1 5
> output =-8
>
> case =3
> input =10
> 1 -2 3 -4 5 -6 7 -8 9 -10
> 2 6
> output =-30
>
> case =4
> input =15
> 100 20 30 45 67 -72 98 43 12 -90 8 7 6 2 3 
> 12 5
> output =-174
>
> case =5
> input =10
> -72 98 43 12 -90 8 7 6 2 3
> 1 5
> output =-208
>
> case =6
> input =20
> -203 456 78 321 23 -76 -98 56 54 32 19 876 90 -56 78 -123 45 276 -89 200
> 6 12
> output =-13
>
> case =7
> input =20
> -203 456 78 321 23 -76 -98 56 54 32 19 876 90 -56 78 -123 45 276 -89 200
> 1 15
> output =-131
>
> case =8
> input =35
> -203 456 78 321 23 -76 -98 56 54 100 20 30 45 67 -72 98 43 12 -90 8 7 6 2 3 32 19 876 90 -56 78 -123 45 276 -89 200
> 5 24
> output =235
>
> case =9
> input =50
> -5 100 100 100 2 -203 456 78 321 23 -76 -98 56 54 100 20 30 45 67 -72 98 43 12 -90 8 7 6 2 3 32 19 876 90 -56 78 -123 45 276 -89 200 1 -2 3 -4 5 -6 7 -8 9 -10
> 15 35
> output =1022
>
> case =10
> input =50
> 1 -2 3 -4 5 -6 7 -8 9 -10 11 -12 13 -14 15 -16 17 -18 19 -20 21 -22 23 -24 25 -26 27 -28 29 -30 31 -32 33 -34 35 -36 37 -38 39 -40 41 -42 43 -44 45 -46 47 -48 49 -50
> 9 38
> output =-171
>
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2046%20Solutions/CircleRun.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 46 Solutions/CircleRun.java
