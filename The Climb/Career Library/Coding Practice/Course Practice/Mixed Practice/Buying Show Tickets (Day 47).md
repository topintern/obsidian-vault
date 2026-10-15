---
kind: "coding-problem"
title: "Buying Show Tickets (Day 47)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 47 Solutions/BuyingShowTickets.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Buying Show Tickets (Day 47)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Alex plans on visiting the museum and is at the counter to purchase tickets to get in. 
Tickets are sold only one at a time. If a visitor needs more than one ticket, 
he/she has to pass through the queue again to buy each one.

Given the number of visitors and the number of tickets each visitor needs, 
determine the amount of time Alex requires to buy the number needed. 
Alex's place in the queue will be given. Each transaction takes 1 unit of time. and 
the time taken to go to the back of the line can be ignored.

Example 1:
	Input:1 2 5		
			 1
	Output: 4

	Explanation:
		There are 3 buyers needing 1, 2 and 5 tickets each. Alex is at index 1 and need 2 tickets.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · BuyingShowTickets.java
> ```java
> /*
> Alex plans on visiting the museum and is at the counter to purchase tickets to get in. 
> Tickets are sold only one at a time. If a visitor needs more than one ticket, 
> he/she has to pass through the queue again to buy each one.
>
> Given the number of visitors and the number of tickets each visitor needs, 
> determine the amount of time Alex requires to buy the number needed. 
> Alex's place in the queue will be given. Each transaction takes 1 unit of time. and 
> the time taken to go to the back of the line can be ignored.
>
> Example 1:
> 	Input:1 2 5		
> 			 1
> 	Output: 4
>
> 	Explanation:
> 		There are 3 buyers needing 1, 2 and 5 tickets each. Alex is at index 1 and need 2 tickets. 
> 		
>  */
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
> import java.util.List;
> import java.util.stream.Collectors;
>
> public class BuyingShowTickets {
>   public static long calculateTimeOptimized(List<Integer> line, int pos) {
>     long waitingTime = line.get(pos);
>     for (int i = 0; i < line.size(); i++) {
>       if (i == pos) continue;
>       waitingTime += (Math.min(line.get(pos), line.get(i)));
>       if (i > pos) {
>         waitingTime--;
>       }
>     }
>
>     return waitingTime;
>   }
>
>   public static void main(String args[]) throws IOException {
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		String str = br.readLine();
> 		String[] numberline = str.split(" ");
> 		int[] A = Arrays.asList(numberline).stream().mapToInt(Integer::parseInt).toArray();
> 		int B = Integer.parseInt(br.readLine());
> 		List<Integer> list = Arrays.stream(A).boxed().collect(Collectors.toList());
> 	    System.out.println(calculateTimeOptimized(list, B));
> 	}
>  
> }
>
>
>
> /*
>
> =====TestCases======
> case =1
> input =1 2 5
> 1
> output =4
>
> case =2
> input =1 2 7 1 7
> 2
> output =16
>
> case =3
> input =7 1 7 4 7 2 5 3 6 3
> 3
> output =27
>
> case =4
> input =1 9 1 1 5 8 9 9 1 6 7 2 6 3 1
> 5
> output =57
>
> case =5
> input =9 7 7 5 9 1 5 7 6 2 4 1 2 5 4 3 5 1 3 2
> 11
> output =12
>
> case =6
> input =8 15 8 10 13 8 3 7 1 12 2 10 11 3 6 15 10 3 1 3 5 6 2 13 12
> 15
> output =178
>
> case =7
> input =2 15 11 5 11 10 4 6 12 12 7 4 11 2 9 3 15 2 9 8 3 4 15 15 15 9 5 10 7 6 11 8 15 4 3
> 24
> output =278
>
> case =8
> input =7 3 13 3 2 5 3 8 9 12 11 3 11 10 1 10 8 10 13 7 14 6 12 5 14 3 7 6 2 3 6 5 13 2 4 8 6 15 12 5 10 11 9 7 7 4 10 8 4 8
> 36
> output =242
>
> case =9
> input =9 9 7 4 5 14 3 18 10 13 14 8 6 10 19 8 17 8 15 3 19 13 10 4 2 1 5 17 9 2 20 13 5 5 19 3 14 18 8 10 13 3 8 19 10 17 3 20 20 1 11 14 3 14 15 4 17 15 10 11 3 10 14 7 13 6 9 20 11 4 18 5 3 12 16
> 43
> output =741
>
> case =10
> input =16 7 1 5 5 7 4 3 16 6 12 17 19 20 15 16 13 10 7 8 13 19 4 12 1 9 2 19 18 5 8 7 7 11 6 13 1 13 18 15 16 12 2 15 19 9 5 5 10 7 9 16 19 6 13 1 9 20 15 5 11 16 13 19 7 15 1 20 17 14 18 12 4 7 5 4 18 7 5 8 5 4 11 4 8 2 3 12 8 10 4 17 19 5 20 2 12 17 6 14
> 99
> output =921
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2047%20Solutions/BuyingShowTickets.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 47 Solutions/BuyingShowTickets.java
