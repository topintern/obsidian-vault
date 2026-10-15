---
kind: "coding-problem"
title: "Power Jump (Day 57)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 57 Solutions/PowerJump.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Power Jump (Day 57)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

In a revised game of hopscotch, a child is trying to cross a line of tiles with a binary string painted on it. 
Consider the line of tiles to be like a 1D array, where each tile has either a 1 or a 0, 
and a consecutive series of tiles making the whole string. 
The game starts with the child standing in front of the leftmost character of the string

All jumps to reach the end of the string can only be on tiles with 0 or only be on tiles with 1.

The game is won if the child can reach the end of the string, taking jumps with the minimum required power. 

In 10101, the power of the jump from beginning to the first tile is 1, 
but from the first to the third tile is 2 and so on.

Find the minimum power the child's jump should have in order to win the game for different binary strings. 

Note : In one jump, the child can jump to the right, any distance from 1 to the value of the power of her jump.

For example, for the string 10101, the power of the jump needs to be minimum 2.

Sample Input 
11111

Sample Output 
1


### Explanation 

Since all the string elements are 1, the minimum power of the jump needs to be 1 to cross the string.

Sample Input 
11101

Sample Output
2


### Explanation

There is one gap of 2 along a path of 1’s/The minimum power of the jump needs to be 2 to cross the string.


========= Testcases Program-1 =========
case =1
input =11111
output =1

case =2
input =11101
output =2

case =3
input =10101
output =2

case =4
input =1001111100111000111
output =4

case =5
input =100111110011110011
output =3

case =6
input =11110101010110111
output =2

case =7
input =11001100111011100111
output =3

case =8
input =1111111101001000100001
output =5

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · PowerJump.java
> ```java
> /*
> In a revised game of hopscotch, a child is trying to cross a line of tiles with a binary string painted on it. 
> Consider the line of tiles to be like a 1D array, where each tile has either a 1 or a 0, 
> and a consecutive series of tiles making the whole string. 
> The game starts with the child standing in front of the leftmost character of the string
>
> All jumps to reach the end of the string can only be on tiles with 0 or only be on tiles with 1.
>
> The game is won if the child can reach the end of the string, taking jumps with the minimum required power. 
>
> In 10101, the power of the jump from beginning to the first tile is 1, 
> but from the first to the third tile is 2 and so on.
>
> Find the minimum power the child's jump should have in order to win the game for different binary strings. 
>
> Note : In one jump, the child can jump to the right, any distance from 1 to the value of the power of her jump.
>
> For example, for the string 10101, the power of the jump needs to be minimum 2.
>
> Sample Input 
> 11111
>
> Sample Output 
> 1
>
> Explanation :
> Since all the string elements are 1, the minimum power of the jump needs to be 1 to cross the string.
>
> Sample Input 
> 11101
>
> Sample Output
> 2
>
> Explanation:
> There is one gap of 2 along a path of 1’s/The minimum power of the jump needs to be 2 to cross the string.
>
>
> ========= Testcases Program-1 =========
> case =1
> input =11111
> output =1
>
> case =2
> input =11101
> output =2
>
> case =3
> input =10101
> output =2
>
> case =4
> input =1001111100111000111
> output =4
>
> case =5
> input =100111110011110011
> output =3
>
> case =6
> input =11110101010110111
> output =2
>
> case =7
> input =11001100111011100111
> output =3
>
> case =8
> input =1111111101001000100001
> output =5
>
>  
>  */
>
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
>
> public class PowerJump {
> 		public static int powerOfJump(String s) 
> 		{ 
> 			// Initialize the count with 1 
> 			int count = 1; 
> 			int max_so_far = Integer.MIN_VALUE; 
>
> 			// Find the character at last index 
> 			char ch = s.charAt(s.length() - 1); 
>
> 			// Start traversing the string 
> 			for (int i = 0; i < s.length(); i++) { 
>
> 			// Check if the current char is equal 
> 			// to the last character 
> 				if (s.charAt(i) == ch) { 
>
> 					// max_so_far stores maximum value of 
> 					// the power of the jump from starting 
> 					// to ith position 
> 					if (count > max_so_far) { 
> 						max_so_far = count; 
> 					} 
> 					
> 					// Reset the count to 1 
> 					count = 1; 
> 				} 
>
> 				// Else, increment the number of jumps/count 
> 				else
> 					count++; 
> 			} 
>
> 			// Return the maximum number of jumps 
> 			return max_so_far; 
> 		} 
>
> 		public static void main(String[] args) throws IOException 
> 		{ 
> 			BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 			String st = br.readLine();//"10000100000011"; 
> 			System.out.println(powerOfJump(st)); 
> 		} 		
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2057%20Solutions/PowerJump.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 57 Solutions/PowerJump.java
