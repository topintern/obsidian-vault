---
kind: "coding-problem"
title: "Solve Equation (Day 48)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 48 Solutions/SolveEquation.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Solve Equation (Day 48)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Solve a given equation and return the value of x in the form of string "x=#value". 
 The equation contains only '+', '-' operation, the variable x and its coefficient.

If there is no solution for the equation, return "No solution".

If there are infinite solutions for the equation, return "Infinite solutions".

If there is exactly one solution for the equation, we ensure that the value of x is an integer.

Example 1:
Input: x+5-3+x=6+x-2
Output: "x=2"
Example 2:
Input: x=x
Output: "Infinite solutions"
Example 3:
Input: 2x=x
Output: "x=0"
Example 4:
Input: 2x+3x-6x=x+2
Output: "x=-1"
Example 5:
Input: x=x+2
Output: "No solution"

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · SolveEquation.java
> ```java
> /*
>  * 
>  Solve a given equation and return the value of x in the form of string "x=#value". 
>  The equation contains only '+', '-' operation, the variable x and its coefficient.
>
> If there is no solution for the equation, return "No solution".
>
> If there are infinite solutions for the equation, return "Infinite solutions".
>
> If there is exactly one solution for the equation, we ensure that the value of x is an integer.
>
> Example 1:
> Input: x+5-3+x=6+x-2
> Output: "x=2"
> Example 2:
> Input: x=x
> Output: "Infinite solutions"
> Example 3:
> Input: 2x=x
> Output: "x=0"
> Example 4:
> Input: 2x+3x-6x=x+2
> Output: "x=-1"
> Example 5:
> Input: x=x+2
> Output: "No solution"
>
>  */
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.Arrays;
>
> public class SolveEquation {
>
> 	  public static String coeff(String x) {
> 	        if (x.length() > 1 && x.charAt(x.length() - 2) >= '0' && x.charAt(x.length() - 2) <= '9')
> 	            return x.replace("x", "");
> 	        return x.replace("x", "1");
> 	    }
> 	    public static String solveEquation(String equation) {
> 	        String[] lr = equation.split("=");
> 	        int lhs = 0, rhs = 0;
> 	        for (String x: lr[0].split("(?=\\+)|(?=-)")) {
> 	            if (x.indexOf("x") >= 0) {
>
> 	                lhs += Integer.parseInt(coeff(x));
> 	            } else
> 	                rhs -= Integer.parseInt(x);
> 	        }
> 	        for (String x: lr[1].split("(?=\\+)|(?=-)")) {
> 	            if (x.indexOf("x") >= 0)
> 	                lhs -= Integer.parseInt(coeff(x));
> 	            else
> 	                rhs += Integer.parseInt(x);
> 	        }
> 	        if (lhs == 0) {
> 	            if (rhs == 0)
> 	                return "Infinite solutions";
> 	            else
> 	                return "No solution";
> 	        } else
> 	            return "x=" + rhs / lhs;
> 	    }
> 	    
> 	    public static void main(String args[] ) throws IOException {
>
> 		    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 			String equation = br.readLine();
>
> 			System.out.println(solveEquation(equation));   
> 			
> 			}
> }
>
>
> /*
> =======Testcases=======
> case =1
> input =x+5-3+x=6+x-2
> output ="x=2"
>
> case =2
> input =x=x
> output ="Infinite solutions"
>
> case =3
> inputut	=2x=x
> output ="x=0"
>
> case =4
> input =2x+3x-6x=x+2
> output	="x=-1"
>
> case =5
> input =x=x+2
> output ="No solution"
>
> case =6
> input =7x+5x-7=3x+8x-4
> output ="x=3"
>
> case =7
> input =8x-7x+15x-9x=3x+5x+4
> output ="x=-4"
>
> case =8
> input =8x-7x+15x-9x=2x+5x+4
> output ="No solution"
>
> case =9
> input =x+34=7x-56x+44
> output ="x=0"
>
> case =10
> input =x-x=x-x
> output ="Infinite solutions"
>
> */
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2048%20Solutions/SolveEquation.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 48 Solutions/SolveEquation.java
