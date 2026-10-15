---
kind: "coding-problem"
title: "Queue Reconstruction (Day 32)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 32 Solutions/QueueReconstruction.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Queue Reconstruction (Day 32)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Suppose you have a random list of people standing in a queue. 
Each person is described by a pair of integers (h, k), 
where h is the height of the person and 
k is the number of people in front of this person who have a height greater than or equal to h.

Write an algorithm to reconstruct the queue.

Note:
The number of people is less than 1,100.

 
Example

    Input:6
    7 0
    4 4
    7 1
    5 0
    6 1
    5 2
    
    Output:
    [[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]


------------testcases------------------
case =1
input =7
3 6
7 1
4 0
6 0
7 0
5 2
6 2
output =[[4, 0], [6, 0], [7, 0], [5, 2], [6, 2], [7, 1], [3, 6]]

case =2
input =6
2 0
4 0
5 0
3 0
1 0
6 0
output =[[1, 0], [2, 0], [3, 0], [4, 0], [5, 0], [6, 0]] 

case =3
input =7
2 1
2 4
4 1
3 0
6 0
5 0
2 2
output =[[3, 0], [2, 1], [2, 2], [5, 0], [2, 4], [4, 1], [6, 0]]  

case =4
input =5
6 0
7 2
8 1
9 0
5 2
output =[[6, 0], [9, 0], [5, 2], [8, 1], [7, 2]]  

case =5
input =8
2 0
4 3
5 1
6 2
7 1
8 0
3 4
7 2
output =[[2, 0], [8, 0], [5, 1], [7, 1], [4, 3], [3, 4], [6, 2], [7, 2]] 

case =6
input =6
1 5
2 4
3 3
4 2
5 1
6 0
output =[[6, 0], [5, 1], [4, 2], [3, 3], [2, 4], [1, 5]]

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · QueueReconstruction.java
> ```java
> /*
> Suppose you have a random list of people standing in a queue. 
> Each person is described by a pair of integers (h, k), 
> where h is the height of the person and 
> k is the number of people in front of this person who have a height greater than or equal to h.
>
> Write an algorithm to reconstruct the queue.
>
> Note:
> The number of people is less than 1,100.
>
>  
> Example
>
>     Input:6
>     7 0
>     4 4
>     7 1
>     5 0
>     6 1
>     5 2
>     
>     Output:
>     [[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
>
>
> ------------testcases------------------
> case =1
> input =7
> 3 6
> 7 1
> 4 0
> 6 0
> 7 0
> 5 2
> 6 2
> output =[[4, 0], [6, 0], [7, 0], [5, 2], [6, 2], [7, 1], [3, 6]]
>
> case =2
> input =6
> 2 0
> 4 0
> 5 0
> 3 0
> 1 0
> 6 0
> output =[[1, 0], [2, 0], [3, 0], [4, 0], [5, 0], [6, 0]] 
>
> case =3
> input =7
> 2 1
> 2 4
> 4 1
> 3 0
> 6 0
> 5 0
> 2 2
> output =[[3, 0], [2, 1], [2, 2], [5, 0], [2, 4], [4, 1], [6, 0]]  
>
> case =4
> input =5
> 6 0
> 7 2
> 8 1
> 9 0
> 5 2
> output =[[6, 0], [9, 0], [5, 2], [8, 1], [7, 2]]  
>
> case =5
> input =8
> 2 0
> 4 3
> 5 1
> 6 2
> 7 1
> 8 0
> 3 4
> 7 2
> output =[[2, 0], [8, 0], [5, 1], [7, 1], [4, 3], [3, 4], [6, 2], [7, 2]] 
>
> case =6
> input =6
> 1 5
> 2 4
> 3 3
> 4 2
> 5 1
> 6 0
> output =[[6, 0], [5, 1], [4, 2], [3, 3], [2, 4], [1, 5]]  
>
>
> */
>
> import java.util.*;
>
> public class QueueReconstruction {
>
> 	public static int[][] reconstructQueue(int[][] people) {
>         //pick up the tallest guy first
>         //when insert the next tall guy, just need to insert him into kth position
>         //repeat until all people are inserted into list
>         Arrays.sort(people,new Comparator<int[]>(){
>            @Override
>            public int compare(int[] o1, int[] o2){
>                return o1[0]!=o2[0]?-o1[0]+o2[0]:o1[1]-o2[1];
>            }
>         });
>         List<int[]> res = new LinkedList<>();
>         for(int[] cur : people){
>             res.add(cur[1],cur);       
>         }
>         return res.toArray(new int[people.length][]);
>     }
> 	public static void main(String args[] ) {
> 		 Scanner scan = new Scanner(System.in);
> 			int n=scan.nextInt();
>
> 			int[][] people=new int[n][2];
> 		       for(int i=0; i<n; i++)
> 		       {
> 		           for(int j=0; j<2; j++)
> 		           {
> 		        	   people[i][j] = scan.nextInt();
> 		           }
> 		       }
> 		       System.out.println(Arrays.deepToString(reconstructQueue(people)));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2032%20Solutions/QueueReconstruction.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 32 Solutions/QueueReconstruction.java
