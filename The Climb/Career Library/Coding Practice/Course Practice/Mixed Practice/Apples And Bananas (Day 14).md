---
kind: "coding-problem"
title: "Apples And Bananas (Day 14)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 14 Solutions/ApplesAndBananas.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Apples And Bananas (Day 14)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Problem

The source has reference code without a separate problem statement. Establish its inputs, expected outputs, and constraints before practising.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ApplesAndBananas.java
> ```java
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class ApplesAndBananas {
>
> 	
> 	public static String getHint(String secret, String guess) {
> 	    int apples = 0;
> 	    int bananas = 0;
> 	    int[] numbers = new int[10];
> 	    for (int i = 0; i<secret.length(); i++) {
> 	        int s = Character.getNumericValue(secret.charAt(i));
> 	        int g = Character.getNumericValue(guess.charAt(i));
> 	        if (s == g) apples++;
> 	        else {
> 	            if (numbers[s] < 0) bananas++;
> 	            if (numbers[g] > 0) bananas++;
> 	            numbers[s] ++;
> 	            numbers[g] --;
> 	        }
> 	    }
> 	    return apples + "A" + bananas + "B";
> 	}
> 	
> 	 public static void main(String args[] ) throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 			String secret = br.readLine();
> 			String guess = br.readLine();
>
> 			System.out.println(getHint(secret,guess));
> 			}
> 	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2014%20Solutions/ApplesAndBananas.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 14 Solutions/ApplesAndBananas.java
