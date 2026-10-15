---
kind: "coding-problem"
title: "Red Knight (Day 64)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 64 Solutions/RedKnight.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Red Knight (Day 64)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

In ordinary chess, the pieces are only of two colors, black and white. 
In our version of chess, we are including new pieces with unique movements. 
One of the most powerful pieces in this version is the red knight.

The red knight can move to six different positions based on its current position 
(UpperLeft, UpperRight, Right, LowerRight, LowerLeft, Left) as shown in the figure below.
	
	--------------------------
	|    |    |    |    |    |    |    |
	--------------------------
	|    |    | ul |    | ur |    |    |
	--------------------------
	|    |    |    |    |    |    |    |
	--------------------------
	|    |    | l  | K |    | r  |    |
	--------------------------
	|    |    |    |    |    |    |    |
	--------------------------
	|    |    | ll |    | lr |    |    |
	--------------------------
	|    |    |    |    |    |    |    |
	--------------------------
	
The board is a grid of size n*n. 
Each cell is identified with a pair of coordinates (i,j), 
where i is the row number and j is the column number, both zero-indexed. 
Thus, (0,0) is the upper-left corner and (n-1,n-1) is the bottom-right corner.

Given the coordinates of the starting position of the red knight and the coordinates of the destination, 
print the minimum number of moves that the red knight has to make 
in order to reach the destination and after that, 
print the order of the moves that must be followed to reach the destination in the shortest way. 
If the destination cannot be reached, print only the word "Impossible".

Note: There may be multiple shortest paths leading to the destination. 
Hence, assume that the red knight considers its possible neighbor locations in the 
following order of priority: UL, UR, R, LR, LL, L. 
In other words, if there are multiple possible options, 
the red knight prioritizes the first move in this list, as long as the shortest path is still achievable. 
Check sample input3: for an illustration.


### Input Format

	- The first line of input contains a single integer n. 
	- The second line contains four space-separated integers istart, jstart, iend, jend 
	  denotes the coordinates of the starting position and  denotes the coordinates of the final position.


### Output Format

	- If the destination can be reached, print two lines. 
		In the first line, print a single integer denoting the minimum number of moves 
		that the red knight has to make in order to reach the destination. 
		In the second line, print the space-separated sequence of moves.
	- If the destination cannot be reached, print a single line containing only the word Impossible.

Sample Input1:
7
6 6 0 1
Sample Output 0
4
UL UL UL L
Explanation1:

Sample Input2:
6
5 1 0 5
Sample Output2:
Impossible
Explanation2:

Sample Input3:
7
0 3 4 3
Sample Output3:
2
LR LL
Explanation3:


========= Testcases Program-3 =========
case =1
input =7
0 3 4 3
output =2
LR LL

case =2
input =6
5 1 0 5
output =Impossible

case =3
input =7
6 6 0 1
4
UL UL UL L
output =

case =4
input =10
0 2 8 6
output =4
LR LR LR LR

case =5
input =70
7 15 67 3
output =30
LR LR LR LR LR LR LR LR LR LL LL LL LL LL LL LL LL LL LL LL LL LL LL LL LL LL LL LL LL LL

case =6
input =30
25 2 23 29
output =14
UR R R R R R R R R R R R R R

case =7
input =10
9 9 5 3
output =4
UL UL L L

