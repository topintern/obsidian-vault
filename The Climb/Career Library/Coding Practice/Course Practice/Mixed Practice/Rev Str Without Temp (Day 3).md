---
kind: "coding-problem"
title: "Rev Str Without Temp (Day 3)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 3 Solutions/RevStrWithoutTemp.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Rev Str Without Temp (Day 3)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Problem: (Problem No.7 from String Algorithm)program to reverse the string without 
	using any temporary variable and String methods.


	Sample Input : 
        This is Elite Finishing School 

	Sample Output : 
	loohcS gnihsiniF etilE si sihT

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · RevStrWithoutTemp.java
> ```java
>
> /*
>  * Problem: (Problem No.7 from String Algorithm)program to reverse the string without 
> 	using any temporary variable and String methods.
>  * 
>  * 
> 	Sample Input : 
>         This is Elite Finishing School 
>
> 	Sample Output : 
> 	loohcS gnihsiniF etilE si sihT
>
>
>
>  * 
>  * 
>  */
>
> import java.util.Scanner;
>
> public class RevStrWithoutTemp {
>
> 	public static String reverseString(String s) {
> 		StringBuilder str = new StringBuilder(s);
>
>         int end = str.length()-1;
>         int start=0;
> 	//We can use XOR logic for swapping the variables.
>         while(start<end) {
>         	str.setCharAt(start,(char) (str.charAt(start)^str.charAt(end)));
>         	str.setCharAt(end,(char) (str.charAt(end)^str.charAt(start)));
>         	str.setCharAt(start,(char) (str.charAt(start)^str.charAt(end)));
>         	++start;
>         	--end;
>         }
> 		return new String(str);
>     }
> 	
> 	/* main program */
> 	public static void main(String args[]) 
> 	{ 
> 		
> 		Scanner sc = new Scanner(System.in);
> 		String str = sc.nextLine();
> 		String revSentence = reverseString(str);
> 		System.out.println(revSentence);
> 		
> 	} 
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%203%20Solutions/RevStrWithoutTemp.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 3 Solutions/RevStrWithoutTemp.java
