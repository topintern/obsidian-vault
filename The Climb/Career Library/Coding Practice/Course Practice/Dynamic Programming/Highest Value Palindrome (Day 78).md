---
kind: "coding-problem"
title: "Highest Value Palindrome (Day 78)"
collection: "Course Practice"
topic: "Dynamic Programming"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 78 Solutions/HighestValuePalindrome.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Highest Value Palindrome (Day 78)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Venkat works with strings made up of digits[0-9].
He wants to find the biggest String possible after a maximum number of changes you can make. 
	- He can alter the string, one digit at a time
	- The final string should be a palindrome.
	- The length of the string should be same.


Input Format:
	- Two integers,  C and R, the count of digits in the number and R number of replacements.
	- Next line contains C-digit string [0-9].

Output Format:
	- An integer, result of the program.
	  If not possible, print -1.


### Sample Input

5 2
13456

### Sample Output

65456


### Sample Input

4 1
1234

### Sample Output

-1
********Testcases*********
case =1
input =20 6
06411597833879519468
output =99491597833879519499

case =2
input =4 1
1234
output =-1

case =3
input =15 6
864115979519468
output =994915999519499

case =4
input =10 4
9785456789
output =9886556889

case =5
input =5 2
13456
output =65456

case =6
input =4 1
0011
output =-1

case =7
input =6 3
092282
output =992299

case =8
input =4 1
3943
output =3993

case =9
input =5 2
00100
output =90109

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · HighestValuePalindrome.java
> ```java
> /*
> Venkat works with strings made up of digits[0-9].
> He wants to find the biggest String possible after a maximum number of changes you can make. 
> 	- He can alter the string, one digit at a time
> 	- The final string should be a palindrome.
> 	- The length of the string should be same.
>
>
> Input Format:
> 	- Two integers,  C and R, the count of digits in the number and R number of replacements.
> 	- Next line contains C-digit string [0-9].
>
> Output Format:
> 	- An integer, result of the program.
> 	  If not possible, print -1.
>
> Sample Input:
> 5 2
> 13456
> Sample Output:
> 65456
>
> Sample Input:
> 4 1
> 1234
> Sample Output:
> -1
>
>
> *********Testcases*********
> case =1
> input =20 6
> 06411597833879519468
> output =99491597833879519499
>
> case =2
> input =4 1
> 1234
> output =-1
>
> case =3
> input =15 6
> 864115979519468
> output =994915999519499
>
> case =4
> input =10 4
> 9785456789
> output =9886556889
>
> case =5
> input =5 2
> 13456
> output =65456
>
> case =6
> input =4 1
> 0011
> output =-1
>
> case =7
> input =6 3
> 092282
> output =992299
>
> case =8
> input =4 1
> 3943
> output =3993
>
> case =9
> input =5 2
> 00100
> output =90109
>
>
> */
>
> import java.util.Scanner;
>
> public class HighestValuePalindrome{
>     public static void main(String[] args) {
>         Scanner scanner = new Scanner(System.in);
>         int n = scanner.nextInt();
>         int k = scanner.nextInt();
>         char[] ch = scanner.next().toCharArray();
>         boolean[] v = new boolean[n];
>
>         for (int i = 0; 2 * i < n - 1; i++) {
>             int j = n - 1 - i;
>             if (ch[j] != ch[i]) {
>                 if (k == 0) {
>                     System.out.println(-1);
>                     return;
>                 }
>                 k--;
>                 char c = (ch[i] > ch[j]) ? ch[i] : ch[j];
>                 ch[i] = c;
>                 ch[j] = c;
>                 v[i] = true;
>             }
>         }
>         int i = 0;
>         while (k > 0 && 2 * i < n) {
>             if (ch[i] == '9') {
>                 i++;
>                 continue;
>             }
>             if (v[i] || 2*i == n-1) {
>                 ch[i] = '9';
>                 ch[n-1-i] = '9';
>                 k--;
>             }
>             if (!v[i] && k >= 2) {
>                 ch[i] = '9';
>                 ch[n-1-i] = '9';
>                 k -= 2;
>             }
>             i++;
>         }
>         System.out.println(new String(ch));
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2078%20Solutions/HighestValuePalindrome.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 78 Solutions/HighestValuePalindrome.java
