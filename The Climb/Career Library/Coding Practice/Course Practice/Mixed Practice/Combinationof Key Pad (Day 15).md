---
kind: "coding-problem"
title: "Combinationof Key Pad (Day 15)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 15 Solutions/CombinationofKeyPad.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Combinationof Key Pad (Day 15)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.



Example:

Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
Note:

Although the above answer is in lexicographical order, your answer could be in any order you want.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · CombinationofKeyPad.java
> ```java
> /*
> Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.
>
> A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.
>
>
>
> Example:
>
> Input: "23"
> Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
> Note:
>
> Although the above answer is in lexicographical order, your answer could be in any order you want.
>
> */
> import java.util.*;
>
> class CombinationofKeyPad {
>   Map<String, String> phone = new HashMap<String, String>() {{
>     put("2", "abc");
>     put("3", "def");
>     put("4", "ghi");
>     put("5", "jkl");
>     put("6", "mno");
>     put("7", "pqrs");
>     put("8", "tuv");
>     put("9", "wxyz");
>   }};
>
>   List<String> output = new ArrayList<String>();
>
>   public void  backtrack(String combination, String next_digits) {
>     // if there is no more digits to check
>     if (next_digits.length() == 0) {
>       // the combination is done
>       output.add(combination);
>     }
>     // if there are still digits to check
>     else {
>       // iterate over all letters which map 
>       // the next available digit
>       String digit = next_digits.substring(0, 1);
>       String letters = phone.get(digit);
>       for (int i = 0; i < letters.length(); i++) {
>         String letter = phone.get(digit).substring(i, i + 1);
>         // append the current letter to the combination
>         // and proceed to the next digits
>         backtrack(combination + letter, next_digits.substring(1));
>       }
>     }
>   }
>
>   public List<String> letterCombinations(String digits) {
>     if (digits.length() != 0)
>       backtrack("", digits);
>     return output;
>   }
>   public static void main(String args[])
>  {
> 	Scanner sc=new Scanner(System.in);
> 	String digits=sc.next();
> 	System.out.println(new CombinationofKeyPad().letterCombinations(digits));
>  }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2015%20Solutions/CombinationofKeyPad.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 15 Solutions/CombinationofKeyPad.java
