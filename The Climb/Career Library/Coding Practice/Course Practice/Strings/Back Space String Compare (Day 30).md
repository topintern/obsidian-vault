---
kind: "coding-problem"
title: "Back Space String Compare (Day 30)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 30 Solutions/BackSpaceStringCompare.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Back Space String Compare (Day 30)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given two strings A and B, return true if they are equal when both are typed into empty text editors.
  # means a backspace character.


Input:gb#d
ac#d
Output: false
Explanation:  A become "gd" and B become "ad".

Input:#a#c
cc#
Output: true
Explanation: A becomes "c" while B becomes "c".


Can you do it in O(N) time and O(1) space?


TestCases :

Input: ab##
c#d#
Output: true
Explanation: Both A and B become "".

Example 3:

Input:a##c
#a#c
Output: true
Explanation: Both A and B become "c".

Example 4:

Input:a#c
b
Output: false
Explanation: A becomes "c" while B becomes "b".

Note:

1 <= A.length <= 200
1 <= B.length <= 200
A and B only contain lowercase letters and '#' characters.
=======================================================================

I believe you have one difficulty here: When we meet a char, we are not sure if it will be still there or be deleted.

However, we can do a back string compare (just like the title of problem).
If we do it backward, we meet a char and we can be sure this char won't be deleted.
If we meet a '#', it tell us we need to skip next lowercase char.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · BackSpaceStringCompare.java
> ```java
> /*
>  * 
>  Given two strings A and B, return true if they are equal when both are typed into empty text editors.
>   # means a backspace character.
>
>
> Input:gb#d
> ac#d
> Output: false
> Explanation:  A become "gd" and B become "ad".
>
> Input:#a#c
> cc#
> Output: true
> Explanation: A becomes "c" while B becomes "c".
>
>
> Can you do it in O(N) time and O(1) space?
>
>
> TestCases :
>
> Input: ab##
> c#d#
> Output: true
> Explanation: Both A and B become "".
>
> Example 3:
>
> Input:a##c
> #a#c
> Output: true
> Explanation: Both A and B become "c".
>
> Example 4:
>
> Input:a#c
> b
> Output: false
> Explanation: A becomes "c" while B becomes "b".
>
> Note:
>
> 1 <= A.length <= 200
> 1 <= B.length <= 200
> A and B only contain lowercase letters and '#' characters.
> =======================================================================
>
> I believe you have one difficulty here: When we meet a char, we are not sure if it will be still there or be deleted.
>
> However, we can do a back string compare (just like the title of problem).
> If we do it backward, we meet a char and we can be sure this char won't be deleted.
> If we meet a '#', it tell us we need to skip next lowercase char.
>
>
>  */
> package Elite2020;
>
> import java.util.Scanner;
>
> public class BackSpaceStringCompare {
> 	
> 	private static String getString(String str) {
>         int n=str.length(), count=0;
>         String result="";
>         for(int i=n-1; i>=0; i--) {
>             char ch=str.charAt(i);
>             if(ch=='#') 
>                 count++;
>             else {
>                 if(count>0)
>                     count--;
>                 else {
>                     result+=ch;
>                 }                     
>             }
>         }
>         return result;
>     }
>     
>     public static boolean backspaceCompare(String S, String T) {
>         return getString(S).equals(getString(T));
>     }
>     
> 	
> 	 public static void main(String args[] ) {
> 		 Scanner sc = new Scanner(System.in);
> 			String S=sc.next();
> 			String T=sc.next();
>
> 		    System.out.println(backspaceCompare(S,T));
> 	}
> 	 
> 	 
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2030%20Solutions/BackSpaceStringCompare.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 30 Solutions/BackSpaceStringCompare.java
