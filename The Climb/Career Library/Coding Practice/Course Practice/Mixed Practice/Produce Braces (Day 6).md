---
kind: "coding-problem"
title: "Produce Braces (Day 6)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day-6-Solutions/ProduceBraces.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Produce Braces (Day 6)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Write a Program to print all the combinations of  well-formed braces form the given no of
 pairs of braces.
 
 Note: Print List in Sorted Order(Ascending)
 
 input :2
Output: [AABB,ABAB]

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ProduceBraces.java
> ```java
> /*
>  * 
>  * 
>  * 
>  * 
>  * 
>
>  Write a Program to print all the combinations of  well-formed braces form the given no of
>  pairs of braces.
>  
>  Note: Print List in Sorted Order(Ascending)
>  
>  input :2
> Output: [AABB,ABAB]
>
>
>  */
>
> import java.util.*;
> public class ProduceBraces {
>
> 	    public static List<String> generateBarces(int n) {
> 	        List<String> ans = new ArrayList();
> 	        abGenerate(ans, "", 0, 0, n);
> 	        //Collections.sort(ans);
> 	        return ans;
> 	    }
>
> 	    public static void abGenerate(List<String> ans, String cur, int open, int close, int max){
> 	        if (cur.length() == max * 2) {
> 	            ans.add(cur);
> 	            return;
> 	        }
>
> 	        if (open < max)
> 	            abGenerate(ans, cur+"A", open+1, close, max);
> 	        if (close < open)
> 	            abGenerate(ans, cur+"B", open, close+1, max);
> 	    }
> 	    
> 	    public static void main(String args[] ) {
> 			 Scanner sc = new Scanner(System.in);
> 				int n=sc.nextInt();
>
> 			    System.out.println(generateBarces(n));
> 		}
> 	
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day-6-Solutions/ProduceBraces.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day-6-Solutions/ProduceBraces.java
