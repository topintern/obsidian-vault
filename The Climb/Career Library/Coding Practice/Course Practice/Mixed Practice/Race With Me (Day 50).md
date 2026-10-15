---
kind: "coding-problem"
title: "Race With Me (Day 50)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 50 Solutions/RaceWithMe.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Race With Me (Day 50)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Abhinav is organizing a racing competation.N numbers of team (numbered as 1 to N) 
are participating in this race. 
Each team has M number of players. 
For each team M (team size) number of T-shirts are to be provided by the organizer. 
Each T-shirt contains a number(of that player) and may contain number of 
other player(s) of his own team.

At a time maximum P number of players(P≤M) can run in a ground.

Rules of race are following-
Each player takes 1 minute to complete his race.
Players(may be all) are dependent on some other players(the player(s)number written on his T-shirt) of his team.
A player can only start the race if player(s) number written on his T-shirt have finished their race.
Time taken by a team to complete the race is total time taken by players of team untill all have finished the race.
	Time may be infinite.
Team who will take minimum time will be winner.
Your task is to find winner team.

Input Format:
----------------
The first line of the input contains an integer N denoting the number of teams
The second line contains integer M denoting number of players of a team and 
D denoting sum of count of numbers written on T-shirt of each player(excluding his number). of a team.
The next D lines contain two integer A and B denoting B will finish only after A finished.
Repeat the steps 2 and 3 N times.

Output Format:
-------------------
Output a single integer in a separate line denoting the team number of winner team.
If all teams take infinite time to complete the race or in case of tie output "0"(without quote).


### Sample Input

2
4 3
1 3
3 2
4 2
3 3
1 2
1 3
2 1

### Sample Output

1


### Explanation:


For Team-1:
Firstly 1 and 4 finish their race simultaneously and take 1 minute, because they haven't need to wait for others.
Now 3 will finish his race in 1 minute.Since, only 2 is left ,he will finish his race in 1 minute.

Total no of time taken by Team-1 =1+1+1=3 minutes.

For Team-2:
3 and 2 will wait to finish 1,but 1 is also waiting for 2. In this situation no one can start race. Hence, 
Team-2 will take infinite time.

