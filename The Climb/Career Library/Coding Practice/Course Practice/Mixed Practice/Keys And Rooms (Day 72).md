---
kind: "coding-problem"
title: "Keys And Rooms (Day 72)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 72 Solutions/KeysAndRooms.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Keys And Rooms (Day 72)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

There are N rooms and you start in room 0.  
Each room has a distinct number in 0, 1, 2, ..., N-1, 
and each room may have some keys to access the next room. 

Formally, each room i has a list of keys rooms[i], and 
each key rooms[i][j] is an integer in [0, 1, ..., N-1] where N = rooms.length. 
A key rooms[i][j] = v opens the room with number v.

Initially, all the rooms start locked (except for room 0). 

You can walk back and forth between rooms freely.

Return true if and only if you can enter every room.

Note:

-> 1 <= rooms.length <= 1000
-> 0 <= rooms[i].length <= 1000
-> The number of keys in all rooms combined is at most 3000.


Sample Input 1: 
4
1
2
3
0
Sample Output 1: 
true


### Explanation:  

We start in room 0, and pick up key 1.
We then go to room 1, and pick up key 2.
We then go to room 2, and pick up key 3.
We then go to room 3.  Since we were able to go to every room, we return true.

Sample Input 2: 
4
1 3
3 0 1
2
0

Sample Output 2: 
false


### Explanation:  

We can't enter the room with number 2.

========= Testcases Program-3 =========
case =1
input =4
1
2
3
0
output ="true"

case =2
input =4
1 3
3 0 1
2
0
output ="false"

case =3
input =5                                                                                                                     
1                                                                                                              
2 3                                                                                                                
4 0                                                                                                                    
2 4                                                                                                                     
3
output ="true"

case =4
input =6                                                                                                            
0                                                                                                              
2 3                                                                                                                
4 0 5                                                                                                                  
2 4                                                                                                                     
3
1 4
output ="false"

case =6
input =12
11 1 2
10 3
9 
8
7
6 4 2 1
1
5
2 1 8 5 4 0
4
3
0
output ="true"

case =7
input =9
1
2
3
0
2 5
4 6 7
5 8
7
6 2 1
output ="false"

case =8
input =9
1
2
3
4
2 5
4 6 5
5 8
7
6 2 7
output ="true"

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · KeysAndRooms.java
> ```java
> /*
>  * 
> There are N rooms and you start in room 0.  
> Each room has a distinct number in 0, 1, 2, ..., N-1, 
> and each room may have some keys to access the next room. 
>
> Formally, each room i has a list of keys rooms[i], and 
> each key rooms[i][j] is an integer in [0, 1, ..., N-1] where N = rooms.length. 
> A key rooms[i][j] = v opens the room with number v.
>
> Initially, all the rooms start locked (except for room 0). 
>
> You can walk back and forth between rooms freely.
>
> Return true if and only if you can enter every room.
>
> Note:
>
> -> 1 <= rooms.length <= 1000
> -> 0 <= rooms[i].length <= 1000
> -> The number of keys in all rooms combined is at most 3000.
>
>
> Sample Input 1: 
> 4
> 1
> 2
> 3
> 0
> Sample Output 1: 
> true
>
> Explanation:  
> We start in room 0, and pick up key 1.
> We then go to room 1, and pick up key 2.
> We then go to room 2, and pick up key 3.
> We then go to room 3.  Since we were able to go to every room, we return true.
>
> Sample Input 2: 
> 4
> 1 3
> 3 0 1
> 2
> 0
>
> Sample Output 2: 
> false
>
> Explanation:  
> We can't enter the room with number 2.
>
> ========= Testcases Program-3 =========
> case =1
> input =4
> 1
> 2
> 3
> 0
> output ="true"
>
> case =2
> input =4
> 1 3
> 3 0 1
> 2
> 0
> output ="false"
>
> case =3
> input =5                                                                                                                     
> 1                                                                                                              
> 2 3                                                                                                                
> 4 0                                                                                                                    
> 2 4                                                                                                                     
> 3
> output ="true"
>
> case =4
> input =6                                                                                                            
> 0                                                                                                              
> 2 3                                                                                                                
> 4 0 5                                                                                                                  
> 2 4                                                                                                                     
> 3
> 1 4
> output ="false"
>
> case =6
> input =12
> 11 1 2
> 10 3
> 9 
> 8
> 7
> 6 4 2 1
> 1
> 5
> 2 1 8 5 4 0
> 4
> 3
> 0
> output ="true"
>
> case =7
> input =9
> 1
> 2
> 3
> 0
> 2 5
> 4 6 7
> 5 8
> 7
> 6 2 1
> output ="false"
>
> case =8
> input =9
> 1
> 2
> 3
> 4
> 2 5
> 4 6 5
> 5 8
> 7
> 6 2 7
> output ="true"
>
>  * 
>  * 
>  */
> import java.util.*;
>
> public class KeysAndRooms {
>
> 	/*
> 	 * When visiting a room for the first time, look at all the keys in that room.
> 	 * For any key that hasn't been used yet, add it to the todo list (stack) for it
> 	 * to be used.
> 	 */
> 	public static boolean canVisitAllRooms(List<List<Integer>> rooms) {
> 		boolean[] seen = new boolean[rooms.size()];
> 		seen[0] = true;
> 		Stack<Integer> stack = new Stack();
> 		stack.push(0);
>
> 		// At the beginning, we have a todo list "stack" of keys to use.
> 		// 'seen' represents at some point we have entered this room.
> 		while (!stack.isEmpty()) { // While we have keys...
> 			int node = stack.pop(); // Get the next key 'node'
> 			for (int nei : rooms.get(node)) // For every key in room # 'node'...
> 				if (!seen[nei]) { // ...that hasn't been used yet
> 					seen[nei] = true; // mark that we've entered the room
> 					stack.push(nei); // add the key to the todo list
> 				}
> 		}
>
> 		for (boolean v : seen) // if any room hasn't been visited, return false
> 			if (!v)
> 				return false;
> 		return true;
> 	}
>
> 	public static void main(String[] args) {
>     	
>         Scanner sc=new Scanner(System.in);
>         
>         int numOfRooms = sc.nextInt();
>         sc.nextLine();
>         List<List<Integer>> rooms = new ArrayList<List<Integer>>();
>         for(int i=0;i<numOfRooms;i++) {
>         	String keys = sc.nextLine();
>         	String keyArray[]= keys.split(" ");
>         	List<Integer> keylist = new ArrayList<Integer>();
>         	for(int j=0;j<keyArray.length;j++)
>         		keylist.add(Integer.parseInt(keyArray[j]));
>         	rooms.add(keylist);
>         }
>         
>         System.out.println(canVisitAllRooms(rooms));
>         
>         
>     }
>
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2072%20Solutions/KeysAndRooms.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 72 Solutions/KeysAndRooms.java
