---
kind: "coding-problem"
title: "Weighted Uniform String (Day 69)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 69 Solutions/WeightedUniformString.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Weighted Uniform String (Day 69)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

A weighted string is a string of lowercase English letters where each letter has a weight. 
Character weights are 1 to 26 from a to z.

We define the following terms:
	- The weight of a string is the sum of the weights of all the string's characters. 
	  For example:
		apple=> 1+16+16+12+5=50
		hack=> 8+1+3+11=23
		ccccc=>3+3+3+3+3=15

	- A uniform string consists of a single character repeated zero or more times. 
	  For example, ccc and a are uniform strings, but bcb and cd are not.

Given a string S, let U be the set of weights for all possible uniform contiguous substrings of string S.
You have to answer n queries, where each query i consists of a single integer, x[i]. 
For each query, print Yes on a new line if x[i] is an element U; 
otherwise, print No instead.


### Input Format

	- The first line contains a string S, the original string.
	- The second line contains an integer n, the number of queries.
	- Each of the next n lines contains an integer x[i], 
	the weight of a uniform subtring of  that may or may not exist.

NOTE:String S contains only lowercase English letters, ascii[a-z].

Output Format:
	- Print n lines. For each query, print Yes on a new line if x[i] is an element U. 
	Otherwise, print No.

Sample Input1:
abccddde
6
1
3
12
5
9
10
Sample Output1:
Yes
Yes
Yes
Yes
No
No

Explanation1:
The weights of every possible uniform substring in the string abccddde are shown below:
	Substring		Weight
		a				1
		b				2
		c				3
		cc				3+3=6
		d				4
		dd			4+4=8
		ddd			4+4+4=12
		e				5

We print Yes on the first four lines because,
the first four queries match weights of uniform substrings of S. 
We print No for the last two queries because,
there are no uniform substrings in S that have those weights.

Note that while de is a substring of S that would have a weight of 9, it is not a uniform substring.

Note that we are only dealing with contiguous substrings. 
So ccc is not a substring of the string ccxxc.

Sample Input2:
aaabbbbcccddd
5
9
7
8
12
5
Sample Output2:
Yes
No
Yes
Yes
No


========= Testcases Program-1 =========
case =1
input =aaabbbbcccddd
5
9
7
8
12
5
output =Yes
No
Yes
Yes
No


case =2
input =abccddde
6
1
3
12
5
9
10
output =Yes
Yes
Yes
Yes
No
No

case =3
input =ababababbabaaaaad
8
1
2
3
4
5
6
7
8
output =Yes
Yes
Yes
Yes
Yes
No
No
No

case =4
input =apple
4
1
5
32
44
output =Yes
Yes
Yes
No

case =5
input =putty
3
15
40
21
output =No
Yes
Yes

case =6
input =abbcccddddeeeeeffffffggggggg
5
4
8
19
42
35
output =Yes
Yes
No
Yes
Yes

case =7
input =dddeeeeeffff
4
12
14
16
18
output =Yes
No
No
Yes

