---
kind: "coding-problem"
title: "Brick Wall (Day 51)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 51 Solutions/BrickWall.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Brick Wall (Day 51)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

There is a brick wall in front of you. The wall is rectangular and has several rows of bricks. 
The bricks have the same height but different width. You want to draw a vertical line from the top to the bottom and cross the least bricks.

The brick wall is represented by a list of rows. 
Each row is a list of integers representing the width of each brick in this row from left to right.

If your line go through the edge of a brick, then the brick is not considered as crossed. 
You need to find out how to draw the line to cross the least bricks and return the number of crossed bricks.

Note:
-	You cannot draw a line just along one of the two vertical edges of the wall, 
	in which case the line will obviously cross no bricks.
-	The width sum of bricks in different rows are the same.
Input: 
6				//No of Rows of bricks
1 2 2 1
3 1 2
1 3 2
2 4
3 1 2
1 3 1 1

Output: 
2

Approach:
We want to cut from the edge of the most common location among all the levels, 
hence using a map to record the locations and their corresponding occurrence.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · BrickWall.java
> ```java
> /*
>  * 
> There is a brick wall in front of you. The wall is rectangular and has several rows of bricks. 
> The bricks have the same height but different width. You want to draw a vertical line from the top to the bottom and cross the least bricks.
>
> The brick wall is represented by a list of rows. 
> Each row is a list of integers representing the width of each brick in this row from left to right.
>
> If your line go through the edge of a brick, then the brick is not considered as crossed. 
> You need to find out how to draw the line to cross the least bricks and return the number of crossed bricks.
>
> Note:
> -	You cannot draw a line just along one of the two vertical edges of the wall, 
> 	in which case the line will obviously cross no bricks.
> -	The width sum of bricks in different rows are the same.
> Input: 
> 6				//No of Rows of bricks
> 1 2 2 1
> 3 1 2
> 1 3 2
> 2 4
> 3 1 2
> 1 3 1 1
>
> Output: 
> 2
>
> Approach:
> We want to cut from the edge of the most common location among all the levels, 
> hence using a map to record the locations and their corresponding occurrence. 
>
>  * 
>  * 
>  */
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.ArrayList;
> import java.util.HashMap;
> import java.util.List;
> import java.util.Map;
>
> public class BrickWall {
>
> 	public static int leastBricks(List<List<Integer>> wall) {
> 		if (wall.size() == 0)
> 			return 0;
> 		int count = 0;
> 		Map<Integer, Integer> map = new HashMap<Integer, Integer>();
> 		for (List<Integer> list : wall) {
> 			int length = 0;
> 			for (int i = 0; i < list.size() - 1; i++) {
> 				length += list.get(i);
> 				map.put(length, map.getOrDefault(length, 0) + 1);
> 				count = Math.max(count, map.get(length));
> 			}
> 		}
> 		return wall.size() - count;
> 	}
>
> 	public static void main(String args[]) throws IOException {
> 		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 		int numOfRowsOfBricks = Integer.parseInt(br.readLine());
> 		List<List<Integer>> wall = new ArrayList<List<Integer>>();
> 		for (int i = 0; i < numOfRowsOfBricks; i++) {
> 			String str = br.readLine();
> 			String[] bricks = str.split(" ");
> 			List<Integer> brickRow = new ArrayList<Integer>(bricks.length);
> 			for (String brick : bricks) {
> 				brickRow.add(Integer.parseInt(brick));
> 			}
> 			wall.add(brickRow);
> 		}
> 		System.out.println(leastBricks(wall));
>
> 	}
> }
>
> /*
> ===== testcases program-1 =====
> case=1
> input=6
> 1 2 3
> 3 1 2
> 1 3 2
> 2 4
> 5 1
> 2 3 1
> output=4
>
> case=2
> input=6
> 1 2 2 1
> 3 1 2
> 1 3 2
> 2 4
> 3 2 1
> 1 3 1 1
> output=3
>
> case=3
> input=8
> 1 2 2 1 1 1
> 3 1 2 1 1
> 1 3 2 1 1
> 2 3 3
> 3 1 2 1 1
> 1 3 1 1 1 1
> 3 1 2 1 1
> 1 3 1 1 1 1
> output=1
>
> case=4
> input=3
> 6 3 1
> 2 5 3
> 1 4 3 2
> output=2
>
> case=5
> input=6
> 3 5 2 4
> 4 2 1 1 1 5
> 3 2 1 2 1 5
> 6 2 1 5
> 6 8
> 1 2 3 4 4
> output=1
>
> case=6
> input=5
> 3 1 4 2
> 5 5
> 2 3 4 1
> 1 2 3 4
> 4 1 2 3
> output=2
>
> case=7
> input=6
> 1 2 2 1 1 1
> 1 3 2 1 1
> 2 3 3
> 3 1 2 1 1
> 1 3 1 1 1 1
> 3 1 2 1 1
> output=1
>
> case=8
> input=4
> 6 3 1 4
> 4 2 5 3
> 1 4 6 1 2
> 2 3 4 5
> output=2
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2051%20Solutions/BrickWall.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 51 Solutions/BrickWall.java
