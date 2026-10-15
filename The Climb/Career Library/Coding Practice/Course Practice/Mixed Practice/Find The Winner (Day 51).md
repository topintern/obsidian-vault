---
kind: "coding-problem"
title: "Find The Winner (Day 51)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 51 Solutions/FindTheWinner.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Find The Winner (Day 51)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Andrea and Maria each have a deck of numbered cards in a pile face down. 
They play a game where they each alternately discard and flip the cards on the pile from top to bottom. 

At the beginning of the game, someone will call out “Even” or “Odd”. 
The first move depends on which is called. 
If “Even” is called, the players top cards are flipped so they can see the face value. 
If instead “Odd” is called, the top card is removed from each deck and discarded, 
then each flips her next card. 
Andrea subtracts the value of Maria’s card from her own and adds the result to her score. 
Likewise, Maria subtracts the value of Andrea’s card from her own and adds the result to her score. 

From this point forward, each alternately discards then flips a card. Each time two cards are flipped, the 
players scores are computed as before. Once all the cards have been played, whoever has the most points wins. 

As an example, Maria’s cards, face down are [3,5,6] and Andrea’s are [4,5,7]. 
After calling “Even” at random, they each compare their first cards. 
Maria’s points are 3-4 =-1, and Andrea’s are 4-3=1. 
They discard the 5’s and turn over their third cards. 
Maria receives 6-7=-1 point and Andrea receives 7-6=1 point. Maria’s score is -2, Andrea’s is +2 so Andrea wins. 

You must determine the name of the winner if there is one, otherwise they tie. Return Andrea,Maria or Tie. 

Input Format:
-------------
number of andrea cards
read all andrea cards
number of maria cards
read all maria cards
read the string either Odd or Even

Output Format:
--------------
Print a string denoting the outcome of the game. 
Print Andrea if Andrea won, or Print Maria if Maria won. If their scores are tied, Print Tie instead. 


### Sample Input

3
1
2
3
3
2
1
3
Even

Sample Output 
Maria

Explanation
In this game, andrea =[1,2,3] and maris=[2,1,3]. Because s=Even, the only cards flipped are at indexes 0 and 2. 

When i=0, Andrea gets a[0]-m[0]=1-2 =-1 point and Maria gets m[0]-a[0]=2-1 = 1 point.
When i=2, Andrea gets a[2]-m[2]=3-3=0 points and Maria gets m[2]-a[2]=3-3 = 0 points. 

