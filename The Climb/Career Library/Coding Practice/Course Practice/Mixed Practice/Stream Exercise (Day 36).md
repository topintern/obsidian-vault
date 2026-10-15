---
kind: "coding-problem"
title: "Stream Exercise (Day 36)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 36 Solutions/StreamExercise.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Stream Exercise (Day 36)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Display the list of strings with length is <=k using stream api.
Print largest odd number in the given array of elements using stream api.
Print all statistics(Max,Min,Sum,Avg) using Statistics Collectors on a given list.


### Input Format

------------
First line of the input contains 2 integers N, K. 
N is the number of strings. K is the length of the word.
Next N lines are strings
Next list of numbers. List size is <=20


### Output Format

-------------
Print list of strings with length is <=K 
Print largest odd number in the given array
Next Four Lines of output follows
Maximum number of list,
Minimum number of list,
Sum of list,
Average of list(Average Value - Round up to 2 decimal places)


Sample Input
4 5
Elite
Finishing School
SONET
Trishul
10 17 21 5 44

Sample Output
Elite SONET 
21
44
5
97
19.4

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · StreamExercise.java
> ```java
> /*
>
> Display the list of strings with length is <=k using stream api.
> Print largest odd number in the given array of elements using stream api.
> Print all statistics(Max,Min,Sum,Avg) using Statistics Collectors on a given list.
>
> Input Format
> ------------
> First line of the input contains 2 integers N, K. 
> N is the number of strings. K is the length of the word.
> Next N lines are strings
> Next list of numbers. List size is <=20
>
> Output Format
> -------------
> Print list of strings with length is <=K 
> Print largest odd number in the given array
> Next Four Lines of output follows
> Maximum number of list,
> Minimum number of list,
> Sum of list,
> Average of list(Average Value - Round up to 2 decimal places)
>
>
> Sample Input
> 4 5
> Elite
> Finishing School
> SONET
> Trishul
> 10 17 21 5 44
>
> Sample Output
> Elite SONET 
> 21
> 44
> 5
> 97
> 19.4
>
>
> */
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.*;
> import java.util.stream.*;
>
> class StreamExercise {
> 	public static void main(String args[]) throws IOException {
>
> 		
>         BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
>
>         String numbers []=br.readLine().split(" "); 
> 		//reading list of strings
> 		int numOfWords = Integer.parseInt(numbers[0]);
> 		
> 		int k = Integer.parseInt(numbers[1]); // length of word
> 		
> 		List<String> wordsList = new ArrayList<String>();
> 		for (int i = 0; i < numOfWords; i++)
> 			wordsList.add(br.readLine());
>
> 		String ListOfNums []=br.readLine().split(" "); 
>
> 		//reading list of numbers
> 		int numOfElem = ListOfNums.length;
> 		List<Integer> numberList = new ArrayList<Integer>();
> 		for (int i = 0; i < numOfElem; i++)
> 			numberList.add(Integer.parseInt(ListOfNums[i]));
>
> 		// Display the list of strings with length is <=k using stream api
> 		List<String> result = wordsList.stream().filter(str -> str.length() <= k).collect(Collectors.toList());
> 		//System.out.println(result);
> 		result.stream().forEach(str->System.out.print(str+" ")); 
> 		System.out.println("");
> 		//Print largest odd number in the given array of elements using stream api.
> 		int largestOddNum = numberList.stream().filter(x -> x % 2 != 0).reduce(0,
> 				(max, ele) -> (max < ele) ? ele : max);
> 		System.out.println(largestOddNum);
> 		
> 		IntSummaryStatistics stats = numberList.stream().mapToInt((x) -> x).summaryStatistics();
>
> 		double avg = Math.round(stats.getAverage() * 100.0) / 100.0;
>
>
> 		System.out.println(stats.getMax());
> 		System.out.println(stats.getMin());
> 		System.out.println(stats.getSum());
> 		System.out.println(avg);
>
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2036%20Solutions/StreamExercise.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 36 Solutions/StreamExercise.java
