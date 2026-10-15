---
kind: "coding-problem"
title: "count-luck (Day 81)"
collection: "Course Practice"
topic: "Graphs"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 81 Solution/count-luck-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 81 Solution/CountLuck.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# count-luck (Day 81)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Input Format:
    - line-1 contains 2 space-separated integers r and c, 
      the rows and columns of grid.
    - Each of the next r lines contains a string of length c
      describing a row of the grid, consist of letters [B .*S].
    - The last line contains an integer , a guess number.

Output Format:
    - print "pass"  if your guess is correct. 
    Otherwise, print "fail"
    


### Sample Input

-------------
5 11
..........*
.BBBBBBBBBB
...........
BBBBBBBBBB.
S..........
0

### Sample Output

--------------
pass



### Sample Input

-------------
4 11
.B.B......B
.B*.B.BBB.B
.BB.B.BS...
......BBBB.
4

### Sample Output

--------------
fail
*************Testcases**************
case =1
input =5 17
BBBBBBBBBBBBBBBBB
BBB.BB.BBBBBBBBBB
BB.*..S.BBBBBBBBB
BBB.BB.BBBBBBBBBB
BBBBBBBBBBBBBBBBB
10
output ="fail"

case =2
input =5 17
BBBBBBBBBBBBBBBBB
BBB.BB.BBBBBBBBBB
BB.*..S.BBBBBBBBB
BBB.BB.BBBBBBBBBB
BBBBBBBBBBBBBBBBB
1
output ="pass"

case =3
input =3 41
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
S.......................................*
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
20
output ="pass"

case =4
input =5 11
..........*
.BBBBBBBBBB
...........
BBBBBBBBBB.
S..........
0
output ="pass"

case =5
input =4 11
.B.B......B
.B*.B.BBB.B
.BB.B.BS...
......BBBB.
4
output ="fail"

case =6
input =4 11
.B.B......B
.B*.B.BBB.B
.BB.B.BS...
......BBBB.
40
output ="fail"

case =7
input =41 41
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
S........................................
BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB.
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
.BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB.
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
.BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB.
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
.BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB.
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
.BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB.
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
.BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB.
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
.BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB.
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.*.......................................
281
output ="fail"

