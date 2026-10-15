---
kind: "coding-problem"
title: "Gaming Array (Day 82)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 82 Solutions/GamingArray.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Gaming Array (Day 82)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Input Format:
-------------
    - Line-1 contains a single integer N, the number of elements
    - Line-2 contains N distinct space-separated integers
Output Format:
--------------
    - Print the name of the winner on a new line (i.e., either NAG or RAM).

Note: Always "RAM" starts first.

Sample Input-1:
6                                                                                                                       
3 7 8 4 9 1   

Sample Output-1:
NAG 


Sample Input-2:
8                                                                                                                       
1 3 2 5 4 6 8 7                                                                                                         

Sample Output-2:
RAM
**********Testcases*************

case =1
input =5
1 3 5 7 9
output ="RAM"

case =2
input =5
7 4 6 5 9
output ="NAG"

case =3
input =5
5 2 6 3 4
output ="NAG"

case =4
input =2
3 1
output ="RAM"

case =5
input =50
36111 93698 80741 94434 22683 6381 53224 69661 26101 71888 97119 77822 61131 76944 63568 50237 41015 66946 5766 13741 67267 5836 53521 8532 53444 65655 99944 39926 59788 75226 9826 2486 81903 3259 42445 94489 71706 34850 1654 83702 68399 76961 89772 42282 92054 83522 50276 2542 56616 14758
output ="RAM"

case =6
input =30
89638 17015 83208 64471 15569 61810 1935 85891 17409 60104 42650 89584 87725 41955 11692 48429 68317 80482 48938 96375 58606 68447 29821 90034 71459 94252 45121 36319 82776 67776
output ="NAG"

case =7
input =96
89644 17506 4432 22750 3565 71526 64287 29748 79224 82710 62105 60082 8903 6167 39579 41112 84407 88392 44651 78310 90948 7811 95123 6219 8846 77311 33393 34124 56531 41635 88998 80137 11395 84689 75359 95471 17311 97977 83875 8808 74105 83483 72018 4880 96434 59384 86542 75875 60180 17942 61123 40794 3435 26256 55865 22589 95394 24489 18761 55707 86941 43041 64087 14425 12810 51299 44832 43887 85737 30339 67341 3365 57079 49873 71282 17916 36274 46478 31480 69431 27996 61581 54078 58596 81289 85086 3974 57368 21018 37285 73439 91187 5966 33799 13540 1116
output ="RAM"

case =8
input =100
21781 1374 36757 69740 99802 76781 30570 82183 9281 62251 47675 63545 42136 22438 36206 7047 76742 72910 14424 85707 18150 9062 5469 32489 23451 16226 75746 80136 78690 23089 33763 34320 44270 65224 60299 87313 97382 66569 32377 65846 89028 21388 86028 4143 6985 75077 63135 74448 57096 56449 16107 38224 42090 33849 6 97251 35853 43309 49193 46156 83607 15798 12017 15854 27971 47407 83137 19569 42673 62748 8574 33189 23092 35008 61890 21369 47409 81010 65986 53515 22328 28665 73148 39542 23204 16698 92821 34991 49939 56861 96240 32427 24653 60509 34370 38436 26606 2203 86258 79657
output ="NAG"

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · GamingArray.java
> ```java
> /*
> Input Format:
> -------------
>     - Line-1 contains a single integer N, the number of elements
>     - Line-2 contains N distinct space-separated integers
> Output Format:
> --------------
>     - Print the name of the winner on a new line (i.e., either NAG or RAM).
>
> Note: Always "RAM" starts first.
>
> Sample Input-1:
> 6                                                                                                                       
> 3 7 8 4 9 1   
>
> Sample Output-1:
> NAG 
>
>
> Sample Input-2:
> 8                                                                                                                       
> 1 3 2 5 4 6 8 7                                                                                                         
>
> Sample Output-2:
> RAM
>
>
> ***********Testcases*************
>
> case =1
> input =5
> 1 3 5 7 9
> output ="RAM"
>
> case =2
> input =5
> 7 4 6 5 9
> output ="NAG"
>
> case =3
> input =5
> 5 2 6 3 4
> output ="NAG"
>
> case =4
> input =2
> 3 1
> output ="RAM"
>
> case =5
> input =50
> 36111 93698 80741 94434 22683 6381 53224 69661 26101 71888 97119 77822 61131 76944 63568 50237 41015 66946 5766 13741 67267 5836 53521 8532 53444 65655 99944 39926 59788 75226 9826 2486 81903 3259 42445 94489 71706 34850 1654 83702 68399 76961 89772 42282 92054 83522 50276 2542 56616 14758
> output ="RAM"
>
> case =6
> input =30
> 89638 17015 83208 64471 15569 61810 1935 85891 17409 60104 42650 89584 87725 41955 11692 48429 68317 80482 48938 96375 58606 68447 29821 90034 71459 94252 45121 36319 82776 67776
> output ="NAG"
>
> case =7
> input =96
> 89644 17506 4432 22750 3565 71526 64287 29748 79224 82710 62105 60082 8903 6167 39579 41112 84407 88392 44651 78310 90948 7811 95123 6219 8846 77311 33393 34124 56531 41635 88998 80137 11395 84689 75359 95471 17311 97977 83875 8808 74105 83483 72018 4880 96434 59384 86542 75875 60180 17942 61123 40794 3435 26256 55865 22589 95394 24489 18761 55707 86941 43041 64087 14425 12810 51299 44832 43887 85737 30339 67341 3365 57079 49873 71282 17916 36274 46478 31480 69431 27996 61581 54078 58596 81289 85086 3974 57368 21018 37285 73439 91187 5966 33799 13540 1116
> output ="RAM"
>
> case =8
> input =100
> 21781 1374 36757 69740 99802 76781 30570 82183 9281 62251 47675 63545 42136 22438 36206 7047 76742 72910 14424 85707 18150 9062 5469 32489 23451 16226 75746 80136 78690 23089 33763 34320 44270 65224 60299 87313 97382 66569 32377 65846 89028 21388 86028 4143 6985 75077 63135 74448 57096 56449 16107 38224 42090 33849 6 97251 35853 43309 49193 46156 83607 15798 12017 15854 27971 47407 83137 19569 42673 62748 8574 33189 23092 35008 61890 21369 47409 81010 65986 53515 22328 28665 73148 39542 23204 16698 92821 34991 49939 56861 96240 32427 24653 60509 34370 38436 26606 2203 86258 79657
> output ="NAG"
>
> */
> import java.util.*;
>
> public class GamingArray  { 
>     public static int solve(int[] a) {
>         int currentMax = 0;
>         int count = 0;
>         for (int i = 0; i < a.length; i++) {
>             if (a[i] > currentMax) {
>                 currentMax = a[i];
>                 count++;
>             }
>         }
>         
>         return count;
>     }
>
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         int g = in.nextInt();
>         for(int a0 = 0; a0 < g; a0++){
>             int n = in.nextInt();
>             int[] a = new int[n];
>             for(int i = 0; i < n; i++) {
>                 a[i] = in.nextInt();
>             }
>             
>             int turns = solve(a);
>             System.out.println( ((turns & 1) == 0) ? "NAG" : "RAM" );
>         }
>         in.close();
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2082%20Solutions/GamingArray.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 82 Solutions/GamingArray.java
