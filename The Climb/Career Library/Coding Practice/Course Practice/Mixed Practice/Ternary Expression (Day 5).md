---
kind: "coding-problem"
title: "Ternary Expression (Day 5)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 5 Solutions/TernaryExpression.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Ternary Expression (Day 5)

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

> [!example]- Reference 1 · TernaryExpression.java
> ```java
> import java.util.*;
> public class TernaryExpression {
> 	public static String parseTernary(String expression) {
> 	    if (expression == null || expression.length() == 0) return "";
>
> 	    Deque<Character> stack = new LinkedList<>();
>
> 	    for (int i = expression.length() - 1; i >= 0; i--) {
> 		char c = expression.charAt(i);
> 		if (!stack.isEmpty() && stack.peek() == '?') {
>
> 		    stack.pop(); //pop '?'
> 		    char first = stack.pop();
> 		    stack.pop(); //pop ':'
> 		    char second = stack.pop();
>
> 		    if (c == 'T') stack.push(first);
> 		    else stack.push(second);
> 		} 
> 		else {
> 		    stack.push(c);
> 		}
> 	    }
>
> 	    return String.valueOf(stack.peek());
> 	}
>
> 	public static void main(String args[] ) {
> 		 Scanner sc = new Scanner(System.in);
> 			String expression=sc.next();
> 		    System.out.println(parseTernary(expression));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%205%20Solutions/TernaryExpression.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 5 Solutions/TernaryExpression.java
