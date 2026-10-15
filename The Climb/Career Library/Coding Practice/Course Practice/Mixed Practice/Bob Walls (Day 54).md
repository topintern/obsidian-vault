---
kind: "coding-problem"
title: "Bob Walls (Day 54)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 54 Solutions/BobWalls.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Bob Walls (Day 54)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Bob the builder has constructed some walls of various length in a line. Now, he wants to count the total number of walls constructed and report that number to his boss. But the report that Bob made was wrong because he counted the total number of walls by standing on the leftmost side of the first wall. So he was only able to see some walls and not all because others were hidden behind. Can you predict the number of walls counted by Bob.


### Input

First line contains T denoting the number of test cases.
First line of each test case contains N denoting the actual no of walls.
Second line of each test case contains N integers (A1...An) denoting the height of each walls.


### Output

For each test case print a single integer denoting the total no of walls as counted by Bob each in a new line.



### Sample input 

5
1 3 2 5 4


### Sample Output 

3



### Explanation 

Bob will only be able to see the walls of length 1,3 and 5

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · BobWalls.java
> ```java
> /*
>
> Bob the builder has constructed some walls of various length in a line. Now, he wants to count the total number of walls constructed and report that number to his boss. But the report that Bob made was wrong because he counted the total number of walls by standing on the leftmost side of the first wall. So he was only able to see some walls and not all because others were hidden behind. Can you predict the number of walls counted by Bob.
>
> Input
> First line contains T denoting the number of test cases.
> First line of each test case contains N denoting the actual no of walls.
> Second line of each test case contains N integers (A1...An) denoting the height of each walls.
>
> Output
> For each test case print a single integer denoting the total no of walls as counted by Bob each in a new line.
>
>
> Sample input :
> 5
> 1 3 2 5 4
>
> Sample Output :
> 3
>
>
> Explanation :
> Bob will only be able to see the walls of length 1,3 and 5
>
>
>
> */
>
> import java.io.*;
>  
> //import for Scanner and other utility classes
> import java.util.*;
>  
>  
> // Warning: Printing unwanted or ill-formatted data to output will cause the test cases to fail
>  
> class BobWalls {
>     
>     static int visible(int[] arr, int numWalls){
>             int max = 0;
>             int count = 0;
>             for(int i=0;i<numWalls;i++){
>                 if(arr[i]>max){
>                     count++;
>                     max=arr[i];
>                 }
>             }
>         return count;    
>         }
>     public static void main(String args[] ) throws Exception {
>         Scanner in = new Scanner(System.in);
>             int numWalls = in.nextInt();
>             int[] arr = new int[numWalls];
>             for(int i=0;i<numWalls;i++){
>                 arr[i]=in.nextInt();
>             }
>             int a = visible(arr,numWalls);
>             System.out.println(a);
>            
>     }
>         
>         
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2054%20Solutions/BobWalls.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 54 Solutions/BobWalls.java
