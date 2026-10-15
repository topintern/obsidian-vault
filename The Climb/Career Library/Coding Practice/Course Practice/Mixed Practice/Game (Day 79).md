---
kind: "coding-problem"
title: "Game (Day 79)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 79 Solutions/Game.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Game (Day 79)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Input Format:
    - The first line contains an integer n , the size of array arr.
    - The next line contains space-separated integers arr[i].

Output Format:
    - Print maximum possible score.
    

### Sample Input

4
3 3 3 3


### Sample Output

2


### Explanation

given set-> [3,3,3,3]
split into [3,3] [3,3] and discard left portion [3,3]
remaining array [3,3]
split in [3] [3] and discard left portion [3]
At this point the array only has 1 element and can no longer be partitioned, 
so we can split the array twice,so we print 3.



### Sample Input

7
8 2 0 2 2 0 2

### Sample Output

3


### Explanation

arr              A2         A3
[8,2,0,2,2,0,2]  [8]       [2,0,2,2,0,2]
[2,0,2,2,0,2]    [2,0,2]   [2,0,2]
[2,0,2]          [2,0]     [2]

so we can split the array trice, so we print 3.




case =1
input =3
3 3 3
output =0

case =2
input =4
5 5 5 5
output =2

case =3
input =7
4 1 0 1 1 0 1
output =3


case =4
input =10
2 0 2 4 0 2 4 2 0 0
output =3

case =5
input =9
4 1 0 1 1 0 1 1 0
output =0

case =6
input =8
1 1 1 1 1 1 2 2
output =1

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Game.java
> ```java
> /*
> Input Format:
>     - The first line contains an integer n , the size of array arr.
>     - The next line contains space-separated integers arr[i].
>
> Output Format:
>     - Print maximum possible score.
>     
> Sample Input:
> 4
> 3 3 3 3
>
> Sample Output:
> 2
>
> Explanation:
> given set-> [3,3,3,3]
> split into [3,3] [3,3] and discard left portion [3,3]
> remaining array [3,3]
> split in [3] [3] and discard left portion [3]
> At this point the array only has 1 element and can no longer be partitioned, 
> so we can split the array twice,so we print 3.
>
>
> Sample Input:
> 7
> 8 2 0 2 2 0 2
> Sample Output:
> 3
>
> Explanation:
> arr              A2         A3
> [8,2,0,2,2,0,2]  [8]       [2,0,2,2,0,2]
> [2,0,2,2,0,2]    [2,0,2]   [2,0,2]
> [2,0,2]          [2,0]     [2]
>
> so we can split the array trice, so we print 3.
>
>
>
>
> case =1
> input =3
> 3 3 3
> output =0
>
> case =2
> input =4
> 5 5 5 5
> output =2
>
> case =3
> input =7
> 4 1 0 1 1 0 1
> output =3
>
>
> case =4
> input =10
> 2 0 2 4 0 2 4 2 0 0
> output =3
>
> case =5
> input =9
> 4 1 0 1 1 0 1 1 0
> output =0
>
> case =6
> input =8
> 1 1 1 1 1 1 2 2
> output =1
>
>
>
>
> */
>
>
> import java.util.*;
> import java.math.*;
>
> public class Game{
>
>     private static int findMaxDivideCount(int[] inputs) {
>         int n = inputs.length;
>         
>         // Return 0 if array can't be partitioned (need at least 2 elements to split)
>         if(n < 2) {
>             return 0;
>         }
>
>         // Initialize rightSum as array sum
>         int rightSum = 0;
>         for (int i = 0; i < n; i++) {
>             rightSum += inputs[i];
>         }
>
>         // Determine if array can be partitioned into equal leftSum and rightSum
>         int leftSum = 0;
>         int partitionIndex = 0;
>         boolean isEqual = false;
>         do {
>             // Deduct each value added to rightSum from leftSum
>             leftSum += inputs[partitionIndex];
>             rightSum -= inputs[partitionIndex];
>
>             // Check balance (i.e., are the two sums equal yet?)
>             if(leftSum == rightSum){
>                 isEqual = true;
>                 break;
>             }
>             
>         } while(++partitionIndex < n);
>         
>         // If sums are not equal, return 0 as current array can't be split into halves with equal sums
>         if(!isEqual) {
>             return 0;
>         }
>
>         // Else she gets 1 point, continue checking the left/right subarrays
>         return 1 + Math.max(
>                     findMaxDivideCount(Arrays.copyOfRange(inputs, 0, partitionIndex + 1)),       
>                     findMaxDivideCount(Arrays.copyOfRange(inputs, partitionIndex + 1, n))
>         );
>     }
>     
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>             int n = in.nextInt();
>             int[] inputs = new int[n];
>
>             for (int j = 0; j < n; j++) {
>                 inputs[j] = in.nextInt();
>             }
>
>             System.out.println(findMaxDivideCount(inputs));
>         
>         in.close();
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2079%20Solutions/Game.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 79 Solutions/Game.java
