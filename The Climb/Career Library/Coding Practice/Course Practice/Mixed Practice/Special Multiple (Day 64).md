---
kind: "coding-problem"
title: "Special Multiple (Day 64)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 64 Solutions/SpecialMultiple.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Special Multiple (Day 64)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

You are given an integer N. Can you find the least positive integer X 
made up of only 9's and 0's, such that, X is a multiple of N?
Note:
X is made up of "one or more occurences of 9" and "zero or more occurences of 0".

Input Format:
An integer N for which the solution has to be found.

Output Format:
Print the answer X. The output should not contain any leading zeroes.

Constraints:
1 <= N <= 500

Sample Input1:
5
Sample Output1:
90
Explanation1:
90 is the smallest number made up of 9's and 0's divisible by 5. Similarly, you can derive for other cases.

Sample Input2:
7
Sample Output2:
9009

Sample Input3:
1
Sample Output3:
9


========= Testcases Program-1 =========
case =1
input =5
output =90

case =2
input =7
output =9009

case =3
input =1
output =9

case =4
input =11
output =99

case =5
input =34
output =999090

case =6
input =47
output =90099

case =7
input =22
output =990

case =8
input =67
output =9909099

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SpecialMultiple.java
> ```java
> /*
> You are given an integer N. Can you find the least positive integer X 
> made up of only 9's and 0's, such that, X is a multiple of N?
> Note:
> X is made up of "one or more occurences of 9" and "zero or more occurences of 0".
>
> Input Format:
> An integer N for which the solution has to be found.
>
> Output Format:
> Print the answer X. The output should not contain any leading zeroes.
>
> Constraints:
> 1 <= N <= 500
>
> Sample Input1:
> 5
> Sample Output1:
> 90
> Explanation1:
> 90 is the smallest number made up of 9's and 0's divisible by 5. Similarly, you can derive for other cases.
>
> Sample Input2:
> 7
> Sample Output2:
> 9009
>
> Sample Input3:
> 1
> Sample Output3:
> 9
>
>
> ========= Testcases Program-1 =========
> case =1
> input =5
> output =90
>
> case =2
> input =7
> output =9009
>
> case =3
> input =1
> output =9
>
> case =4
> input =11
> output =99
>
> case =5
> input =34
> output =999090
>
> case =6
> input =47
> output =90099
>
> case =7
> input =22
> output =990
>
> case =8
> input =67
> output =9909099
>
> */
>
> import java.io.*;
> import java.util.*;
>
> public class SpecialMultiple {
>
>     public static void main(String[] args) {
>         Scanner sc = new Scanner(System.in);
>         int t = sc.nextInt();
>         while(t > 0){
>             t--;
>             sc.nextLine();
>             int n = sc.nextInt();
>             String[] ans = new String[n];
>             for (int i = 0; i < ans.length; i++) {
>                 ans[i] = "";
>             }
>             Queue<Integer> queue = new LinkedList<>();
>             queue.add(9%n);
>             ans[9%n] = "9";
>             while(!queue.isEmpty()){
>                 Integer rem = queue.poll();
>                 if(ans[(rem*10)%n].equals("")){
>                     ans[(rem*10)%n] = ans[rem] + "0";
>                     queue.add((rem*10)%n);
>                 }
>                 if(ans[(rem*10+9)%n].equals("")){
>                     ans[(rem*10+9)%n] = ans[rem] + "9";
>                     queue.add((rem*10+9)%n);
>                 }
>             }
>             System.out.println(ans[0]);
>         }
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2064%20Solutions/SpecialMultiple.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 64 Solutions/SpecialMultiple.java
