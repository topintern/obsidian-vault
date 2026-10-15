---
kind: "coding-problem"
title: "Brace Expression (Day 5)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 5 Solutions/BraceExpression.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Brace Expression (Day 5)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a string 'S' represents a format.

In the given format, Each letter in the word has 1 or more options.  If there is one option, the letter is represented as is.  
If there is more than one option, then curly braces delimit the options.  

-> For example, {a,b,c} represents options a, b, c.
-> For example, {a,b}c{d,e} represents the list acd, ace, bcd, bce

Return all words that can be formed in this manner, in lexicographical order.

Example 1:
		input=		{b}c{e,g}k
		output=	bcek bcgk

Example 2:
		input=		{a,b}{c,d}
		output=	ab ad bc bd

Example 3:
		input=	 {xyz}a{b,c}
		output= xyzab xyzac

TestCases:
case =1
input ={a,b,c,d}e{x,y,z}
output =aex aey aez bex bey bez cex cey cez dex dey dez 

case =2
input ={ab,cd}x{y,z}
output =abxy abxz cdxy cdxz

case =3
input =abcd{x,y,z}f
output =abcdxf abcdyf abcdzf

case =4
input ={abc}{d,e}f{g,h,i}j
output =abcdfgj abcdfhj abcdfij abcefgj abcefhj abcefij

case =5
input =abcdef
output =abcdef

case =6
input =abc{e,f}j{k,l}i{g,h}
output =abcejkig abcejkih abcejlig abcejlih abcfjkig abcfjkih abcfjlig abcfjlih

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · BraceExpression.java
> ```java
> /*
> Given a string 'S' represents a format.
>
> In the given format, Each letter in the word has 1 or more options.  If there is one option, the letter is represented as is.  
> If there is more than one option, then curly braces delimit the options.  
>
> -> For example, {a,b,c} represents options a, b, c.
> -> For example, {a,b}c{d,e} represents the list acd, ace, bcd, bce
>
> Return all words that can be formed in this manner, in lexicographical order.
>
> Example 1:
> 		input=		{b}c{e,g}k
> 		output=	bcek bcgk
>
> Example 2:
> 		input=		{a,b}{c,d}
> 		output=	ab ad bc bd
>
> Example 3:
> 		input=	 {xyz}a{b,c}
> 		output= xyzab xyzac
>
> TestCases:
> case =1
> input ={a,b,c,d}e{x,y,z}
> output =aex aey aez bex bey bez cex cey cez dex dey dez 
>
> case =2
> input ={ab,cd}x{y,z}
> output =abxy abxz cdxy cdxz
>
> case =3
> input =abcd{x,y,z}f
> output =abcdxf abcdyf abcdzf
>
> case =4
> input ={abc}{d,e}f{g,h,i}j
> output =abcdfgj abcdfhj abcdfij abcefgj abcefhj abcefij
>
> case =5
> input =abcdef
> output =abcdef
>
> case =6
> input =abc{e,f}j{k,l}i{g,h}
> output =abcejkig abcejkih abcejlig abcejlih abcfjkig abcfjkih abcfjlig abcfjlih
>  */
>
> import java.util.*;
>
> public class BraceExpression {
> 	public static  String[] expand(String S) {
> 		// TreeSet to sort
>         TreeSet<String> set = new TreeSet<>();
>         if (S.length() == 0) {
>             return new String[]{""}; 
>         } else if (S.length() == 1) {
>             return new String[]{S};
>         }
>         if (S.charAt(0) == '{') {
>             int i = 0; // keep track of content in the "{content}"
>             while (S.charAt(i) != '}') {
>                 i++;
>             }
>             String sub = S.substring(1, i);
>             String[] subs = sub.split(",");
>             String[] strs = expand(S.substring(i + 1)); // dfs
>             for (int j = 0; j < subs.length; j++) {
>                 for (String str : strs) {
>                     set.add(subs[j] + str);
>                 }
>             }
>         } else {
>             String[] strs = expand(S.substring(1));
>             for (String str : strs) {
>                 set.add(S.charAt(0) + str);
>             }
>         }
>         return set.toArray(new String[0]);
>     }
>
> 	 public static void main(String args[] ) {
> 			 Scanner sc = new Scanner(System.in);
> 		     String str=sc.next();
> 		     System.out.println(Arrays.deepToString(expand(str)));
> 	}	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%205%20Solutions/BraceExpression.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 5 Solutions/BraceExpression.java
