---
kind: "coding-problem"
title: "Vaikuntapali (Day 49)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 49 Solutions/Vaikuntapali.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Vaikuntapali (Day 49)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Shakuni playing 'Paramapadasopanam' game with Dharamaraja.
Shakuni wants to win everytime. He has a boon that whenever he used to roll the dice,
the dice roll to show his desired number. 
You have to findout, what would be the least number of rolls required for shakuni to win.

Rules
--------
The game is played with a cubic die of 6 faces numbered 1 to 6.
- 	Starting from square 1, land on square 132 with the exact roll of the die. 
	If moving the number rolled would place the player beyond square 132, no move is made.
- 	If a player lands at the base of a ladder, the player must climb the ladder. Ladders go up only.
- 	If a player lands at the mouth of a snake, the player must go down the snake and come out through the tail. 
	Snakes go down only.

Function Description
Complete the quickestWayUp function in the editor below. It should return an integer that represents the minimum number of moves required.
quickestWayUp has the following parameter(s):
	ladders: a 2D integer array where each ladders[i] contains the start and end cell numbers of a ladder
	snakes: a 2D integer array where each  snakes[i] contains the start and end cell numbers of a snake

### Input Format

- The first line contains two integers n,m : n is the number of ladders and m is the number of snakes.
- Each of the next n lines contains two space-separated integers, the start and end of a ladder.
- Each of the next m lines contains two space-separated integers, the start and end of a snake.


### Output Format

- 	Print the least number of rolls to move from start to finish on a separate line. 


### Constraints

--------------
	1<= n,m<=15
	The board is always 12x11 with squares numbered  1 to 132.
	Neither square 1 nor square 132 will be the starting point of a ladder or snake.
	A square will have at most one endpoint from either a snake or a ladder.


Sample Input-1:
3 7
32 72
42 65
12 128
95 13
126 25
123 37
124 27
121 19
54 47
68 17
Sample Output-1: 3
Explanation-1:
The player can roll a 6 and a 6 to land at square 12. 
There is a ladder to square 128. A roll of 4 ends the traverse in 3 rolls.


Sample Input-2:
4 9
7 65
25 56
2 75
8 96
51 19
39 11
37 29
81 3
59 5
79 23
53 7
43 33
77 21 
Sample Output-2: 8
Explanation-2:
	Shakuni rolls to a 6 and then rolls to a 2 then climbs the ladder to square 96. 
	Six rolls of 6 get to the target square 132 in 8 total rolls.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Vaikuntapali.java