case =8
input =41 41
.B.BBBBBBBBBBBBBBBBBBB.B.B.B.B.B.B.B.B.B.
...BBBBBBBBBBBBBBBBBBB...................
.B..B.B.B.B.B.B.B..BBBB*B.B.B.B.B.B.B.BB.
.BBBB.B.B.B.B.B.B.BB.B.B.B.B.B.B.B.B.B.B.
.........................................
.BB.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.BB.
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
.BB.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.BB.
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
.BB.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.BB.
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
.BB.B.B.B.BB.B.BB.B.B.B.B.B.B.B.B.B.B.B.B
.B.B.B.B.B.BBB.B.B.B.B.B.B.B.B.B.B.B.B.B.
B........................................
B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.BB.
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
.B.BB.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.BB.BB
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.BSB.
.B....................................B..
..B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.BB.
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.B...................................B...
.BB.B.B.B.B.B.B.B.B.B.B.B.B.B.BB.BB.BBBB.
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.BB.
.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
.........................................
294
output ="pass"

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · CountLuck.txt
> ```java
> /*
> Input Format:
>     - line-1 contains 2 space-separated integers r and c, 
>       the rows and columns of grid.
>     - Each of the next r lines contains a string of length c
>       describing a row of the grid, consist of letters [B .*S].
>     - The last line contains an integer , a guess number.
>
> Output Format:
>     - print "pass"  if your guess is correct. 
>     Otherwise, print "fail"
>     
>
> Sample Input:
> -------------
> 5 11
> ..........*
> .BBBBBBBBBB
> ...........
> BBBBBBBBBB.
> S..........
> 0
> Sample Output:
> --------------
> pass
>
>
> Sample Input:
> -------------
> 4 11
> .B.B......B
> .B*.B.BBB.B
> .BB.B.BS...
> ......BBBB.
> 4
> Sample Output:
> --------------
> fail
>
>
>
> **************Testcases**************
> case =1
> input =5 17
> BBBBBBBBBBBBBBBBB
> BBB.BB.BBBBBBBBBB
> BB.*..S.BBBBBBBBB
> BBB.BB.BBBBBBBBBB
> BBBBBBBBBBBBBBBBB
> 10
> output ="fail"
>
> case =2
> input =5 17
> BBBBBBBBBBBBBBBBB
> BBB.BB.BBBBBBBBBB
> BB.*..S.BBBBBBBBB
> BBB.BB.BBBBBBBBBB
> BBBBBBBBBBBBBBBBB
> 1
> output ="pass"
>
> case =3
> input =3 41
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> S.......................................*
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> 20
> output ="pass"
>
> case =4
> input =5 11
> ..........*
> .BBBBBBBBBB
> ...........
> BBBBBBBBBB.
> S..........
> 0
> output ="pass"
>
> case =5
> input =4 11
> .B.B......B
> .B*.B.BBB.B
> .BB.B.BS...
> ......BBBB.
> 4
> output ="fail"
>
> case =6
> input =4 11
> .B.B......B
> .B*.B.BBB.B
> .BB.B.BS...
> ......BBBB.
> 40
> output ="fail"
>
> case =7
> input =41 41
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> S........................................
> BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB.
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> .BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB.
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> .BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB.
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> .BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB.
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> .BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB.
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> .BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB.
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> .BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB.
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .*.......................................
> 281
> output ="fail"
>
> case =8
> input =41 41
> .B.BBBBBBBBBBBBBBBBBBB.B.B.B.B.B.B.B.B.B.
> ...BBBBBBBBBBBBBBBBBBB...................
> .B..B.B.B.B.B.B.B..BBBB*B.B.B.B.B.B.B.BB.
> .BBBB.B.B.B.B.B.B.BB.B.B.B.B.B.B.B.B.B.B.
> .........................................
> .BB.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.BB.
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> .BB.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.BB.
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> .BB.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.BB.
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> .BB.B.B.B.BB.B.BB.B.B.B.B.B.B.B.B.B.B.B.B
> .B.B.B.B.B.BBB.B.B.B.B.B.B.B.B.B.B.B.B.B.
> B........................................
> B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.BB.
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> .B.BB.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.BB.BB
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.BSB.
> .B....................................B..
> ..B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.BB.
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .B...................................B...
> .BB.B.B.B.B.B.B.B.B.B.B.B.B.B.BB.BB.BBBB.
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.BB.
> .B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.B.
> .........................................
> 294
> output ="pass"
>
>
> */
>
> import java.util.*;
>
> public class Solution{
>     static boolean visited[][];
>     static int n,m,posi,posj,desti,destj;
>     static String[] forest;
>     static boolean dfs(int i,int j,int waves[]){
>         if (i<0||j<0||i>=n||j>=m)return false;
>         if (forest[i].charAt(j)=='B')return false;
>         if (visited[i][j])return false;
>         if (i==desti&&j==destj)return true;
>         int w1[]={0},w2[]={0},w3[]={0},w4[]={0};
>         
>         if (check(i+1,j)+check(i-1,j)+check(i,j+1)+check(i,j-1)>1){
>             waves[0]++;
>         }
>         visited[i][j]=true;
>         boolean b=false;
>         if (dfs(i+1,j,w1)){
>             b=true;
>             
>             waves[0]+=w1[0];
>         }else if (dfs(i-1,j,w2)){
>             b=true;
>             waves[0]+=w2[0];
>             
>         }
>         else if (dfs(i,j+1,w3)){
>             b=true;
>             waves[0]+=w3[0];
>         }
>         else if (dfs(i,j-1,w4)){
>             b=true;
>             waves[0]+=w4[0];
>         }
>         
>         return b;
>     }
>     
>     private static int check(int i, int j) {
>         if (i<0||j<0||i>=n||j>=m)return 0;
>         if (forest[i].charAt(j)=='B')return 0;
>         if (visited[i][j])return 0;
>         return 1;
>     }
>     public static void main(String args[]){
>         Scanner sc=new Scanner(System.in);
>          n=sc.nextInt();
>          m=sc.nextInt(); 
>          visited=new boolean[n][m];
>          for (int i=0;i<n;++i)Arrays.fill(visited[i],false);
>          forest=new String[n];
>          for (int i=0;i<n;++i){
>              forest[i]=sc.next();
>              int x;
>              if ((x=forest[i].indexOf("S"))!=-1){
>                  posi=i;
>                  posj=x;
>              }
>              if ((x=forest[i].indexOf("*"))!=-1){
>                  desti=i;
>                  destj=x;
>              }
>          }
>          int k=sc.nextInt();
>          int rr[]={0};
>          dfs(posi,posj,rr);
>          if(rr[0]==k){
>              System.out.println("pass");
>          }
>          else{
>              System.out.println("fail");
>          }  
>     }
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/count-luck-English-0cd2a244.pdf|count-luck-English-0cd2a244.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/count-luck-English-0cd2a244.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2081%20Solution/count-luck-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 81 Solution/count-luck-English.pdf
- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2081%20Solution/CountLuck.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 81 Solution/CountLuck.txt
