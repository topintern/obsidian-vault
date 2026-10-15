---
kind: "coding-problem"
title: "String Modified (Day 110)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 110 Solutions/StringModified.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# String Modified (Day 110)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Somesh is given a task to you on Strings.
You have given a string S ([a-z]), and an integer array Arr[]
Now your task is to modify 'S' in such way:
replace the 'i+1' characters in the string, with next i-th character in alphabetic order(cyclic).

For example, if S="art", Arr[]=[2,3,5] is 3, 
i=0, modify('a') = 'c' , S="crt".
i=1, modify('c') = 'f', modify('r') = 'u', S="fut".
i=2, modify('f') = 'k', modify('u') = 'z', modify('t') = 'y', S="kzy"
Finally modified string is kzy. 

Note: if arr[i]=3 modify('z') ='c'

Return the final modified string after all such modifications to S are applied.

Input Format:
-------------
Line-1 -> A String S,  string length is L
Line-2 -> L space separated integers.

Output Format:
--------------
Print modifed String.


Sample Input-1:
-------------------
adbp
1 2 3 4

Sample Output-1:
--------------------
kmit

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · StringModified.txt
> ```java
> /*
> Somesh is given a task to you on Strings.
> You have given a string S ([a-z]), and an integer array Arr[]
> Now your task is to modify 'S' in such way:
> replace the 'i+1' characters in the string, with next i-th character in alphabetic order(cyclic).
>
> For example, if S="art", Arr[]=[2,3,5] is 3, 
> i=0, modify('a') = 'c' , S="crt".
> i=1, modify('c') = 'f', modify('r') = 'u', S="fut".
> i=2, modify('f') = 'k', modify('u') = 'z', modify('t') = 'y', S="kzy"
> Finally modified string is kzy. 
>
> Note: if arr[i]=3 modify('z') ='c'
>
> Return the final modified string after all such modifications to S are applied.
>
> Input Format:
> -------------
> Line-1 -> A String S,  string length is L
> Line-2 -> L space separated integers.
>
> Output Format:
> --------------
> Print modifed String.
>
>
> Sample Input-1:
> -------------------
> adbp
> 1 2 3 4
>
> Sample Output-1:
> --------------------
> kmit
> */
>
> import java.util.*;
>
> class StringModified {
>     public static String modifyLetters(String S, int[] Arr) {
>         StringBuilder res = new StringBuilder(S);
>         for (int i = Arr.length - 2; i >= 0; i--)
>             Arr[i] = (Arr[i] + Arr[i + 1]) % 26;
>         for (int i = 0; i < S.length(); i++)
>             res.setCharAt(i, (char)((S.charAt(i) - 'a' + Arr[i]) % 26 + 'a'));
>         return res.toString();
>     }
> 	
> 	public static void main(String args[])
> 	{
> 		Scanner sc = new Scanner(System.in);
> 		String s=sc.nextLine();
> 		String array[]=sc.nextLine().split(" ");
> 		
> 		int Arr[]=new int[array.length];
> 	
> 		for(int i=0;i<array.length;i++)
> 			Arr[i]=Integer.parseInt(array[i]);
>
> 		System.out.println(modifyLetters(s,Arr));
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20110%20Solutions/StringModified.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 110 Solutions/StringModified.txt
