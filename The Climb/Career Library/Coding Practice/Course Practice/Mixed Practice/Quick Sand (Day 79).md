---
kind: "coding-problem"
title: "Quick Sand (Day 79)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 79 Solutions/QuickSand.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Quick Sand (Day 79)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Input Format:
    - The first line contains m and n. 
    - The next lines contain characters each describing the state of the land.
        'x' if it is a quicksand and '.' otherwise
Output Format:
   - Output contains a single integer - the largest perimeter. If the rectangular fence cannot be built, 
     print -1
     
     

### Sample Input

3 4
....
.xx.
....


### Sample Output

10



### Explanation

Fence can be put up across the entire. The perimeter is 2*(3-1)+2*(4-1)=10


Sample Input:2
2 2
x.
.x


### Output

-1

We need minimum of 4 points to place the 4 corners of the fence. Hence, print -1.



case =1
input =3 4
....
.xx.
....
output =10

case =2
input =4 4
....
.xx.
.xx.
....
output =12

case =3
input =3 3
...
x.x
...
output =-1

case =4
input =4 4
...x
....
....
x...
output =8


case =5
input =6 6
......
.x.x..
.xxxx.
..xx..
.x..x.
......
output =20

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · QuickSand.java
> ```java
> /*
> Input Format:
>     - The first line contains m and n. 
>     - The next lines contain characters each describing the state of the land.
>         'x' if it is a quicksand and '.' otherwise
> Output Format:
>    - Output contains a single integer - the largest perimeter. If the rectangular fence cannot be built, 
>      print -1
>      
>      
> Sample Input:
> 3 4
> ....
> .xx.
> ....
>
> Sample Output:
> 10
>
>
> Explanation:
> Fence can be put up across the entire. The perimeter is 2*(3-1)+2*(4-1)=10
>
>
> Sample Input:2
> 2 2
> x.
> .x
>
> Output
> -1
>
> We need minimum of 4 points to place the 4 corners of the fence. Hence, print -1.
>
>
>
> case =1
> input =3 4
> ....
> .xx.
> ....
> output =10
>
> case =2
> input =4 4
> ....
> .xx.
> .xx.
> ....
> output =12
>
> case =3
> input =3 3
> ...
> x.x
> ...
> output =-1
>
> case =4
> input =4 4
> ...x
> ....
> ....
> x...
> output =8
>
>
> case =5
> input =6 6
> ......
> .x.x..
> .xxxx.
> ..xx..
> .x..x.
> ......
> output =20
>
>
> */
>
> import java.io.*;
> import java.util.*;
> import java.text.*;
> import java.math.*;
> import java.util.regex.*;
>
> public class QuickSand{
>     
>     public static void main(String[] args) throws Exception {
>         /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
>         BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
>         String s[] = bf.readLine().split(" ");
>         int n = Integer.parseInt(s[0]);
>         int m = Integer.parseInt(s[1]);
>         char ar[][] = new char[n][m];
>         for (int i = 0; i < n; i++) {
>             ar[i] = bf.readLine().toCharArray();
>         }
>         int sumX[][] = new int[n][m];
>         for (int i = 0; i < n; i++) {
>             sumX[i][0] = (ar[i][0] == '.') ? 0 : 1;
>             for (int j = 1; j < m; j++) {
>                 sumX[i][j] = sumX[i][j - 1] + ((ar[i][j] == '.') ? 0 : 1);
>             }
>         }
>         
>         int ans = -1;
>         int y1 = -1;
>         for (int x1 = 0; x1 < m - 1; x1++) {
>             for (int x2 = x1 + 1; x2 < m; x2++) {
>                 y1 = -1;
>                 for (int y2 = 0; y2 < n; y2++) {
>                     if (sumX[y2][x2] == ((x1 == 0) ? 0 : sumX[y2][x1 - 1])) {
>                         if (y1 == -1) {
>                             y1 = y2;
>                         } else {
>                             int perim = 2 * (x2 - x1 + y2 - y1);
>                             ans = Math.max(perim, ans);
>                         }
>                         
>                     } else {
>                         if (ar[y2][x2] == 'x' || ar[y2][x1] == 'x') {
>                             y1 = -1;
>                         }
>                     }
>                 }
>             }
>         }
>         System.out.println((ans == -1) ? -1 : ans);
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2079%20Solutions/QuickSand.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 79 Solutions/QuickSand.java
