---
kind: "coding-problem"
title: "Highest Number (Day 115)"
collection: "Course Practice"
topic: "Math and Counting"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 115 Solutions/HighestNumber.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Highest Number (Day 115)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Manasa is playing with numbers. She is given a list of integers.
She is appending the numbers together, in such a way
the newly formed number should be the highest possible number.

Help Manasa with a program, to find the highest possible number.

Note: The result may be long, please maintain the number as string.

Input Format:
-------------
Space separated integers nums[], list of numbers.

Output Format:
--------------
Print the highest possible number.


Sample Input-1:
---------------
10 2

Sample Output-1:
----------------
210


Sample Input-2:
---------------
3 30 34 5 9

Sample Output-2:
----------------
9534330

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · HighestNumber.java
> ```java
> /*
> Manasa is playing with numbers. She is given a list of integers.
> She is appending the numbers together, in such a way
> the newly formed number should be the highest possible number.
>
> Help Manasa with a program, to find the highest possible number.
>
> Note: The result may be long, please maintain the number as string.
>
> Input Format:
> -------------
> Space separated integers nums[], list of numbers.
>
> Output Format:
> --------------
> Print the highest possible number.
>
>
> Sample Input-1:
> ---------------
> 10 2
>
> Sample Output-1:
> ----------------
> 210
>
>
> Sample Input-2:
> ---------------
> 3 30 34 5 9
>
> Sample Output-2:
> ----------------
> 9534330
>
> */
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.*;
>
> public class HighestNumber {
>      public String largestNumber(int[] num) {
> 		if(num == null || num.length == 0)
> 		    return "";
> 		
> 		// Convert int array to String array, so we can sort later on
> 		String[] s_num = new String[num.length];
> 		for(int i = 0; i < num.length; i++)
> 		    s_num[i] = String.valueOf(num[i]);
> 			
> 		// Comparator to decide which string should come first in concatenation
> 		Comparator<String> comp = new Comparator<String>(){
> 		    @Override
> 		    public int compare(String str1, String str2){
> 		        String s1 = str1 + str2;
> 				String s2 = str2 + str1;
> 				return s2.compareTo(s1); // reverse order here, so we can do append() later
> 		    }
> 	     };
> 		
> 		Arrays.sort(s_num, comp);
> 		// An extreme edge case by lc, say you have only a bunch of 0 in your int array
> 		if(s_num[0].charAt(0) == '0')
> 			return "0";
>             
> 		StringBuilder sb = new StringBuilder();
> 		for(String s: s_num)
> 	        sb.append(s);
> 		
> 		return sb.toString();
> 		
> 	}
> 	
> 	public static void main(String args[] ) throws IOException {
>
> 	    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 		String str = br.readLine();
> 		String[] sarr = str.split(" ");
> 		int[] nums = Arrays.asList(sarr).stream().mapToInt(Integer::parseInt).toArray();
> 		System.out.println(new HighestNumber().highestNumber(nums));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20115%20Solutions/HighestNumber.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 115 Solutions/HighestNumber.java
