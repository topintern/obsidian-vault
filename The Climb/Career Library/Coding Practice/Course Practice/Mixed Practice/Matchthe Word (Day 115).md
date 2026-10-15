---
kind: "coding-problem"
title: "Matchthe Word (Day 115)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 115 Solutions/MatchtheWord.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Matchthe Word (Day 115)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Madhu is given strings, Word W and Pattern P.
W contains only lowercase letters, P contains lowercase letters and $, *.

In the pattern:
'$' indicates any single lowercase letter.
'*' indicates zero more number of lowercase letters.

Madhu's task is to find out, whether Pattern is matching the complete Word or not.
If pattern match the complete word, print true.
Otherwise false.

Input Format:
-------------
Two strings, Word and Pattern

Output Format:
--------------
Print the boolean result


Sample Input-1:
---------------
aa *

Sample Output-1:
----------------
true


Sample Input-2:
---------------
cb $a

Sample Output-2:
----------------
false


Sample Input-3:
---------------
abcde a*d*

Sample Output-3:
----------------
true


Sample Input-4:
---------------
acdcb a*c$b

Sample Output-4:
----------------
false

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · MatchtheWord.java
> ```java
> /*
> Madhu is given strings, Word W and Pattern P.
> W contains only lowercase letters, P contains lowercase letters and $, *.
>
> In the pattern:
> '$' indicates any single lowercase letter.
> '*' indicates zero more number of lowercase letters.
>
> Madhu's task is to find out, whether Pattern is matching the complete Word or not.
> If pattern match the complete word, print true.
> Otherwise false.
>
> Input Format:
> -------------
> Two strings, Word and Pattern
>
> Output Format:
> --------------
> Print the boolean result
>
>
> Sample Input-1:
> ---------------
> aa *
>
> Sample Output-1:
> ----------------
> true
>
>
> Sample Input-2:
> ---------------
> cb $a
>
> Sample Output-2:
> ----------------
> false
>
>
> Sample Input-3:
> ---------------
> abcde a*d*
>
> Sample Output-3:
> ----------------
> true
>
>
> Sample Input-4:
> ---------------
> acdcb a*c$b
>
> Sample Output-4:
> ----------------
> false
>
> */
>
> import java.util.*;
>
> class MatchtheWord {
> 	boolean isMatch(String word, String pattern) {
>         int s = 0, p = 0, match = 0, starIdx = -1;            
>         while (s < word.length()){
>             // advancing both pointers
>             if (p < pattern.length()  && (pattern.charAt(p) == '$' || word.charAt(s) == pattern.charAt(p))){
>                 s++;
>                 p++;
>             }
>             // * found, only advancing pattern pointer
>             else if (p < pattern.length() && pattern.charAt(p) == '*'){
>                 starIdx = p;
>                 match = s;
>                 p++;
>             }
>            // last pattern pointer was *, advancing string pointer
>             else if (starIdx != -1){
>                 p = starIdx + 1;
>                 match++;
>                 s = match;
>             }
>            //current pattern pointer is not star, last patter pointer was not *
>           //characters do not match
>             else return false;
>         }
>         
>         //check for remaining characters in pattern
>         while (p < pattern.length() && pattern.charAt(p) == '*')
>             p++;
>         
>         return p == pattern.length();
> 	}
> 	
> 	public static void main(String args[])
> 	{
> 		Scanner sc= new Scanner(System.in);
> 		String w=sc.next();
> 		String p=sc.next();
> 		System.out.println(new MatchtheWord().isMatch(w,p));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%20115%20Solutions/MatchtheWord.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 115 Solutions/MatchtheWord.java
