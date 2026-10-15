---
kind: "coding-problem"
title: "String Value (Day 110)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 110 Solutions/StringValue.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# String Value (Day 110)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Subodh is interested in playing with Strings,
For a given String 'S', Subodh applies some rules to find the value of 'S'.
The rules are as follows:
	- If it is a balanced () has value 1
	- XY has value X + Y , where X and Y are balanced () strings.
	- (Z) has score 2 * Z , where Z is a balanced parentheses string.
	
Find out the value of given String and print it.

Note: All the given strings are balanced

Input Format:
----------------
A String contains only '(', ')'


Output Format:
------------------
Print an integer as result.


Sample Input-1:
-------------------
()

Sample Output-1:
---------------------
1

Sample Input-2:
-------------------
(())

Sample Output-2:
---------------------
2

Sample Input-3:
-------------------
(()(()))

Sample Output-3:
---------------------
6

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · StringValue.txt
> ```java
> /*
> Subodh is interested in playing with Strings,
> For a given String 'S', Subodh applies some rules to find the value of 'S'.
> The rules are as follows:
> 	- If it is a balanced () has value 1
> 	- XY has value X + Y , where X and Y are balanced () strings.
> 	- (Z) has score 2 * Z , where Z is a balanced parentheses string.
> 	
> Find out the value of given String and print it.
>
> Note: All the given strings are balanced
>
> Input Format:
> ----------------
> A String contains only '(', ')'
>
>
> Output Format:
> ------------------
> Print an integer as result.
>
>
> Sample Input-1:
> -------------------
> ()
>
> Sample Output-1:
> ---------------------
> 1
>
> Sample Input-2:
> -------------------
> (())
>
> Sample Output-2:
> ---------------------
> 2
>
> Sample Input-3:
> -------------------
> (()(()))
>
> Sample Output-3:
> ---------------------
> 6
>
> */
>
> import java.util.*;
>
> class StringValue {
>     public static int valueOfString(String S) {
>         Stack<Integer> stack = new Stack<>();
>         int cur = 0;
>         for (char c : S.toCharArray()) {
>             if (c == '(') {
>                 stack.push(cur);
>                 cur = 0;
>             } else {
>                 cur = stack.pop() + Math.max(cur * 2, 1);
>             }
>         }
>         return cur;
>     }
> 	
> 	public static void main(String args[])
> 	{
> 		Scanner sc = new Scanner(System.in);
> 		String s=sc.next();
> 		System.out.println(valueOfString(s));
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20110%20Solutions/StringValue.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 110 Solutions/StringValue.txt
