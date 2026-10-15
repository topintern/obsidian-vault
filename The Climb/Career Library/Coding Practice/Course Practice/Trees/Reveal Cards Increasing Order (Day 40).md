---
kind: "coding-problem"
title: "Reveal Cards Increasing Order (Day 40)"
collection: "Course Practice"
topic: "Trees"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 40 Solutions/RevealCardsIncreasingOrder.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Reveal Cards Increasing Order (Day 40)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

In a deck of cards, every card has a unique integer.  You can order the deck in any order you want.

Initially, all the cards start face down (unrevealed) in one deck.

Now, you do the following steps repeatedly, until all cards are revealed:

Take the top card of the deck, reveal it, and take it out of the deck.
If there are still cards in the deck, put the next top card of the deck at the bottom of the deck.
If there are still unrevealed cards, go back to step 1.  Otherwise, stop.
Return an ordering of the deck that would reveal the cards in increasing order.

The first entry in the answer is considered to be the top of the deck.

 

Example 1:

Input: 28 24 22 13 14 16 18
Output: 13 24 14 22 16 28 18


### Explanation: 

We get the deck in the order [28,24,22,13,14,16,18] (this order doesn't matter), and reorder it.
After reordering, the deck starts as [13,24,14,22,16,28,18], where 13 is the top of the deck.
We reveal 13, and move 24 to the bottom.  Deck Now-> [14,22,16,28,18,24].
We reveal 14, and move 22 to the bottom.  Deck Now-> [16,28,18,24,22].
We reveal 16, and move 28 to the bottom.  Deck Now-> [18,24,22,28].
We reveal 18, and move 24 to the bottom.  Deck Now-> [22,28,24].
We reveal 22, and move 28 to the bottom.  Deck Now-> [24,28].
We reveal 24, and move 28 to the bottom.  Deck Now-> [28].
We reveal 28.
Since all the cards revealed are in increasing order, the answer is correct.


==================================================================================

Simulate the process with a queue.

Sort the deck, it is actually the "final sequence" we want to get according to the question.
Then put it back to the result array, we just need to deal with the index now!
Simulate the process with a queue (initialized with 0,1,2...(n-1)), now how do we pick the card?
We first pick the index at the top: res[q.poll()]=deck[i]
Then we put the next index to the bottom: q.add(q.poll());
Repeat it n times, and you will have the result array!
update


Let's walk through the example:
Input: [17,13,11,2,3,5,7]
Output: [2,13,3,11,5,17,7]

Sort the deck: [2,3,5,7,11,13,17], this is the increasing order we want to generate
Initialize the queue: [0,1,2,3,4,5,6], this is the index of the result array
The first card we pick is res[0], observe the deck, it should be deck[0]==2, so assign res[0]=2
Then we put res[1] to the bottom, so we re-insert 1 to the queue
The second card we pick is res[2], which should be deck[1]==3, so assign res[2]=3
Then we re-insert 3 to the queue
Each time we assign 1 value to the res, so we repeat this n times.

=============================================================================================

case=1
input=17 13 11 2 3 5 7
output=2 13 3 11 5 17 7

case=2
input=1 2 3 4 5 6 7 8 9
output=[1, 9, 2, 6, 3, 8, 4, 7, 5]

case=3
input=3 2 1 4 5 6 9 8 7 1 5 9  
output=[1, 5, 1, 8, 2, 6, 3, 9, 4, 7, 5, 9]

case=4
input=15 18 19 20 25 26 14 17 13 23 2 4 6 88 91
output=[2, 25, 4, 19, 6, 88, 13, 20, 14, 26, 15, 23, 17, 91, 18]

case=5
input=10 20 25 30 11 22 23 24 35 36 37 48 9
output=[9, 37, 10, 25, 11, 36, 20, 30, 22, 48, 23, 35, 24]

case=6
input=30 20 10 15 16 14 18 19 24 26 31 5 4 2 1 7 9  
output=[1, 31, 2, 16, 4, 24, 5, 18, 7, 30, 9, 19, 10, 26, 14, 20, 15]

case=7
input=2 13 3 11 5 17 7
output=2 13 3 11 5 17 7

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · RevealCardsIncreasingOrder.java
> ```java
> /*
>  In a deck of cards, every card has a unique integer.  You can order the deck in any order you want.
>
> Initially, all the cards start face down (unrevealed) in one deck.
>
> Now, you do the following steps repeatedly, until all cards are revealed:
>
> Take the top card of the deck, reveal it, and take it out of the deck.
> If there are still cards in the deck, put the next top card of the deck at the bottom of the deck.
> If there are still unrevealed cards, go back to step 1.  Otherwise, stop.
> Return an ordering of the deck that would reveal the cards in increasing order.
>
> The first entry in the answer is considered to be the top of the deck.
>
>  
>
> Example 1:
>
> Input: 28 24 22 13 14 16 18
> Output: 13 24 14 22 16 28 18
>
> Explanation: 
> We get the deck in the order [28,24,22,13,14,16,18] (this order doesn't matter), and reorder it.
> After reordering, the deck starts as [13,24,14,22,16,28,18], where 13 is the top of the deck.
> We reveal 13, and move 24 to the bottom.  Deck Now-> [14,22,16,28,18,24].
> We reveal 14, and move 22 to the bottom.  Deck Now-> [16,28,18,24,22].
> We reveal 16, and move 28 to the bottom.  Deck Now-> [18,24,22,28].
> We reveal 18, and move 24 to the bottom.  Deck Now-> [22,28,24].
> We reveal 22, and move 28 to the bottom.  Deck Now-> [24,28].
> We reveal 24, and move 28 to the bottom.  Deck Now-> [28].
> We reveal 28.
> Since all the cards revealed are in increasing order, the answer is correct.
>
>
> ==================================================================================
>
> Simulate the process with a queue.
>
> Sort the deck, it is actually the "final sequence" we want to get according to the question.
> Then put it back to the result array, we just need to deal with the index now!
> Simulate the process with a queue (initialized with 0,1,2...(n-1)), now how do we pick the card?
> We first pick the index at the top: res[q.poll()]=deck[i]
> Then we put the next index to the bottom: q.add(q.poll());
> Repeat it n times, and you will have the result array!
> update
>
>
> Let's walk through the example:
> Input: [17,13,11,2,3,5,7]
> Output: [2,13,3,11,5,17,7]
>
> Sort the deck: [2,3,5,7,11,13,17], this is the increasing order we want to generate
> Initialize the queue: [0,1,2,3,4,5,6], this is the index of the result array
> The first card we pick is res[0], observe the deck, it should be deck[0]==2, so assign res[0]=2
> Then we put res[1] to the bottom, so we re-insert 1 to the queue
> The second card we pick is res[2], which should be deck[1]==3, so assign res[2]=3
> Then we re-insert 3 to the queue
> Each time we assign 1 value to the res, so we repeat this n times.
>
> =============================================================================================
>
> case=1
> input=17 13 11 2 3 5 7
> output=2 13 3 11 5 17 7
>
> case=2
> input=1 2 3 4 5 6 7 8 9
> output=[1, 9, 2, 6, 3, 8, 4, 7, 5]
>
> case=3
> input=3 2 1 4 5 6 9 8 7 1 5 9  
> output=[1, 5, 1, 8, 2, 6, 3, 9, 4, 7, 5, 9]
>
> case=4
> input=15 18 19 20 25 26 14 17 13 23 2 4 6 88 91
> output=[2, 25, 4, 19, 6, 88, 13, 20, 14, 26, 15, 23, 17, 91, 18]
>
> case=5
> input=10 20 25 30 11 22 23 24 35 36 37 48 9
> output=[9, 37, 10, 25, 11, 36, 20, 30, 22, 48, 23, 35, 24]
>
> case=6
> input=30 20 10 15 16 14 18 19 24 26 31 5 4 2 1 7 9  
> output=[1, 31, 2, 16, 4, 24, 5, 18, 7, 30, 9, 19, 10, 26, 14, 20, 15]
>
> case=7
> input=2 13 3 11 5 17 7
> output=2 13 3 11 5 17 7 
>  
>  */
>
>
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.*;
>
> public class RevealCardsIncreasingOrder {
>
> 	  public static int[] deckRevealedIncreasing(int[] deck) {
> 	        int n= deck.length;
> 	        Arrays.sort(deck);
> 	        Queue<Integer> q= new LinkedList<>();
> 	        for (int i=0; i<n; i++) q.add(i);
> 	        int[] res= new int[n];
> 	        for (int i=0; i<n; i++){
> 	            res[q.poll()]=deck[i];
> 	            q.add(q.poll());
> 	        }
> 	        return res;
> 	    }
> 	  public static void main(String args[] ) throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 			String str = br.readLine();
> 			
> 			String[] stockpriceline = str.split(" ");
> 			int[] deck = Arrays.asList(stockpriceline).stream().mapToInt(Integer::parseInt).toArray();
> 			
> 			System.out.println(Arrays.toString(deckRevealedIncreasing(deck)));   
> 			
> 			}
> 	  
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2040%20Solutions/RevealCardsIncreasingOrder.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 40 Solutions/RevealCardsIncreasingOrder.java
