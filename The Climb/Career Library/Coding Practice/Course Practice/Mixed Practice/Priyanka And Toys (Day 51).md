---
kind: "coding-problem"
title: "Priyanka And Toys (Day 51)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 51 Solutions/PriyankaAndToys.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Priyanka And Toys (Day 51)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Priyanka works for an international toy company that ships by container. 
Her task is to the determine the lowest cost way to combine her orders for shipping. 
She has a list of item weights. 
The shipping company has a requirement that all items loaded in a container must weigh less than 
or equal to 4 units plus the weight of the minimum weight item. 
All items meeting that requirement will be shipped in one container.

What is the smallest number of containers that can be contracted to ship the items based on the given list of weights?

For example, there are items with weights w=[1,2,3,4,5,11,12,13]. 
This can be broken into two containers:[1,2,3,4,5] and [10,11,12,13]. 
Each container will contain items weighing within 4 units of the minimum weight item. 


### Input Format

-------------
The first line contains an integer n, the number of orders to ship.
The next line contains n space-separated integers,w[1],w[2],...w[n] , representing the orders in a weight array.


### Output Format

-------------
Print the integer value of the number of containers Priyanka must contract to ship all of the toys. 

Sample Input
------------
8
1 2 3 21 7 12 14 25

Sample Output
-------------
4

Explanation
-----------
The first container holds items weighing 1, 2 and 3. (weights in range 1...5)
The second container holds the items weighing 21 units. (21...25)
The third container holds the item weighing 7 units. (7...11)
The fourth container holds the items weighing 12 and 14 units. (12 ..14)

4 containers are required.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · PriyankaAndToys.java
> ```java
> /*
>  * 
> Priyanka works for an international toy company that ships by container. 
> Her task is to the determine the lowest cost way to combine her orders for shipping. 
> She has a list of item weights. 
> The shipping company has a requirement that all items loaded in a container must weigh less than 
> or equal to 4 units plus the weight of the minimum weight item. 
> All items meeting that requirement will be shipped in one container.
>
> What is the smallest number of containers that can be contracted to ship the items based on the given list of weights?
>
> For example, there are items with weights w=[1,2,3,4,5,11,12,13]. 
> This can be broken into two containers:[1,2,3,4,5] and [10,11,12,13]. 
> Each container will contain items weighing within 4 units of the minimum weight item. 
>
> Input Format
> -------------
> The first line contains an integer n, the number of orders to ship.
> The next line contains n space-separated integers,w[1],w[2],...w[n] , representing the orders in a weight array.
>
> Output Format
> -------------
> Print the integer value of the number of containers Priyanka must contract to ship all of the toys. 
>
> Sample Input
> ------------
> 8
> 1 2 3 21 7 12 14 25
>
> Sample Output
> -------------
> 4
>
> Explanation
> -----------
> The first container holds items weighing 1, 2 and 3. (weights in range 1...5)
> The second container holds the items weighing 21 units. (21...25)
> The third container holds the item weighing 7 units. (7...11)
> The fourth container holds the items weighing 12 and 14 units. (12 ..14)
>
> 4 containers are required.
>
>  * 
>  */
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
> import java.util.StringTokenizer;
>
> public class PriyankaAndToys {
>
> 	public static void main(String[] args) throws NumberFormatException, IOException {
> 		BufferedReader bfr = new BufferedReader(new InputStreamReader(System.in));
> 		final int N = Integer.parseInt(bfr.readLine());
>
> 		String line = bfr.readLine();
> 		StringTokenizer st = new StringTokenizer(line);
>
> 		int[] array = new int[N];
> 		for (int i = 0; i < N; ++i) {
> 			array[i] = Integer.parseInt(st.nextToken());
> 		}
> 		System.out.println(minContainers(array));
> 	}
>
> 	private static int minContainers(int[] array) {
> 		Arrays.sort(array);
> 		int selectedWeight = array[0];
> 		int cost = 1;
> 		for (int i = 1; i < array.length; ++i) {
> 			if (array[i] > selectedWeight + 4) {
> 				cost++;
> 				selectedWeight = array[i];
> 			}
> 		}
> 		return cost;
> 	}
>
> }
>
> /*
> ====== testcases program-4 ======
> case=1
> input=13
> 2 5 6 15 14 12 11 27 24 28 22 21 23
> output=4
>
> case=2
> input=10
> 2 5 14 12 11 27 24 23 30 35
> output=5
>
> case=3
> input=6
> 2 6 10 12 9 14
> output=3
>
> case=4
> input=5
> 2 6 10 12 9
> output=2
>
> case=5
> input=4
> 10 9 11 8
> output=1
>
> case=6
> input=6
> 4 7 2 9 10 13
> output=3
>
> case=7
> input=8
> 2 6 10 4 3 1 12 9
> output=3
>
> case=8
> input=8
> 10 9 11 8 7 12 15 14 
> output=2
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2051%20Solutions/PriyankaAndToys.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 51 Solutions/PriyankaAndToys.java
