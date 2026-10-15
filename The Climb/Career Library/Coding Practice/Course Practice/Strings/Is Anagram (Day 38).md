---
kind: "coding-problem"
title: "Is Anagram (Day 38)"
collection: "Course Practice"
topic: "Strings"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 38 Solutions/IsAnagram.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Is Anagram (Day 38)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Find if 2 strings are anagrams, is it possible to find it in o(n) time and O(1) space.
 
input:god
dog
 
 output:
 true
 
 
 input:kmit
 ngir
 
 output:
 false

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · IsAnagram.txt
> ```java
> /*
>  * 
>  Find if 2 strings are anagrams, is it possible to find it in o(n) time and O(1) space.
>  
> input:god
> dog
>  
>  output:
>  true
>  
>  
>  input:kmit
>  ngir
>  
>  output:
>  false
>  
>  */
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class IsAnagram {
>
> 	private static boolean isAnagramWithOneArray(String strFirst, String strSecond) {
> 	    int[] charsCount = new int[256];
>
> 	    if (strFirst != null && strSecond != null) {
> 	        if (strFirst.length() != strSecond.length()) {
> 	            return false;
> 	        }
> 	        for (int i = 0; i < strFirst.length(); i++) {
> 	            charsCount[strFirst.charAt(i)]++;
> 	            charsCount[strSecond.charAt(i)]--;
> 	        }
> 	        for (int i = 0; i < charsCount.length; i++) {
> 	            if (charsCount[i] != 0) {
> 	                return false;
> 	            }
> 	        }
> 	        return true;
> 	    } else {
> 	        return (strFirst == null && strSecond == null);
> 	    }
> 	}
> 	
> 	   public static void main(String args[])  throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
> 			String strFirst = br.readLine();
> 			String strSecond = br.readLine();
>
> 			System.out.println(isAnagramWithOneArray(strFirst,strSecond));
> 	  
> 	    } 
> 	
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2038%20Solutions/IsAnagram.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 38 Solutions/IsAnagram.txt
