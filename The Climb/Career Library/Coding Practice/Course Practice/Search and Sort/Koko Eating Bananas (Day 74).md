---
kind: "coding-problem"
title: "Koko Eating Bananas (Day 74)"
collection: "Course Practice"
topic: "Search and Sort"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 74 Solutions/KokoEatingBananas.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Koko Eating Bananas (Day 74)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Koko loves to eat bananas.  There are N piles of bananas, the i-th pile has piles[i] bananas.  
The guards have gone and will come back in H hours.

Koko can decide her bananas-per-hour eating speed of K.  
Each hour, she chooses some pile of bananas, and eats K bananas from that pile.  
If the pile has less than K bananas, she eats all of them instead, and won't eat any more bananas during this hour.

Koko likes to eat slowly, but still wants to finish eating all the bananas before the guards come back.

Return the minimum integer K such that she can eat all the bananas within H hours.



### Sample Input: 

3 6 7 11
8

Output: 
4


### Explanation:


let take K = 3, Koko can finish eating all the bananas (within 8 hours) with an eating speed of 3.
we have total 27 bananas. if she start eating 3/hr . he can eat only 24 bananas in 8 hours.

let take K = 4, she can finish eating all the bananas (within 8 hours) with an eating speed of 4.

 let take K = 5, she can finish eating all the bananas (within 6 hours) with an eating speed of 5. 
 But we need to find minimum value of K such that she can eat all the bananas.
 So, the answer is 4.


--------Testcases Prog-1----------
case =1
input =3 6 7 11
8
output =4

case =2
input =6 9 12 13
7
output =7

case =3
input =9 5 7 3 12 8
10
output =6

case =4
input =12 65 43 37 85 73 92 56
35
output =15

case =5
input =9 3 8 6 4 5 7
16
output =3

case =6
input =11 15 18 17 12 14 13 19 16
20
output =9

case =7
input =23 17 18 15 16 26 27
15
output =13

case =8
input =8 5 6 4 9 5 3 7 8 10 12 16 15 18 19 13
23
output =10

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · KokoEatingBananas.txt
> ```java
> /*
>  * 
>
> Koko loves to eat bananas.  There are N piles of bananas, the i-th pile has piles[i] bananas.  
> The guards have gone and will come back in H hours.
>
> Koko can decide her bananas-per-hour eating speed of K.  
> Each hour, she chooses some pile of bananas, and eats K bananas from that pile.  
> If the pile has less than K bananas, she eats all of them instead, and won't eat any more bananas during this hour.
>
> Koko likes to eat slowly, but still wants to finish eating all the bananas before the guards come back.
>
> Return the minimum integer K such that she can eat all the bananas within H hours.
>
>
> Sample Input: 
> 3 6 7 11
> 8
>
> Output: 
> 4
>
> Explanation:
>
> let take K = 3, Koko can finish eating all the bananas (within 8 hours) with an eating speed of 3.
> we have total 27 bananas. if she start eating 3/hr . he can eat only 24 bananas in 8 hours.
>
> let take K = 4, she can finish eating all the bananas (within 8 hours) with an eating speed of 4.
>
>  let take K = 5, she can finish eating all the bananas (within 6 hours) with an eating speed of 5. 
>  But we need to find minimum value of K such that she can eat all the bananas.
>  So, the answer is 4.
>
>
> --------Testcases Prog-1----------
> case =1
> input =3 6 7 11
> 8
> output =4
>
> case =2
> input =6 9 12 13
> 7
> output =7
>
> case =3
> input =9 5 7 3 12 8
> 10
> output =6
>
> case =4
> input =12 65 43 37 85 73 92 56
> 35
> output =15
>
> case =5
> input =9 3 8 6 4 5 7
> 16
> output =3
>
> case =6
> input =11 15 18 17 12 14 13 19 16
> 20
> output =9
>
> case =7
> input =23 17 18 15 16 26 27
> 15
> output =13
>
> case =8
> input =8 5 6 4 9 5 3 7 8 10 12 16 15 18 19 13
> 23
> output =10
>
>  * 
>  */
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class KokoEatingBananas {
>
> 	/*
> 	 * 
> 	 * If Koko can finish eating all the bananas (within H hours) with an eating
> 	 * speed of K, she can finish with a larger speed too.
> 	 * 
> 	 * If we let possible(K) be true if and only if Koko can finish with an eating
> 	 * speed of K, then there is some X such that possible(K) = True if and only if
> 	 * K >= X.
> 	 * 
> 	 * For example, with piles = [3, 6, 7, 11] and H = 8, there is some X = 4 so
> 	 * that possible(1) = possible(2) = possible(3) = False, and possible(4) =
> 	 * possible(5) = ... = True
> 	 * 
> 	 * We can binary search on the values of possible(K) to find the first X such
> 	 * that possible(X) is True: that will be our answer.
> 	 */
> 	public static int minEatingSpeed(int[] piles, int H) {
> 		int lo = 1;
> 		int hi = Arrays.stream(piles).sum();
> 		//
> 		while (lo < hi) {
> 			int mi = (lo + hi) / 2;
> 			if (!possible(piles, H, mi))
> 				lo = mi + 1;
> 			else
> 				hi = mi;
> 		}
>
> 		return lo;
> 	}
>
> 	// Can Koko eat all bananas in H hours with eating speed K?
> 	public static boolean possible(int[] piles, int H, int K) {
> 		int time = 0;
> 		for (int p : piles)
> 			time += (p - 1) / K + 1;
> 		return time <= H;
> 	}
>
> 	public static void main(String args[]) throws IOException {
>
> 		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 		String str = br.readLine();
> 		String[] numbers = str.split(" ");
> 		int[] piles = Arrays.asList(numbers).stream().mapToInt(Integer::parseInt).toArray();
> 		int hours = Integer.parseInt(br.readLine());
> 		System.out.println(minEatingSpeed(piles, hours));
> 	}
>
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2074%20Solutions/KokoEatingBananas.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 74 Solutions/KokoEatingBananas.txt