> ```java
> /*
> Shakuni playing 'Paramapadasopanam' game with Dharamaraja.
> Shakuni wants to win everytime. He has a boon that whenever he used to roll the dice,
> the dice roll to show his desired number. 
> You have to findout, what would be the least number of rolls required for shakuni to win.
>
> Rules
> --------
> The game is played with a cubic die of 6 faces numbered 1 to 6.
> - 	Starting from square 1, land on square 132 with the exact roll of the die. 
> 	If moving the number rolled would place the player beyond square 132, no move is made.
> - 	If a player lands at the base of a ladder, the player must climb the ladder. Ladders go up only.
> - 	If a player lands at the mouth of a snake, the player must go down the snake and come out through the tail. 
> 	Snakes go down only.
>
> Function Description
> Complete the quickestWayUp function in the editor below. It should return an integer that represents the minimum number of moves required.
> quickestWayUp has the following parameter(s):
> 	ladders: a 2D integer array where each ladders[i] contains the start and end cell numbers of a ladder
> 	snakes: a 2D integer array where each  snakes[i] contains the start and end cell numbers of a snake
> Input Format
> - The first line contains two integers n,m : n is the number of ladders and m is the number of snakes.
> - Each of the next n lines contains two space-separated integers, the start and end of a ladder.
> - Each of the next m lines contains two space-separated integers, the start and end of a snake.
>
> Output Format
> - 	Print the least number of rolls to move from start to finish on a separate line. 
>
> Constraints
> --------------
> 	1<= n,m<=15
> 	The board is always 12x11 with squares numbered  1 to 132.
> 	Neither square 1 nor square 132 will be the starting point of a ladder or snake.
> 	A square will have at most one endpoint from either a snake or a ladder.
>
>
> Sample Input-1:
> 3 7
> 32 72
> 42 65
> 12 128
> 95 13
> 126 25
> 123 37
> 124 27
> 121 19
> 54 47
> 68 17
> Sample Output-1: 3
> Explanation-1:
> The player can roll a 6 and a 6 to land at square 12. 
> There is a ladder to square 128. A roll of 4 ends the traverse in 3 rolls.
>
>
> Sample Input-2:
> 4 9
> 7 65
> 25 56
> 2 75
> 8 96
> 51 19
> 39 11
> 37 29
> 81 3
> 59 5
> 79 23
> 53 7
> 43 33
> 77 21 
> Sample Output-2: 8
> Explanation-2:
> 	Shakuni rolls to a 6 and then rolls to a 2 then climbs the ladder to square 96. 
> 	Six rolls of 6 get to the target square 132 in 8 total rolls.
>
> */
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.LinkedList;
>
>
> public class Vaikuntapali
> {
> 	public static void main (String[] args) throws IOException
> 	{
> 		InputStreamReader a = new InputStreamReader(System.in);
> 		BufferedReader buf = new BufferedReader(a);
> 		int[] move = new int[132];
> 		String[] tmp = buf.readLine().split(" ");
> 		int ladders = Integer.parseInt(tmp[0]);
> 		int snakes = Integer.parseInt(tmp[1]);
> 		for (int i=0; i<ladders; i++)
> 		{
> 			tmp = buf.readLine().split(" ");
> 			move[Integer.parseInt(tmp[0])-1] = Integer.parseInt(tmp[1]); 
> 		}
> 		
> 		for (int i=0; i<snakes; i++)
> 		{
> 			tmp = buf.readLine().split(" ");
> 			move[Integer.parseInt(tmp[0])-1] = Integer.parseInt(tmp[1]); 
> 		}
> 		
> 		int[] steps = new int[133];
> 		int[] visited = new int[132];
> 		LinkedList<Integer> wait = new LinkedList<Integer>();
> 		wait.add(0);
> 		while(true)
> 		{
> 			int curr = wait.pop();
> 			int next=0;
> 			int i;
> 			for(i=1; i<=6; i++)
> 			{
> 				next = curr+i;
> 				if(move[next-1]!=0)
> 					next = move[next-1];
> 				if(visited[next-1]!=1)
> 				{
> 					visited[next-1] = 1;
> 					wait.addLast(next);
> 					steps[next] = steps[curr]+1;
> 					if(next==132)
> 						break;
> 				}
> 			}
> 			if(next==132)
> 				break;
> 		}
> 		System.out.println(steps[132]);
> 	}
> }
>
>
> /*
> ====== Testcases Program-1 ======
> case =1
> input =3 7
> 32 72
> 42 65
> 12 128
> 95 13
> 126 25
> 123 37
> 124 27
> 121 19
> 54 47
> 68 17
> output =3
>
> case =2
> input =4 9
> 7 65
> 25 56
> 2 75
> 8 96
> 51 19
> 39 11
> 37 29
> 81 3
> 59 5
> 79 23
> 53 7
> 43 33
> 77 21 
> output =8
>
> case =3
> input =5 8
> 2 76				
> 3 56				
> 8 45				
> 14 67
> 28 89
> 45 12
> 56 14
> 67 2
> 76 8
> 89 3
> 124 4
> 125 7
> 126 9
> output =11
>
> case =4
> input =5 8
> 2 76
> 3 56
> 4 45
> 5 67
> 6 86
> 45 4
> 67 5
> 56 3
> 76 2
> 86 6
> 99 7
> 98 7
> 97 7
> output =9
>
> case =5
> input =6 6
> 2 46
> 3 56
> 4 66
> 5 76
> 6 86
> 7 96
> 46 2
> 56 3
> 66 4
> 76 5
> 86 6
> 96 7
> output =8
>
> case =6
> input =4 8
> 4 18
> 7 67
> 12 120
> 15 131
> 130 45
> 125 34
> 114 23
> 97 24
> 113 4
> 100 8
> 108 15
> 124 38
> output =4
>
> case =7
> input =8 5
> 4 78
> 8 93
> 12 65
> 18 84
> 24 123
> 35 79
> 44 90
> 54 59
> 58 13
> 74 18
> 95 34
> 121 23
> 130 2
> output =7
>
> case =8
> input =3 7
> 2 9
> 3 34
> 4 56
> 57 2
> 58 7
> 65 4
> 64 5
> 63 6
> 73 8
> 76 9
> output =14
>
> case =9
> input =5 8
> 7 44
> 12 78
> 17 89
> 22 112
> 27 126
> 98 15
> 78 34
> 65 45
> 116 21
> 123 34
> 128 43
> 130 21
> 131 48
> output =6
>
> case =10
> input =8 8
> 2 67
> 3 65
> 4 63
> 5 64
> 6 61
> 7 59
> 8 62
> 9 66
> 68 2
> 69 3
> 70 4
> 71 5
> 72 2
> 74 4
> 75 3
> 84 5
> output =12
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2049%20Solutions/Vaikuntapali.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 49 Solutions/Vaikuntapali.java
