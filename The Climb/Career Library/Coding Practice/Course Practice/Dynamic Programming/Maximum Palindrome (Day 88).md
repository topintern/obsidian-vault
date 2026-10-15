---
kind: "coding-problem"
title: "Maximum Palindrome (Day 88)"
collection: "Course Practice"
topic: "Dynamic Programming"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 88 Solutions/MaximumPalindrome.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Maximum Palindrome (Day 88)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

*********Testcases*************
case =1
input =abcbc
3
1 4
1 3
2 4
output =2
3
1

case =2
input =week
2
1 4
2 3
output =2
1

case =3
input =abab
1
1 4
output =2

case =4
input =redivider
4
1 4
2 8
1 9
3 7
output =4
6
24
2

case =5
input =madamimadam
5
1 5
2 7
2 10
1 11
3 9
output =2
4
12
30
6

case =6
input =racecar
3
1 7
2 7
4 6
output =6
4
3

case =7
input =wasitaratisaw
4
1 13
2 6
3 10
3 11
output =360
3
12
24

-----------Removed Testcase----------------
case =8
input =abcdefghijklmnopqrstuvwxyzyxwvutsrqponmlkjihgfedcba
5
1 51
1 45
5 51
6 45
10 51
output =440732388
901214128
364236510
114632607
897415411

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MaximumPalindrome.java
> ```java
> /*
> **********Testcases*************
> case =1
> input =abcbc
> 3
> 1 4
> 1 3
> 2 4
> output =2
> 3
> 1
>
> case =2
> input =week
> 2
> 1 4
> 2 3
> output =2
> 1
>
> case =3
> input =abab
> 1
> 1 4
> output =2
>
> case =4
> input =redivider
> 4
> 1 4
> 2 8
> 1 9
> 3 7
> output =4
> 6
> 24
> 2
>
> case =5
> input =madamimadam
> 5
> 1 5
> 2 7
> 2 10
> 1 11
> 3 9
> output =2
> 4
> 12
> 30
> 6
>
> case =6
> input =racecar
> 3
> 1 7
> 2 7
> 4 6
> output =6
> 4
> 3
>
> case =7
> input =wasitaratisaw
> 4
> 1 13
> 2 6
> 3 10
> 3 11
> output =360
> 3
> 12
> 24
>
> -----------Removed Testcase----------------
> case =8
> input =abcdefghijklmnopqrstuvwxyzyxwvutsrqponmlkjihgfedcba
> 5
> 1 51
> 1 45
> 5 51
> 6 45
> 10 51
> output =440732388
> 901214128
> 364236510
> 114632607
> 897415411
>
>
> */
>
> import java.util.*;
>
> public class MaximumPalindrome {
>
>     private static final int MAX_SIZE = 100010;
>     private static final int REM = 1000000007;
>
>     private static int[][] count;
>     private static int[] fact = new int[MAX_SIZE];
>     private static int[] rfact = new int[MAX_SIZE];
>     
>     static int pow(int a, int b) {
>         if (b == 0) {return 1;}
>         if (b % 2 == 1) {return (int)((long)pow(a, b-1) * a % REM);}
>         int mid = pow(a, b/2);
>         return (int)((long)mid * mid % REM);
>     }
>     
>     static void initialize(String s) {
>         int len = s.length();
>         count = new int[26][len];
>         for (int i=0; i<=25; ++i) {
>             char ch = (char)('a' + i);
>             count[i][0] = (s.charAt(0) == ch ? 1 : 0);
>             for (int j=1; j<len; ++j) {
>                 count[i][j] = count[i][j-1] + (s.charAt(j) == ch ? 1 : 0);
>             }
>         }
>         
>         fact[0] = 1;
>         rfact[0] = 1;
>         for (int i=1; i<MAX_SIZE; ++i) {
>             fact[i] = (int)((long)fact[i-1] * (long)i % REM);
>             rfact[i] = (int)((long)rfact[i-1] * (long)pow(i, REM-2) % REM);
>         }
>         // This function is called once before all queries.
>     }
>
>     static int answerQuery(int l, int r) {
>         r--; l--;
>         List<Integer> counts = new ArrayList<>();
>         int len = 0;
>         for (int i=0; i<=25; ++i) {
>             int cnt = count[i][r] - (l>0?count[i][l-1]:0);
>             len += cnt / 2;
>             counts.add(cnt);
>         }
>         int ans = 1;
>         int odd_count = 0;
>         for (int i=0; i<=25; ++i) {
>             int cnt = counts.get(i);
>             ans = (int)((long)ans * fact[len] % REM * rfact[cnt/2] % REM * rfact[len-cnt/2] % REM);
>             len -= cnt/2;
>             if (cnt % 2 == 1) {++odd_count;}
>         }
>         if (odd_count > 0) {
>             ans = (int)((long)ans * odd_count % REM);
>         }
>         return ans;
>         // Return the answer for this query modulo 1000000007.
>     }
>
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         String s = in.next();
>         initialize(s);
>         int q = in.nextInt();
>         for(int a0 = 0; a0 < q; a0++){
>             int l = in.nextInt();
>             int r = in.nextInt();
>             int result = answerQuery(l, r);
>             System.out.println(result);
>         }
>         in.close();
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2088%20Solutions/MaximumPalindrome.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 88 Solutions/MaximumPalindrome.java
