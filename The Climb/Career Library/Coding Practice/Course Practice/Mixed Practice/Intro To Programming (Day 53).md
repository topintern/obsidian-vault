---
kind: "coding-problem"
title: "Intro To Programming (Day 53)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 53 Solutions/IntroToProgramming.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Intro To Programming (Day 53)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Introduction to programming is considered as easiest subject among the students of first years (well ,usually). 
So they are not focusing much on lectures. when professor realises this he becomes very angry and 
plans to fail all the students of the batch.

He writes a very big number on the whiteboard and says : 
" This will be the minimum mark required to pass this course" . 
When students see this gigantic number written on the whiteboard most of them become pretty sure 
that they are going to fail this semester.

So the some of the students started trying to convince the professor to not do so. 
So the professor gives them a number K and says : 
" You can erase exactly K digits of the given number" .

Now students want to make this number as small as possible. 
So you being the second most intelligent student of the batch decide 
to solve the problem. Save the other students.


### Input

The only line in the input contains one string denoting the number written on the whiteboard and integer K.


### Output

Output the minimum number you can make without any trailing zeroes.



### Sample Input 

1023231 3


### Sample output 

221


### Explanation 

Need to remove 3 digits from the given number so 
First we need to remove starting 1 to take the advantage of preceeding zero which any way has no value being as first digit. 
So Number is 023231(23231)
Second Remove 3 Number becomes 2231
Third Remove 3 Number becomes 221

========= TestCases Prog-4 =========

case =1
input =4732801984 7
output =14

case =2
input =65487948914 7
output =4414

case =3
input =97987453193 8
output =193

case =4
input =978234516 8
output =16

case =5
input =120023431 4
output =231

case =6
input =120054621 4
output =421

case =7
input =120054634 5
output =34

case =8
input =1023231 4
output =21

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · IntroToProgramming.java
> ```java
> /*
> Introduction to programming is considered as easiest subject among the students of first years (well ,usually). 
> So they are not focusing much on lectures. when professor realises this he becomes very angry and 
> plans to fail all the students of the batch.
>
> He writes a very big number on the whiteboard and says : 
> " This will be the minimum mark required to pass this course" . 
> When students see this gigantic number written on the whiteboard most of them become pretty sure 
> that they are going to fail this semester.
>
> So the some of the students started trying to convince the professor to not do so. 
> So the professor gives them a number K and says : 
> " You can erase exactly K digits of the given number" .
>
> Now students want to make this number as small as possible. 
> So you being the second most intelligent student of the batch decide 
> to solve the problem. Save the other students.
>
> Input
> The only line in the input contains one string denoting the number written on the whiteboard and integer K.
>
> Output
> Output the minimum number you can make without any trailing zeroes.
>
>
> Sample Input :
> 1023231 3
>
> Sample output :
> 221
>
> Explanation :
> Need to remove 3 digits from the given number so 
> First we need to remove starting 1 to take the advantage of preceeding zero which any way has no value being as first digit. 
> So Number is 023231(23231)
> Second Remove 3 Number becomes 2231
> Third Remove 3 Number becomes 221
>
> ========= TestCases Prog-4 =========
>
> case =1
> input =4732801984 7
> output =14
>
> case =2
> input =65487948914 7
> output =4414
>
> case =3
> input =97987453193 8
> output =193
>
> case =4
> input =978234516 8
> output =16
>
> case =5
> input =120023431 4
> output =231
>
> case =6
> input =120054621 4
> output =421
>
> case =7
> input =120054634 5
> output =34
>
> case =8
> input =1023231 4
> output =21
>
> */
>
> import java.util.*;
>
> class IntroToProgramming {
> 	public static void main(String args[]) throws Exception {
>
> 		Scanner s = new Scanner(System.in);
> 		char c[] = s.next().toCharArray();
> 		int k = s.nextInt();
> 		Stack<Character> stack = new Stack<>();
>
> 		for (int i = 0; i < c.length; i++) {
>
> 			while (!stack.isEmpty() && c[i] < stack.peek() && k > 0) {
> 				stack.pop();
> 				k--;
> 			}
>
> 			stack.push(c[i]);
>
> 		}
>
> 		Stack<Character> st = new Stack<>();
>
> 		while (!stack.isEmpty()) {
> 			st.push(stack.pop());
> 		}
>
> 		while (st.peek() == '0') {
> 			st.pop();
> 		}
> 		char ch[] = new char[st.size()];
> 		int l = 0;
> 		while (!st.isEmpty())
> 			ch[l++] = st.pop();
>
> 		String str = new String(ch);
>
> 		System.out.println(str);
>
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2053%20Solutions/IntroToProgramming.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 53 Solutions/IntroToProgramming.java
