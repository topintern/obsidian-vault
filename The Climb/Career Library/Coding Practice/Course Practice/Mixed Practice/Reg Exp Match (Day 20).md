---
kind: "coding-problem"
title: "Reg Exp Match (Day 20)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 20 Solutions/RegExpMatch.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Reg Exp Match (Day 20)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*'.

'.' Matches any single character.
'*' Matches zero or more of the preceding element.
The matching should cover the entire input string (not partial).

Note:

s could be empty and contains only lowercase letters a-z.
p could be empty and contains only lowercase letters a-z, and characters like . or *.
Example 1:

Input:
s = "aa"
p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
Example 2:

Input:
s = "aa"
p = "a*"
Output: true
Explanation: '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
Example 3:

Input:
s = "ab"
p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
Example 4:

Input:
s = "aab"
p = "c*a*b"
Output: true
Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore, it matches "aab".
Example 5:

Input:
s = "mississippi"
p = "mis*is*p*."
Output: false

-----------TestCases---------
case =1
input =memorial
m*emor*al
output =false

case =2
input =iiijjjjijjjkkkkiii
i*j*ik*iii
output =false

case =3
input =institute
i.s*ti*ut*.
output =false

case =4
input =institute
i.s*.it*ut*.
output =true

case =5
input =aaaaaaaaaaaaabbbbbbbbcccccc
a*b*.....c
output =true

case =6
input =iiijjjjijjjkkkkiii
i*j*i...k*iii
output =true

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · RegExpMatch.java
> ```java
> /*
> Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*'.
>
> '.' Matches any single character.
> '*' Matches zero or more of the preceding element.
> The matching should cover the entire input string (not partial).
>
> Note:
>
> s could be empty and contains only lowercase letters a-z.
> p could be empty and contains only lowercase letters a-z, and characters like . or *.
> Example 1:
>
> Input:
> s = "aa"
> p = "a"
> Output: false
> Explanation: "a" does not match the entire string "aa".
> Example 2:
>
> Input:
> s = "aa"
> p = "a*"
> Output: true
> Explanation: '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
> Example 3:
>
> Input:
> s = "ab"
> p = ".*"
> Output: true
> Explanation: ".*" means "zero or more (*) of any character (.)".
> Example 4:
>
> Input:
> s = "aab"
> p = "c*a*b"
> Output: true
> Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore, it matches "aab".
> Example 5:
>
> Input:
> s = "mississippi"
> p = "mis*is*p*."
> Output: false
>
> -----------TestCases---------
> case =1
> input =memorial
> m*emor*al
> output =false
>
> case =2
> input =iiijjjjijjjkkkkiii
> i*j*ik*iii
> output =false
>
> case =3
> input =institute
> i.s*ti*ut*.
> output =false
>
> case =4
> input =institute
> i.s*.it*ut*.
> output =true
>
> case =5
> input =aaaaaaaaaaaaabbbbbbbbcccccc
> a*b*.....c
> output =true
>
> case =6
> input =iiijjjjijjjkkkkiii
> i*j*i...k*iii
> output =true
>
> */
>
> import java.util.*;
>
> class RegExpMatch
> {
> 	public static boolean isMatch(String text, String pattern) {
>         if (pattern.isEmpty()) return text.isEmpty();
>         boolean first_match = (!text.isEmpty() &&
>                                (pattern.charAt(0) == text.charAt(0) || pattern.charAt(0) == '.'));
>
>         if (pattern.length() >= 2 && pattern.charAt(1) == '*'){
>             return (isMatch(text, pattern.substring(2)) ||
>                     (first_match && isMatch(text.substring(1), pattern)));
>         } else {
>             return first_match && isMatch(text.substring(1), pattern.substring(1));
>         }
>     }
> 	public static void main(String args[])
> 	{
> 		Scanner scan=new Scanner(System.in);
> 		String s=scan.next();
> 		String p=scan.next();
> 		System.out.println(isMatch(s,p));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2020%20Solutions/RegExpMatch.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 20 Solutions/RegExpMatch.java
