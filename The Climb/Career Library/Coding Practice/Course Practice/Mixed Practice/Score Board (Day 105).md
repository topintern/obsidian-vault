---
kind: "coding-problem"
title: "Score Board (Day 105)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 105 Solutions/ScoreBoard.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Score Board (Day 105)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You are asked to design the Tessellator scoring list. 
The class is TessellatorScore. 
The member functions are updatescore(studentid,score) 
    (if the student does not exist the student should be created in the scoring list 
    with score as his initial score). 

Once the students gets an offer , he/she should be deleted using delete(studentid). 

Before calling a company Sudheer Reddy – our placement officer wants to know 
the sum of scores of top k students. So we must provide him a method getsum(k) 
which returns the sum of of the scores of top k students.

Function calls:
===============
1. updatecore(int,int)
2. getsum(int)
3. delete(int)
0. stop the execution

Input Format:
-------------
There will be some lines of input, 
Each line will startwith function call option and followed by parameters list

Output Format:
--------------
Print an integer when top funtion called.


Sample Input-1:
---------------
1 1 73
1 2 56
1 3 39
1 4 51
1 5 4
2 1
3 1
3 2
1 2 51
2 3
0

Sample Output-1:
----------------
73   
141


### Explanation

------------
First line indicates 1 1 73, option 1 indicates updatescore(1,73) added to Score List.
After 5 lines of input, Score List will looks like
    1 73
    2 56
    3 39
    4 51
    5 4

Next Line 2 1: Option 2 indicates getsum(1) answer is 73.

Next 2 lines 3 1, 3 2 indicates delete 1,2 from the Score List, new Score List is
    3 39
    4 51
    5 4

Next line 1 2 51, option 1 -> update score and student id is 2 and score is 51
new Score List is:
    2 51
    3 39
    4 51
    5 4

Next line 2 3, Option 2 indicates getsum(3) answer is 141.

Next line 0, indicates stop the execution.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ScoreBoard.txt
> ```java
> /*
>
> You are asked to design the Tessellator scoring list. 
> The class is TessellatorScore. 
> The member functions are updatescore(studentid,score) 
>     (if the student does not exist the student should be created in the scoring list 
>     with score as his initial score). 
>
> Once the students gets an offer , he/she should be deleted using delete(studentid). 
>
> Before calling a company Sudheer Reddy – our placement officer wants to know 
> the sum of scores of top k students. So we must provide him a method getsum(k) 
> which returns the sum of of the scores of top k students.
>
> Function calls:
> ===============
> 1. updatecore(int,int)
> 2. getsum(int)
> 3. delete(int)
> 0. stop the execution
>
> Input Format:
> -------------
> There will be some lines of input, 
> Each line will startwith function call option and followed by parameters list
>
> Output Format:
> --------------
> Print an integer when top funtion called.
>
>
> Sample Input-1:
> ---------------
> 1 1 73
> 1 2 56
> 1 3 39
> 1 4 51
> 1 5 4
> 2 1
> 3 1
> 3 2
> 1 2 51
> 2 3
> 0
>
> Sample Output-1:
> ----------------
> 73   
> 141
>
> Explanation:
> ------------
> First line indicates 1 1 73, option 1 indicates updatescore(1,73) added to Score List.
> After 5 lines of input, Score List will looks like
>     1 73
>     2 56
>     3 39
>     4 51
>     5 4
>
> Next Line 2 1: Option 2 indicates getsum(1) answer is 73.
>
> Next 2 lines 3 1, 3 2 indicates delete 1,2 from the Score List, new Score List is
>     3 39
>     4 51
>     5 4
>
> Next line 1 2 51, option 1 -> update score and student id is 2 and score is 51
> new Score List is:
>     2 51
>     3 39
>     4 51
>     5 4
>
> Next line 2 3, Option 2 indicates getsum(3) answer is 141.
>
> Next line 0, indicates stop the execution.
>
> */
>
> import java.util.*;
>
> class TessellatorScore {
>     Map<Integer, Integer> map;
>     TreeMap<Integer, Integer> sorted;
>     public TessellatorScore() {
>         map = new HashMap<>();
>         sorted = new TreeMap<>(Collections.reverseOrder());
>     }
>     
>     public void updatescore(int playerId, int score) {
>         if (!map.containsKey(playerId)) {
>             map.put(playerId, score);
>             sorted.put(score, sorted.getOrDefault(score, 0) + 1);
>         } else {
>             int preScore = map.get(playerId);
>             sorted.put(preScore, sorted.get(preScore) - 1);
>             if (sorted.get(preScore) == 0) {
>                 sorted.remove(preScore);
>             }
>             int newScore = preScore + score;
>             map.put(playerId, newScore);
>             sorted.put(newScore, sorted.getOrDefault(newScore, 0) + 1);
>         }
>     }
>     
>     public int getsum(int K) {
>         int count = 0;
>         int sum = 0;
>         for (int key : sorted.keySet()) {
>             int times = sorted.get(key);
>             for (int i = 0; i < times; i++) {
>                 sum += key;
>                 count++;
>                 if (count == K) {
>                     break;
>                 }
>             }
>             if (count == K) {
>                 break;
>             }
>         }
>         return sum;
>     }
>     
>     public void delete(int playerId) {
>         int preScore = map.get(playerId);
>         sorted.put(preScore, sorted.get(preScore) - 1);
>         if (sorted.get(preScore) == 0) {
>             sorted.remove(preScore);
>         }
>         map.remove(playerId);
>     }	
> }
> class Solution{
> 	public static void main(String args[]){
> 		Scanner sc=new Scanner(System.in);
> 		TessellatorScore l=new TessellatorScore();
> 		int ch=sc.nextInt();
> 		do
> 		{
> 			switch(ch)
> 			{
> 				case 1: 
> 					l.updatescore(sc.nextInt(), sc.nextInt());
> 					break;
> 				case 2:
> 					System.out.println(l.getsum(sc.nextInt()));
> 					break;
> 				case 3:
> 					l.delete(sc.nextInt());
> 			}
> 			ch=sc.nextInt();
> 		}while(ch!=0);
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20105%20Solutions/ScoreBoard.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 105 Solutions/ScoreBoard.txt