case =8
input =aanand
4
3
2
28
14
output =No
Yes
No
Yes

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · WeightedUniformString.java
> ```java
> /*
> A weighted string is a string of lowercase English letters where each letter has a weight. 
> Character weights are 1 to 26 from a to z.
>
> We define the following terms:
> 	- The weight of a string is the sum of the weights of all the string's characters. 
> 	  For example:
> 		apple=> 1+16+16+12+5=50
> 		hack=> 8+1+3+11=23
> 		ccccc=>3+3+3+3+3=15
>
> 	- A uniform string consists of a single character repeated zero or more times. 
> 	  For example, ccc and a are uniform strings, but bcb and cd are not.
>
> Given a string S, let U be the set of weights for all possible uniform contiguous substrings of string S.
> You have to answer n queries, where each query i consists of a single integer, x[i]. 
> For each query, print Yes on a new line if x[i] is an element U; 
> otherwise, print No instead.
>
> Input Format
> 	- The first line contains a string S, the original string.
> 	- The second line contains an integer n, the number of queries.
> 	- Each of the next n lines contains an integer x[i], 
> 	the weight of a uniform subtring of  that may or may not exist.
>
> NOTE:String S contains only lowercase English letters, ascii[a-z].
>
> Output Format:
> 	- Print n lines. For each query, print Yes on a new line if x[i] is an element U. 
> 	Otherwise, print No.
>
> Sample Input1:
> abccddde
> 6
> 1
> 3
> 12
> 5
> 9
> 10
> Sample Output1:
> Yes
> Yes
> Yes
> Yes
> No
> No
>
> Explanation1:
> The weights of every possible uniform substring in the string abccddde are shown below:
> 	Substring		Weight
> 		a				1
> 		b				2
> 		c				3
> 		cc				3+3=6
> 		d				4
> 		dd			4+4=8
> 		ddd			4+4+4=12
> 		e				5
>
> We print Yes on the first four lines because,
> the first four queries match weights of uniform substrings of S. 
> We print No for the last two queries because,
> there are no uniform substrings in S that have those weights.
>
> Note that while de is a substring of S that would have a weight of 9, it is not a uniform substring.
>
> Note that we are only dealing with contiguous substrings. 
> So ccc is not a substring of the string ccxxc.
>
> Sample Input2:
> aaabbbbcccddd
> 5
> 9
> 7
> 8
> 12
> 5
> Sample Output2:
> Yes
> No
> Yes
> Yes
> No
>
>
> ========= Testcases Program-1 =========
> case =1
> input =aaabbbbcccddd
> 5
> 9
> 7
> 8
> 12
> 5
> output =Yes
> No
> Yes
> Yes
> No
>
>
> case =2
> input =abccddde
> 6
> 1
> 3
> 12
> 5
> 9
> 10
> output =Yes
> Yes
> Yes
> Yes
> No
> No
>
> case =3
> input =ababababbabaaaaad
> 8
> 1
> 2
> 3
> 4
> 5
> 6
> 7
> 8
> output =Yes
> Yes
> Yes
> Yes
> Yes
> No
> No
> No
>
> case =4
> input =apple
> 4
> 1
> 5
> 32
> 44
> output =Yes
> Yes
> Yes
> No
>
> case =5
> input =putty
> 3
> 15
> 40
> 21
> output =No
> Yes
> Yes
>
> case =6
> input =abbcccddddeeeeeffffffggggggg
> 5
> 4
> 8
> 19
> 42
> 35
> output =Yes
> Yes
> No
> Yes
> Yes
>
> case =7
> input =dddeeeeeffff
> 4
> 12
> 14
> 16
> 18
> output =Yes
> No
> No
> Yes
>
> case =8
> input =aanand
> 4
> 3
> 2
> 28
> 14
> output =No
> Yes
> No
> Yes
>
> */
>
> import java.io.*;
> import java.util.*;
> import java.text.*;
> import java.math.*;
> import java.util.regex.*;
>
> public class WeightedUniformString {
>     public static void main(String[] args) {
>         Scanner in = new Scanner(System.in);
>         String s = in.next();
>         int len =  s.length();
>         int n = in.nextInt();
>         Set<Integer> set = new HashSet<Integer>();
>         int i=0;
>         while(i<len){
>              int j=i;
>              int sum =0;
>              while( j<len && s.charAt(i)==s.charAt(j) ){
>                  sum += (s.charAt(i)-'a') +1;
>                  set.add(sum);
>                  j++;
>              }
>             i = j;
>         }
>         for(int a0 = 0; a0 < n; a0++){
>             int x = in.nextInt();
>             if (set.contains(x)){
>                 System.out.println("Yes");
>             }
>             else{
>                 System.out.println("No");
>             }
>         }
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2069%20Solutions/WeightedUniformString.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 69 Solutions/WeightedUniformString.java