Team 1 will be winner.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · RaceWithMe.java
> ```java
> /*
> Abhinav is organizing a racing competation.N numbers of team (numbered as 1 to N) 
> are participating in this race. 
> Each team has M number of players. 
> For each team M (team size) number of T-shirts are to be provided by the organizer. 
> Each T-shirt contains a number(of that player) and may contain number of 
> other player(s) of his own team.
>
> At a time maximum P number of players(P≤M) can run in a ground.
>
> Rules of race are following-
> * Each player takes 1 minute to complete his race.
> * Players(may be all) are dependent on some other players(the player(s)number written on his T-shirt) of his team.
> * A player can only start the race if player(s) number written on his T-shirt have finished their race.
> * Time taken by a team to complete the race is total time taken by players of team untill all have finished the race.
> 	Time may be infinite.
> * Team who will take minimum time will be winner.
> * Your task is to find winner team.
>
> Input Format:
> ----------------
> * The first line of the input contains an integer N denoting the number of teams
> * The second line contains integer M denoting number of players of a team and 
> D denoting sum of count of numbers written on T-shirt of each player(excluding his number). of a team.
> * The next D lines contain two integer A and B denoting B will finish only after A finished.
> * Repeat the steps 2 and 3 N times.
>
> Output Format:
> -------------------
> Output a single integer in a separate line denoting the team number of winner team.
> If all teams take infinite time to complete the race or in case of tie output "0"(without quote).
>
> Sample Input:
> 2
> 4 3
> 1 3
> 3 2
> 4 2
> 3 3
> 1 2
> 1 3
> 2 1
> Sample Output:
> 1
>
> Explanation:
>
> For Team-1:
> Firstly 1 and 4 finish their race simultaneously and take 1 minute, because they haven't need to wait for others.
> Now 3 will finish his race in 1 minute.Since, only 2 is left ,he will finish his race in 1 minute.
>
> Total no of time taken by Team-1 =1+1+1=3 minutes.
>
> For Team-2:
> 3 and 2 will wait to finish 1,but 1 is also waiting for 2. In this situation no one can start race. Hence, 
> Team-2 will take infinite time.
>
> Team 1 will be winner.
>
>  */
> import java.util.*;
> import java.util.ArrayList;
> import java.util.Scanner;
>
> public class RaceWithMe {
>
> 	static class Node {
> 		boolean flag;
> 		int id;
> 		int od;
> 		ArrayList<Integer> adjNodes;
> 	}
>
> 	public static void main(String args[]) {
>
> 		int numOfTeams, numOfPlayers, d;
> 		// D denoting sum of count of numbers written on T-shirt of each
> 		// player(excluding his number). of a team.
>
> 		Scanner sc = new Scanner(System.in);
> 		numOfTeams = sc.nextInt();
> 		int a, b;
>
> 		List<Integer> run = new ArrayList<Integer>(Collections.nCopies(numOfTeams, Integer.MAX_VALUE));
>
> 		for (int i = 0; i < numOfTeams; i++) {
>
> 			numOfPlayers = sc.nextInt();
> 			d = sc.nextInt();
> 			List<Node> allNodes = new ArrayList<Node>();
>
> 			// Initializing all the nodes
> 			for (int j = 0; j < numOfPlayers; j++) {
> 				Node n = new Node();
> 				n.flag = false;
> 				n.od = n.id = 0;
> 				n.adjNodes = new ArrayList<Integer>();
> 				allNodes.add(j, n);
> 			}
>
> 			
> 			for (int j = 0; j < d; j++) {
> 				a = sc.nextInt() - 1;
> 				b = sc.nextInt() - 1;
>
> 				allNodes.get(a).od++;// add outdegree
> 				allNodes.get(b).id++;// add indegree
>
> 				// add adjacent node
> 				Node p = new Node();
> 				p = allNodes.get(a);
> 				p.adjNodes.add(b);
> 				allNodes.set(a, p);
>
> 			}
>
> 			int time = 0;
> 			boolean ok;
> 			while (true) {
> 				ok = true;
> 				List<Integer> save = new ArrayList<>();// saving adjacent nodes
> 				for (int j = 0; j < allNodes.size(); j++) {
>
> 					// not started the race and no need to wait for any one(because indegree is 0)
> 					if (allNodes.get(j).flag == false && allNodes.get(j).id == 0) {
> 						allNodes.get(j).flag = true;
> 						for (int k = 0; k < allNodes.get(j).adjNodes.size(); k++)
> 							save.add(allNodes.get(j).adjNodes.get(k));
> 						ok = false;// still some players didn't finish the race
> 					}
> 				}
> 				// The player(who has indegree 0) has finished the race just now.So,removing
> 				// dependencies of the player
> 				for (int j = 0; j < save.size(); j++)
> 					allNodes.get(save.get(j)).id--;
>
> 				boolean ch = false;// players could finish the race in "time" minutes
> 				if (ok == true) {
> 					for (int j = 0; j < allNodes.size(); j++) {
> 						if (allNodes.get(j).flag == false)
> 							ch = true;
> 					}
> 					if (ch == false)
> 						run.set(i, time);
> 					break;
> 				} else
> 					time++;
> 			} // end of while
>
> 		} // end of each team
>
> 		//System.out.println(run.toString());
> 		if (!run.isEmpty()) {
>
> 			int minValue = Collections.min(run);
> 			int minIndex = run.indexOf(minValue);
>
> 			int count = Collections.frequency(run, minValue);
>
> 			if (count == 1)// only one winner
> 				System.out.println(minIndex + 1);
> 			else // if more than one winner
> 				System.out.println("0");
>
> 		} else {
> 			System.out.println("0");
> 		}
>
> 	}// end of main
> }// end of class
>
>
> /*
> ========= Testcases Program-4 =========
> case =1
> input =2
> 5 4
> 1 3
> 4 2
> 3 2
> 2 5
> 5 5
> 1 2
> 1 3
> 2 4
> 3 4
> 3 5
> output =2
>
> case =2
> input =2
> 5 5
> 1 2
> 1 3
> 2 4
> 3 4
> 3 5
> 9 10
> 1 2
> 1 3
> 1 7
> 2 4
> 3 4
> 3 5
> 7 8
> 8 9
> 9 6
> 6 5
> output =1
>
> case =3
> input =3
> 5 4
> 1 3
> 4 2
> 3 2
> 2 5
> 9 10
> 1 2
> 1 3
> 1 7
> 2 4
> 3 4
> 3 5
> 7 8
> 8 9
> 9 6
> 6 5
> 5 5
> 1 2
> 1 3
> 2 4
> 3 4
> 3 5
> output =3
>
> case =4
> input =2
> 4 3
> 1 3
> 4 2
> 3 2
> 5 5
> 1 2
> 1 3
> 2 4
> 3 4
> 3 5
> output =0
>
> case =5
> input =2
> 4 3
> 1 3
> 3 2
> 4 2
> 3 3
> 1 2
> 1 3
> 2 1
> output =1
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2050%20Solutions/RaceWithMe.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 50 Solutions/RaceWithMe.java
