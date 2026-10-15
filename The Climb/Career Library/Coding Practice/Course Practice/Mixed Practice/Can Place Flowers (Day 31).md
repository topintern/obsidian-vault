---
kind: "coding-problem"
title: "Can Place Flowers (Day 31)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 31 Solutions/CanPlaceFlowers.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Can Place Flowers (Day 31)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Suppose you have a long flowerbed in which some of the plots are planted and some are not. However, flowers cannot be planted in adjacent plots - they would compete for water and both would die.

Given a flowerbed (represented as an array containing 0 and 1, where 0 means empty and 1 means not empty), and a number n, return if n new flowers can be planted in it without violating the no-adjacent-flowers rule.

Example 1:

Input:1 0 0 0 1
1
Output: True


Input:1 0 0 0 1
2
Output: False


Note:
The input array won't violate no-adjacent-flowers rule.
The input array size is in the range of [1, 20000].
n is a non-negative integer which won't exceed the input array size.

case =1
input =1 0 0 0 0 0 1 0 1 0 0 1 0 1
2
output =true

case =2
input =0 0 1 0 0 0 0 0 1 0 1 0 0 1 0 1
3
output =true

case =3
input =0 0 1 0 0 0 0 0 1 0 1 0 0 0 1 0 1 0 0 0 0 0 1 0 1 
6
output =true

case =4
input =0 0 1 0 0 0 0 0 1 0 1 0 0 0 1 0 1 0 0 0 0 0 1 0 1 
7
output =false

case =5
input =0 0 1 0 0 0 0 0 1 0 1 0 0 1 0 1 0 0 0 1 0 
5
output =false

case =6
input =0 1 0 0 1 0 0 1 0 0 1 0 0
2
output =false

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · CanPlaceFlowers.java
> ```java
> /*
>  * 
>  Suppose you have a long flowerbed in which some of the plots are planted and some are not. However, flowers cannot be planted in adjacent plots - they would compete for water and both would die.
>
> Given a flowerbed (represented as an array containing 0 and 1, where 0 means empty and 1 means not empty), and a number n, return if n new flowers can be planted in it without violating the no-adjacent-flowers rule.
>
> Example 1:
>
> Input:1 0 0 0 1
> 1
> Output: True
>
>
> Input:1 0 0 0 1
> 2
> Output: False
>
>
> Note:
> The input array won't violate no-adjacent-flowers rule.
> The input array size is in the range of [1, 20000].
> n is a non-negative integer which won't exceed the input array size.
>
> case =1
> input =1 0 0 0 0 0 1 0 1 0 0 1 0 1
> 2
> output =true
>
> case =2
> input =0 0 1 0 0 0 0 0 1 0 1 0 0 1 0 1
> 3
> output =true
>
> case =3
> input =0 0 1 0 0 0 0 0 1 0 1 0 0 0 1 0 1 0 0 0 0 0 1 0 1 
> 6
> output =true
>
> case =4
> input =0 0 1 0 0 0 0 0 1 0 1 0 0 0 1 0 1 0 0 0 0 0 1 0 1 
> 7
> output =false
>
> case =5
> input =0 0 1 0 0 0 0 0 1 0 1 0 0 1 0 1 0 0 0 1 0 
> 5
> output =false
>
> case =6
> input =0 1 0 0 1 0 0 1 0 0 1 0 0
> 2
> output =false
>
>
>  */
>
> package Elite2020;
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class CanPlaceFlowers {
>
> 	  public static boolean canPlaceFlowers(int[] flowerbed, int n) {
> 	        int i = 0, count = 0;
> 	        while (i < flowerbed.length) {
> 	            if (flowerbed[i] == 0 && (i == 0 || flowerbed[i - 1] == 0) && 
> 	            		(i == flowerbed.length - 1 || flowerbed[i + 1] == 0)) {
> 	                flowerbed[i++] = 1;
> 	                count++;
> 	            }
> 	             if(count>=n)
> 	                return true;
> 	            i++;
> 	        }
> 	        return false;
> 	    }
> 	  
> 	  public static void main(String args[] ) throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 			String str = br.readLine();
> 			String[] numbers = str.split(" ");
> 			int[] arr = Arrays.asList(numbers).stream().mapToInt(Integer::parseInt).toArray();
> 			int k =Integer.parseInt(br.readLine());
> 			System.out.println(canPlaceFlowers(arr,k));
> 		}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2031%20Solutions/CanPlaceFlowers.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 31 Solutions/CanPlaceFlowers.java
