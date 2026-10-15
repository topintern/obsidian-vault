---
kind: "coding-problem"
title: "Morgan And String (Day 74)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 74 Solutions/MorganAndString.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Morgan And String (Day 74)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Jack and Daniel are friends. Both of them like letters, especially upper-case ones.
They are cutting upper-case letters from newspapers, and each one of them has his collection of letters stored in a stack.

One beautiful day, Morgan visited Jack and Daniel. He saw their collections. He wondered what is the lexicographically minimal string made of those two collections. He can take a letter from a collection only when it is on the top of the stack. Morgan wants to use all of the letters in their collections.

As an example, assume Jack has collected a={A,C,A} and Daniel has b={B,C,F} . The example shows the top at index  for each stack of letters. Assembling the string would go as follows:

Jack	Daniel	result
ACA	BCF
CA	BCF	A
CA	CF	AB
A	CF	ABC
A	CF	ABCA
    	F	ABCAC
    		ABCACF
Note the choice when there was a tie at CA and CF.

Function Description

Complete the morganAndString function in the editor below. It should return the completed string.

morganAndString has the following parameter(s):

a: a string representing Jack's letters, top at index 
b: a string representing Daniel's letters, top at index 



### Input Format

 pair of lines are as follows:
- The first line contains string a
- The second line contains string b.

Output the lexicographically minimal string

Sample Input
JACK
DANIEL

Sample Output
DAJACKNIEL

Explanation

The first letters to choose from were J and D since they were at the top of the stack. D was chosen, the options then were J and A. A chosen. Then the two stacks have J and N, so J is chosen. (Current string is DAJ) Continuing this way till the end gives us the resulting string.




### Sample Input

ABACABA
ABACABA


### Sample Output

AABABACABACABA

--------------Testcases Prog-3 -----------
case =1
input =JACK
DANIEL
output ="DAJACKNIEL"

case =2
input =ABACABA
ABACABA
output ="AABABACABACABA"

case =3
input =RAMMOHAN
NAGIREDDY
output ="NAGIRAMMOHANREDDY"

case =4
input =CONFUSION
CONFESSION
output ="CCONFEONFSSIONUSION"

case =5
input =ORANGE
PINAPPLE
output ="OPINAPPLERANGE"

case =6
input =VISHAKHAPATNAM
VIZIANAGARAM
output ="VISHAKHAPATNAMVIZIANAGARAM"

case =7
input =ABBBACACCACBBACABCAC
CBCBBBABCABACBACB
output ="ABBBACACBCBBBABCABACBACBCCACBBACABCAC"

case =8
input =PSEUDOPSEUDOHYPOPARATHYROIDISM
COVOLCANOCONIOSIS
output ="COPSEUDOPSEUDOHVOLCANOCONIOSISYPOPARATHYROIDISM"

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MorganAndString.txt
> ```java
> /*
> Jack and Daniel are friends. Both of them like letters, especially upper-case ones.
> They are cutting upper-case letters from newspapers, and each one of them has his collection of letters stored in a stack.
>
> One beautiful day, Morgan visited Jack and Daniel. He saw their collections. He wondered what is the lexicographically minimal string made of those two collections. He can take a letter from a collection only when it is on the top of the stack. Morgan wants to use all of the letters in their collections.
>
> As an example, assume Jack has collected a={A,C,A} and Daniel has b={B,C,F} . The example shows the top at index  for each stack of letters. Assembling the string would go as follows:
>
> Jack	Daniel	result
> ACA	BCF
> CA	BCF	A
> CA	CF	AB
> A	CF	ABC
> A	CF	ABCA
>     	F	ABCAC
>     		ABCACF
> Note the choice when there was a tie at CA and CF.
>
> Function Description
>
> Complete the morganAndString function in the editor below. It should return the completed string.
>
> morganAndString has the following parameter(s):
>
> a: a string representing Jack's letters, top at index 
> b: a string representing Daniel's letters, top at index 
>
>
> Input Format
>  pair of lines are as follows:
> - The first line contains string a
> - The second line contains string b.
>
> Output the lexicographically minimal string
>
> Sample Input
> JACK
> DANIEL
>
> Sample Output
> DAJACKNIEL
>
> Explanation
>
> The first letters to choose from were J and D since they were at the top of the stack. D was chosen, the options then were J and A. A chosen. Then the two stacks have J and N, so J is chosen. (Current string is DAJ) Continuing this way till the end gives us the resulting string.
>
>
>
> Sample Input:
> ABACABA
> ABACABA
>
> Sample Output:
> AABABACABACABA
>
> --------------Testcases Prog-3 -----------
> case =1
> input =JACK
> DANIEL
> output ="DAJACKNIEL"
>
> case =2
> input =ABACABA
> ABACABA
> output ="AABABACABACABA"
>
> case =3
> input =RAMMOHAN
> NAGIREDDY
> output ="NAGIRAMMOHANREDDY"
>
> case =4
> input =CONFUSION
> CONFESSION
> output ="CCONFEONFSSIONUSION"
>
> case =5
> input =ORANGE
> PINAPPLE
> output ="OPINAPPLERANGE"
>
> case =6
> input =VISHAKHAPATNAM
> VIZIANAGARAM
> output ="VISHAKHAPATNAMVIZIANAGARAM"
>
> case =7
> input =ABBBACACCACBBACABCAC
> CBCBBBABCABACBACB
> output ="ABBBACACBCBBBABCABACBACBCCACBBACABCAC"
>
> case =8
> input =PSEUDOPSEUDOHYPOPARATHYROIDISM
> COVOLCANOCONIOSIS
> output ="COPSEUDOPSEUDOHVOLCANOCONIOSISYPOPARATHYROIDISM"
>
> */
> import java.io.*;
> import java.util.*;
> import java.text.*;
> import java.math.*;
> import java.util.regex.*;
>
> public class MorganAndString {
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>
>         int t = in.nextInt();
>         in.nextLine();
>
>
>             String A = in.nextLine();
>             String B = in.nextLine();
>
>             int i = 0, j = 0;
>             StringBuffer sb = new StringBuffer();
>
>             while(i < A.length() && j < B.length()) {
>                 if (A.charAt(i) < B.charAt(j)) {
>                     sb.append(A.charAt(i++));
>                 } else if (A.charAt(i) > B.charAt(j)) {
>                     sb.append(B.charAt(j++));
>                 } else {
>                     int x = i, y = j;
>                     char a = A.charAt(i);
>                     for(; x < A.length() && y < B.length(); x++, y++) {
>                         if (A.charAt(x) != B.charAt(y)) {
>                             break;
>                         } else if (A.charAt(x) > a) {
>                             sb.append(A.substring(i, x)).append(B.substring(j, y));
>                             i = x; j = y;
>                             a = A.charAt(x);
>                         }
>                     }
>
>                     if (x == A.length()) {
>                         sb.append(B.charAt(j));
>                         j++;
>                     } else if (y == B.length()) {
>                         sb.append(A.charAt(i));
>                         i++;
>                     } else {
>                         if (A.charAt(x) < B.charAt(y)) {
>                             sb.append(A.charAt(i));
>                             i++;
>                         } else {
>                             sb.append(B.charAt(j));
>                             j++;
>                         }
>                     }
>                 }
>           
>
>             sb.append(A.substring(i)).append(B.substring(j));
>
>             System.out.println(sb);
>         }
>     }
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2074%20Solutions/MorganAndString.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 74 Solutions/MorganAndString.txt