At the end of play, Andrea’s cumulative score is -1 and Maria’s is 1 so Maria wins.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · FindTheWinner.java
> ```java
> /*
>  * 
> Andrea and Maria each have a deck of numbered cards in a pile face down. 
> They play a game where they each alternately discard and flip the cards on the pile from top to bottom. 
>
> At the beginning of the game, someone will call out “Even” or “Odd”. 
> The first move depends on which is called. 
> If “Even” is called, the players top cards are flipped so they can see the face value. 
> If instead “Odd” is called, the top card is removed from each deck and discarded, 
> then each flips her next card. 
> Andrea subtracts the value of Maria’s card from her own and adds the result to her score. 
> Likewise, Maria subtracts the value of Andrea’s card from her own and adds the result to her score. 
>
> From this point forward, each alternately discards then flips a card. Each time two cards are flipped, the 
> players scores are computed as before. Once all the cards have been played, whoever has the most points wins. 
>
> As an example, Maria’s cards, face down are [3,5,6] and Andrea’s are [4,5,7]. 
> After calling “Even” at random, they each compare their first cards. 
> Maria’s points are 3-4 =-1, and Andrea’s are 4-3=1. 
> They discard the 5’s and turn over their third cards. 
> Maria receives 6-7=-1 point and Andrea receives 7-6=1 point. Maria’s score is -2, Andrea’s is +2 so Andrea wins. 
>
> You must determine the name of the winner if there is one, otherwise they tie. Return Andrea,Maria or Tie. 
>
> Input Format:
> -------------
> number of andrea cards
> read all andrea cards
> number of maria cards
> read all maria cards
> read the string either Odd or Even
>
> Output Format:
> --------------
> Print a string denoting the outcome of the game. 
> Print Andrea if Andrea won, or Print Maria if Maria won. If their scores are tied, Print Tie instead. 
>
> Sample Input:
> 3
> 1
> 2
> 3
> 3
> 2
> 1
> 3
> Even
>
> Sample Output 
> Maria
>
> Explanation
> In this game, andrea =[1,2,3] and maris=[2,1,3]. Because s=Even, the only cards flipped are at indexes 0 and 2. 
>
> When i=0, Andrea gets a[0]-m[0]=1-2 =-1 point and Maria gets m[0]-a[0]=2-1 = 1 point.
> When i=2, Andrea gets a[2]-m[2]=3-3=0 points and Maria gets m[2]-a[2]=3-3 = 0 points. 
>
> At the end of play, Andrea’s cumulative score is -1 and Maria’s is 1 so Maria wins. 
>
>
>  * 
>  */
> import java.util.ArrayList;
> import java.util.Scanner;
>
> public class FindTheWinner {
>
> 	public static void main(String args[]) {
> 		Scanner sc = new Scanner(System.in);
> 		int numOfCardsA = sc.nextInt();
> 		ArrayList<Integer> andreaCards = new ArrayList<>();
> 		for (int i = 0; i < numOfCardsA; i++) {
> 			andreaCards.add(sc.nextInt());
> 		}
>
> 		int numOfCardsM = sc.nextInt();
>
> 		ArrayList<Integer> mariaCards = new ArrayList<>();
> 		for (int i = 0; i < numOfCardsM; i++) {
> 			mariaCards.add(sc.nextInt());
> 		}
> 		String s = sc.next();
> 		int andreaScore = 0, mariaScore = 0;
>
> 		switch (s) {
>
> 		case "Even":
> 			for (int i = 0; i < numOfCardsA; i++) {
> 				if (i % 2 == 0) {
> 					andreaScore += andreaCards.get(i) - mariaCards.get(i);
> 					mariaScore += mariaCards.get(i) - andreaCards.get(i);
> 				}
> 			}
> 			break;
> 		case "Odd":
> 			for (int i = 0; i < numOfCardsA; i++) {
> 				if (i % 2 != 0) {
> 					andreaScore += andreaCards.get(i) - mariaCards.get(i);
> 					mariaScore += mariaCards.get(i) - andreaCards.get(i);
> 				}
> 			}
> 			break;
> 		}// end of switch
> 		
> 		if (andreaScore > mariaScore) {
> 			System.out.println("Andrea");
> 		} else if (mariaScore > andreaScore) {
> 			System.out.println("Maria");
> 		} else {
> 			System.out.println("Tie");
> 		}
> 	}
> }
>
>
> /*
>
> ======= testcases program-3 =======
> case=1
> input=3
> 4 5 7
> 3
> 3 5 6
> Even
> output=Andrea
>
> case=2
> input=3
> 1 2 3
> 3
> 2 1 3
> Even
> output=Maria
>
> case=3
> input=3
> 3 15 6
> 3
> 3 5 6
> Even
> output=Tie
>
> case=4
> input=5
> 4 5 7 8 10
> 5
> 3 5 6 8 9
> Odd
> output=Tie
>
> case=5
> input=5
> 1 12 5 3 14
> 5
> 12 14 3 5 13
> Even
> output=Maria
>
> case=6
> input=4
> 3 15 6 5
> 4
> 3 4 5 6
> Even
> output=Andrea
>
> case=7
> input=3
> 4 5 7
> 3
> 3 5 6
> Odd
> output=Tie
>
> case=8
> input=3
> 1 2 3
> 3
> 2 1 3
> Odd
> output=Andrea
>
> case=9
> input=3
> 3 15 6
> 3
> 3 5 6
> Odd
> output=Andrea
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2051%20Solutions/FindTheWinner.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 51 Solutions/FindTheWinner.java
