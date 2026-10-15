---
kind: "coding-problem"
title: "Lily Homework (Day 80)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 80 Solutions/LilyHomework.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Lily Homework (Day 80)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

### Input Format


The first line contains a single integer n, , the number of elements in arr. The second line contains n space-separated integers arr[i].



### Output Format


Return the minimum number of swaps needed to make the array beautiful.

Sample Input

4
2 5 3 1
Sample Output

2




Initial Thoughts: We can compare a sorted array to the original
                  and just keep track of the differences. As we
                  go we will need to perform the swaps, becasue we
                  are not guranteed 1 swap will fix both elements.
                  We will do this on both a ascending sort and a
                  descending sort as both meet the minimal 
                  requirement
                  
Time Complexity: O(n log(n)) //We must sort the input
Space Complexity: O(n) //We store the input in an array



case =1
input =4
2 5 3 1
output =2

case =2
input =7
2 5 3 1 8 7 6
output =3

case =3
input =4
1 2 3 4
output =0

case =4
input =8
2 5 3 1 9 8 7 6
output =4

case =5
input =12
2 1 4 3 6 5 8 7 10 9 12 11
output =6

case =6
input =5
4 5 3 2 1
output =1

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · LilyHomework.java
> ```java
>
> /*
>
>
> Input Format
>
> The first line contains a single integer n, , the number of elements in arr. The second line contains n space-separated integers arr[i].
>
>
> Output Format
>
> Return the minimum number of swaps needed to make the array beautiful.
>
> Sample Input
>
> 4
> 2 5 3 1
> Sample Output
>
> 2
>
>
>
>
> Initial Thoughts: We can compare a sorted array to the original
>                   and just keep track of the differences. As we
>                   go we will need to perform the swaps, becasue we
>                   are not guranteed 1 swap will fix both elements.
>                   We will do this on both a ascending sort and a
>                   descending sort as both meet the minimal 
>                   requirement
>                   
> Time Complexity: O(n log(n)) //We must sort the input
> Space Complexity: O(n) //We store the input in an array
>
>
>
> case =1
> input =4
> 2 5 3 1
> output =2
>
> case =2
> input =7
> 2 5 3 1 8 7 6
> output =3
>
> case =3
> input =4
> 1 2 3 4
> output =0
>
> case =4
> input =8
> 2 5 3 1 9 8 7 6
> output =4
>
> case =5
> input =12
> 2 1 4 3 6 5 8 7 10 9 12 11
> output =6
>
> case =6
> input =5
> 4 5 3 2 1
> output =1
>
> */
> import java.io.*;
> import java.util.*;
>
> public class LilyHomework{
>
>     public static void main(String[] args) {
>         Scanner input = new Scanner(System.in);
>         int n = input.nextInt();
>         
>         int sortedSwaps = 0;
>         int[] homework = new int[n];
>         Integer[] homeworkSorted = new Integer[n];
>         Map<Integer,Integer> original = new HashMap<>();
>         
>         int sortedReverseSwaps = 0;    
>         int[] homework2ndCopy = new int[n];        
>         Map<Integer,Integer> original2ndCopy = new HashMap<>();
>         
>         //Initialize our arrays and maps
>         for(int i = 0; i < n; i++)
>         {
>             homeworkSorted[i] = input.nextInt();
>             homework[i] = homeworkSorted[i];
>             homework2ndCopy[i] = homeworkSorted[i];
>             original.put(homework[i],i);
>             original2ndCopy.put(homework2ndCopy[i],i);
>         }
>             
>         Arrays.sort(homeworkSorted);//Sort the input ascending
>         
>         for(int i = 0; i < n; i++)
>         {
>             if(homework[i] != homeworkSorted[i])
>             {
>                 //swap the element from homework to the right position
>                 int tmp = homework[i];
>                 homework[i] = homework[original.get(homeworkSorted[i])];
>                 homework[original.get(homeworkSorted[i])] = tmp;
>                 //Update index after swap
>                 original.put(tmp,original.get(homeworkSorted[i]));
>                 sortedSwaps++;               
>             }
>         }
>         
>         Arrays.sort(homeworkSorted, Collections.reverseOrder());//Sort the input descending
>         
>         for(int i = 0; i < n; i++)
>         {
>             if(homework2ndCopy[i] != homeworkSorted[i])
>             {
>                 //swap the element from homework to the right position
>                 int tmp = homework2ndCopy[i];
>                 homework2ndCopy[i] = homework2ndCopy[original.get(homeworkSorted[i])];
>                 homework2ndCopy[original2ndCopy.get(homeworkSorted[i])] = tmp;
>                 //Update index after swap
>                 original2ndCopy.put(tmp, original2ndCopy.get(homeworkSorted[i]));
>                 sortedReverseSwaps++;
>             }
>         }
>         System.out.println(Math.min(sortedSwaps,sortedReverseSwaps));//Choose the smallest of the two possible smallest
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2080%20Solutions/LilyHomework.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 80 Solutions/LilyHomework.java
