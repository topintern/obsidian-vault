---
kind: "coding-problem"
title: "Selling Photo Frames (Day 48)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 48 Solutions/SellingPhotoFrames.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Selling Photo Frames (Day 48)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Selling Photo Frames

Shakuni, a self-employed photo frame maker, has started his business. In short time, he
became popular as the frames were quite good and more importantly the prices were
reasonable. Now that the business is on track, Shakuni, in order to make more money, has
devised a cunning formula for the prices. According to the new formula, in a given transaction,
per customer, the price of a frame shall be equal to its current price * (number of frames
purchased previously + 1).

Bheem and his friends wanted to purchase some photo frames. After knowing the pricing
formula of Sakuni to maximize the cost of frames, he is looking for someone to help him with
an idea that gives the minimum cost and buy the required number of photo frames for him and
his friends.

Given, the total number of Frames (F), the number of friends (N) and the price list of all frames,
write a program to find the minimum total cost that Bheem must pay to purchase F number of
frames from Shakuni.


### Input

3 2
2 5 6


### Output

15

Comments

The first line 3 2 – Total Frames (F=3) and Friends(N=2)
Second line 2 5 6 – Prices of Frames


### Explanation

First person
o purchases Frame of 5 so its cost is
(0+1)*5 = 5
o Purchases Frame of 2 so its cost is
(1+1)*2 = 4

Second Person
o Purchases Frame of 6 so its cost is
(0+1)*6 = 6

Total Cost of Frames = 5 + 4 + 6 = 15

answer will be same for
input:
3 2
5 6 2
also.

Approach:
---------
Strategy: Each person should buy most expensive frame available and continue doing so until none are left

read the price of frames in a list.
sort price list in decending order.
initialise moneySpent variable to zero.
for each frame,
repeat till end of the frames
calculate costMultiplier(= framePriceIndex/N + 1)
multiply the currentPrice of frame with costMultiplier and add to moneySpent
end repeat
display moneySpent

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SellingPhotoFrames.java
> ```java
> /*
>  * 
> Selling Photo Frames
>
> Shakuni, a self-employed photo frame maker, has started his business. In short time, he
> became popular as the frames were quite good and more importantly the prices were
> reasonable. Now that the business is on track, Shakuni, in order to make more money, has
> devised a cunning formula for the prices. According to the new formula, in a given transaction,
> per customer, the price of a frame shall be equal to its current price * (number of frames
> purchased previously + 1).
>
> Bheem and his friends wanted to purchase some photo frames. After knowing the pricing
> formula of Sakuni to maximize the cost of frames, he is looking for someone to help him with
> an idea that gives the minimum cost and buy the required number of photo frames for him and
> his friends.
>
> Given, the total number of Frames (F), the number of friends (N) and the price list of all frames,
> write a program to find the minimum total cost that Bheem must pay to purchase F number of
> frames from Shakuni.
>
> Input
> 3 2
> 2 5 6
>
> Output
> 15
>
> Comments
>
> The first line 3 2 – Total Frames (F=3) and Friends(N=2)
> Second line 2 5 6 – Prices of Frames
>
> Explanation:
> First person
> o purchases Frame of 5 so its cost is
> (0+1)*5 = 5
> o Purchases Frame of 2 so its cost is
> (1+1)*2 = 4
>
> Second Person
> o Purchases Frame of 6 so its cost is
> (0+1)*6 = 6
>
> Total Cost of Frames = 5 + 4 + 6 = 15
>
> answer will be same for
> input:
> 3 2
> 5 6 2
> also.
>
> Approach:
> ---------
> Strategy: Each person should buy most expensive frame available and continue doing so until none are left
>
> read the price of frames in a list.
> sort price list in decending order.
> initialise moneySpent variable to zero.
> for each frame,
> repeat till end of the frames
> calculate costMultiplier(= framePriceIndex/N + 1)
> multiply the currentPrice of frame with costMultiplier and add to moneySpent
> end repeat
> display moneySpent
>
>  * 
>  */
> import java.util.*;
>
> public class SellingPhotoFrames {
>
>     @SuppressWarnings("deprecation")
> 	public static void main(String[] args) {
>         
>         Scanner sc = new Scanner(System.in);
>         int framesCount = sc.nextInt();
>         int friendsCount = sc.nextInt();
>         
>         //read in all the frame prices
>         List<Integer> framesPrices = new ArrayList<Integer>();
>         for(int currFrame = 0; currFrame < framesCount; currFrame++){
>             framesPrices.add(new Integer(sc.nextInt()));
>         }
>         
>         /*
>         * Strategy: Each person should buy most expensive frame available and continue doing so until none are left
>         */
>         
>         //sort the frame prices so we always know which is the most expensive frame
>         Collections.sort(framesPrices,Collections.reverseOrder());
>         
>         int moneySpent = 0;
>        
>         //buy each frame, starting with the most expensive one first
>         for(int framePriceIndex = 0; framePriceIndex<framesCount; framePriceIndex++){
>         	int costMultiplier = (framePriceIndex / friendsCount) + 1;
>             moneySpent += framesPrices.get(framePriceIndex) * costMultiplier;
>         }
>         
>         System.out.println(moneySpent);
>     }
>     
> }
>
> /*
> =======Testcases=======
> case =1
> input =3 2
> 2 5 6
> output =15
>
> case =2
> input =4 2
> 5 3 2 6
> output =21
>
> case =3
> input =5 4
> 7 5 3 8 2
> output =
>
> case =4
> input =8 3
> 9 4 10 7 8 13 15 14
> output =129
>
> case =5
> input =10 3
> 9 8 10 13 24 5 17 6 3 11
> output =183
>
> case =6
> input =15 4
> 9 5 3 45 43 23 29 34 53 7 9 19 46 35 25
> output =673
>
> case =7
> input =10 10
> 1 8 9 10 4 5 2 3 6 7
> output =55
>
> case =8
> input =14 7
> 13 24 5 17 6 3 11 23 29 34 53 7 9 19
> output =307
>
> case =9
> input =14 4
> 13 24 5 17 6 3 11 23 29 34 53 7 9 19
> output =415
>
> case =10
> input =10 3
> 1 8 9 10 4 5 2 3 6 7
> output =94
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2048%20Solutions/SellingPhotoFrames.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 48 Solutions/SellingPhotoFrames.java
