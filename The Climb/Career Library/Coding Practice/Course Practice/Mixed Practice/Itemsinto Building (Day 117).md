---
kind: "coding-problem"
title: "Itemsinto Building (Day 117)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 117 Solutions/ItemsintoBuilding.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Itemsinto Building (Day 117)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

A courier company has to deliver N items with different heights.
All the items have to deliver to one building only.

The building has K rooms inside indexed 0,1,..-K-1, and the heights of the rooms are different.
All the rooms connected with each other and has only one entry point, 
e.g, you can reach room-1 from room-0 only, room-2 from room-1 only, ..so on.

Now the task of the delivery agent is to keep the items inside the building.

To keep the items into the rooms, delivery agent has to follow these rules:
 - Agent can't keep, two goods in same room.
 - As there is only one entry point, If the height of some room is less than the height of an item,
   then the item will be stopped before that room, so are the items behind it.
 - Agent can rearrange the order of items to keep them inside the building.
   
Return the maximum number of items, the delivery agent can keep inside the building.

Input Format:
-------------
Line-1 -> two integers N and K, number of items and number of rooms.
Line-2 -> N space separated integers, heights of the items.
Line-3 -> K space separated integers, heights of the rooms.

Output Format:
--------------
Print an integer as result.


Sample Input-1:
---------------
4 5
4 3 4 1
5 3 3 4 1

Sample Output-1:
----------------
3


### Explanation

------------
We can first keep the item of height 1 in room 4. 
Then we can keep the item of height 3 in either of the 3 rooms 1, 2, or 3.
Lastly, we can keep one box of height 4 in room 0.
There is no way we can keep all 4 items in the building.


Sample Input-2:
---------------
5 4
1 2 2 3 4
3 4 1 2

Sample Output-2:
----------------
3


### Explanation

------------
Notice that it's not possible to keep the item of height 4 into the building,
since it cannot pass the first room of height 3.
Also, for the last two rooms, 2 and 3, only items of height 1 can kept.
In room 2 or 3, keep item of height 1.
In room 1, keep item of height 2.
Finally in room 0, keep item of height 3. 
We can keep 3 items maximum.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ItemsintoBuilding.txt
> ```java
> /*
> A courier company has to deliver N items with different heights.
> All the items have to deliver to one building only.
>
> The building has K rooms inside indexed 0,1,..-K-1, and the heights of the rooms are different.
> All the rooms connected with each other and has only one entry point, 
> e.g, you can reach room-1 from room-0 only, room-2 from room-1 only, ..so on.
>
> Now the task of the delivery agent is to keep the items inside the building.
>
> To keep the items into the rooms, delivery agent has to follow these rules:
>  - Agent can't keep, two goods in same room.
>  - As there is only one entry point, If the height of some room is less than the height of an item,
>    then the item will be stopped before that room, so are the items behind it.
>  - Agent can rearrange the order of items to keep them inside the building.
>    
> Return the maximum number of items, the delivery agent can keep inside the building.
>
> Input Format:
> -------------
> Line-1 -> two integers N and K, number of items and number of rooms.
> Line-2 -> N space separated integers, heights of the items.
> Line-3 -> K space separated integers, heights of the rooms.
>
> Output Format:
> --------------
> Print an integer as result.
>
>
> Sample Input-1:
> ---------------
> 4 5
> 4 3 4 1
> 5 3 3 4 1
>
> Sample Output-1:
> ----------------
> 3
>
> Explanation:
> ------------
> We can first keep the item of height 1 in room 4. 
> Then we can keep the item of height 3 in either of the 3 rooms 1, 2, or 3.
> Lastly, we can keep one box of height 4 in room 0.
> There is no way we can keep all 4 items in the building.
>
>
> Sample Input-2:
> ---------------
> 5 4
> 1 2 2 3 4
> 3 4 1 2
>
> Sample Output-2:
> ----------------
> 3
>
> Explanation:
> ------------
> Notice that it's not possible to keep the item of height 4 into the building,
> since it cannot pass the first room of height 3.
> Also, for the last two rooms, 2 and 3, only items of height 1 can kept.
> In room 2 or 3, keep item of height 1.
> In room 1, keep item of height 2.
> Finally in room 0, keep item of height 3. 
> We can keep 3 items maximum.
>
> */
>
> import java.util.*;
>
> class ItemsintoBuilding {
>      public int maxItemsInBuilding(int[] items, int[] building) {
>         int minHere = Integer.MAX_VALUE;
>         int[] realSpace = new int[building.length];
>         for (int i = 0; i < building.length; i++) {
>             minHere = Math.min(minHere, building[i]);
>             realSpace[i] = minHere;
>         }
>         Arrays.sort(items);
>         
>         int i = 0;
>         int j = realSpace.length - 1;
>         int result = 0;
>         while (i < items.length && j >= 0) {
>             if (realSpace[j--] >= items[i]) {
>                 i++;
>                 result++;
>             }
>         }
>         return result;
>     }
> 	
> 	public static void main(String args[] ) {
>
> 	    Scanner sc = new Scanner(System.in);
> 		int N= sc.nextInt();
> 		int K= sc.nextInt();
> 		int[] items = new int[N];
> 		int[] building=new int[K];
> 		for(int i=0;i<N;i++)
> 			items[i]= sc.nextInt();
> 		for(int i=0;i<K;i++)
> 			building[i]= sc.nextInt();
> 			
> 		System.out.println(new ItemsintoBuilding().maxItemsInBuilding(items,building));
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20117%20Solutions/ItemsintoBuilding.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 117 Solutions/ItemsintoBuilding.txt