case =8
input =5
4 1 0 3
output =2
UR UR

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · RedKnight.java
> ```java
> /*
> In ordinary chess, the pieces are only of two colors, black and white. 
> In our version of chess, we are including new pieces with unique movements. 
> One of the most powerful pieces in this version is the red knight.
>
> The red knight can move to six different positions based on its current position 
> (UpperLeft, UpperRight, Right, LowerRight, LowerLeft, Left) as shown in the figure below.
> 	
> 	--------------------------
> 	|    |    |    |    |    |    |    |
> 	--------------------------
> 	|    |    | ul |    | ur |    |    |
> 	--------------------------
> 	|    |    |    |    |    |    |    |
> 	--------------------------
> 	|    |    | l  | K |    | r  |    |
> 	--------------------------
> 	|    |    |    |    |    |    |    |
> 	--------------------------
> 	|    |    | ll |    | lr |    |    |
> 	--------------------------
> 	|    |    |    |    |    |    |    |
> 	--------------------------
> 	
> The board is a grid of size n*n. 
> Each cell is identified with a pair of coordinates (i,j), 
> where i is the row number and j is the column number, both zero-indexed. 
> Thus, (0,0) is the upper-left corner and (n-1,n-1) is the bottom-right corner.
>
> Given the coordinates of the starting position of the red knight and the coordinates of the destination, 
> print the minimum number of moves that the red knight has to make 
> in order to reach the destination and after that, 
> print the order of the moves that must be followed to reach the destination in the shortest way. 
> If the destination cannot be reached, print only the word "Impossible".
>
> Note: There may be multiple shortest paths leading to the destination. 
> Hence, assume that the red knight considers its possible neighbor locations in the 
> following order of priority: UL, UR, R, LR, LL, L. 
> In other words, if there are multiple possible options, 
> the red knight prioritizes the first move in this list, as long as the shortest path is still achievable. 
> Check sample input3: for an illustration.
>
> Input Format
> 	- The first line of input contains a single integer n. 
> 	- The second line contains four space-separated integers istart, jstart, iend, jend 
> 	  denotes the coordinates of the starting position and  denotes the coordinates of the final position.
>
> Output Format
> 	- If the destination can be reached, print two lines. 
> 		In the first line, print a single integer denoting the minimum number of moves 
> 		that the red knight has to make in order to reach the destination. 
> 		In the second line, print the space-separated sequence of moves.
> 	- If the destination cannot be reached, print a single line containing only the word Impossible.
>
> Sample Input1:
> 7
> 6 6 0 1
> Sample Output 0
> 4
> UL UL UL L
> Explanation1:
>
> Sample Input2:
> 6
> 5 1 0 5
> Sample Output2:
> Impossible
> Explanation2:
>
> Sample Input3:
> 7
> 0 3 4 3
> Sample Output3:
> 2
> LR LL
> Explanation3:
>
>
> ========= Testcases Program-3 =========
> case =1
> input =7
> 0 3 4 3
> output =2
> LR LL
>
> case =2
> input =6
> 5 1 0 5
> output =Impossible
>
> case =3
> input =7
> 6 6 0 1
> 4
> UL UL UL L
> output =
>
> case =4
> input =10
> 0 2 8 6
> output =4
> LR LR LR LR
>
> case =5
> input =70
> 7 15 67 3
> output =30
> LR LR LR LR LR LR LR LR LR LL LL LL LL LL LL LL LL LL LL LL LL LL LL LL LL LL LL LL LL LL
>
> case =6
> input =30
> 25 2 23 29
> output =14
> UR R R R R R R R R R R R R R
>
> case =7
> input =10
> 9 9 5 3
> output =4
> UL UL L L
>
> case =8
> input =5
> 4 1 0 3
> output =2
> UR UR
>
> */
>
>
> import java.io.*;
> import java.util.*;
> import java.text.*;
> import java.math.*;
> import java.util.regex.*;
>
> public class RedKnight {
>
>     static void printShortestPath(int n, int i1, int j1, int i2, int j2) {
>         //  Print the distance along with the sequence of moves.
>         Queue<int[]> que=new LinkedList<>();
>         que.add(new int[]{i1,j1,0,0,-1});
>         int[][][] prev=new int[n][n][3];
>         //prev[i1][j1][2]=-1;
>         int ans=0;
>         while(que.size()>0){
>             Queue<int[]> temp=new LinkedList<>();
>             while(que.size()>0){
>                 int[] arr=que.poll();
>                 //System.out.println(arr[0]+" "+arr[1]);
>                 if(arr[0]<0||arr[0]>=n||arr[1]<0||arr[1]>=n||prev[arr[0]][arr[1]][2]!=0)
>                     continue;
>                 if(arr[0]==i2&&arr[1]==j2){
>                     System.out.println(ans);
>                     String str=turn(arr[4]);
>                     int i=arr[2],j=arr[3];
>                     while(prev[i][j][2]!=-1){
>                         str=turn(prev[i][j][2])+" "+str;
>                         int i3=prev[i][j][0],i4=prev[i][j][1];
>                         i=i3;
>                         j=i4;
>                     }
>                     System.out.println(str);
>                     return;
>                 }
>                 
>                 prev[arr[0]][arr[1]][0]=arr[2];
>                 prev[arr[0]][arr[1]][1]=arr[3];
>                 prev[arr[0]][arr[1]][2]=arr[4];
>                 
>                 int i=arr[0],j=arr[1];
>                 temp.add(new int[]{i-2,j-1,i,j,1});
>                 temp.add(new int[]{i-2,j+1,i,j,2});
>                 temp.add(new int[]{i,j+2,i,j,3});
>                 temp.add(new int[]{i+2,j+1,i,j,4});
>                 temp.add(new int[]{i+2,j-1,i,j,5});
>                 temp.add(new int[]{i,j-2,i,j,6});
>                 
>             }
>             ans++;
>             que=temp;
>         }
>         System.out.println("Impossible");
>     }
>     
>     public static String turn(int x){
>         switch(x){
>             case 1:
>                 return "UL";
>             case 2:
>                 return "UR";
>             case 3:
>                 return "R";
>             case 4:
>                 return "LR";
>             case 5:
>                 return "LL";
>             case 6:
>                 return "L";
>         }
>         return "";
>     }
>
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         int n = in.nextInt();
>         int i_start = in.nextInt();
>         int j_start = in.nextInt();
>         int i_end = in.nextInt();
>         int j_end = in.nextInt();
>         printShortestPath(n, i_start, j_start, i_end, j_end);
>         in.close();
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2064%20Solutions/RedKnight.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 64 Solutions/RedKnight.java
