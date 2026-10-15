---
kind: "coding-problem"
title: "Calculator (Day 3)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 3 Solutions/Calculator.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Calculator (Day 3)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Implement a basic calculator to evaluate a simple expression string.
The expression string may contain open ( and closing parentheses ) , 
the plus + or minus sign - , non-negative integers and empty spaces .

The expression string contains only non-negative integers, + , - , * , / operators,
open '(' and closing parentheses ')' and empty spaces . The integer division
should truncate toward zero.

You may assume that the given expression is always valid. 
All intermediate results will be in the range of [-2147483648, 2147483647] .

IO Format:
 Input Format:   A String S, contains the expression
 Output Format:  An integer, indicates the value of the expression

Example-1:
    input =  1 + 1
    output = 2

Example-2:
    input = 6-4 / 2 
    output = 4

Example-3:
input = 2*(5+5*2)/3+(6/2+8)
output = 21

Example-4:
    input = (2+6* 3+5- (3*14/7+2)*5)+3
    output = -12

Note: Do not use the 'eval' built-in library function.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Calculator.java
> ```java
> /*
> Implement a basic calculator to evaluate a simple expression string.
> The expression string may contain open ( and closing parentheses ) , 
> the plus + or minus sign - , non-negative integers and empty spaces .
>
> The expression string contains only non-negative integers, + , - , * , / operators,
> open '(' and closing parentheses ')' and empty spaces . The integer division
> should truncate toward zero.
>
> You may assume that the given expression is always valid. 
> All intermediate results will be in the range of [-2147483648, 2147483647] .
>
> IO Format:
>  Input Format:   A String S, contains the expression
>  Output Format:  An integer, indicates the value of the expression
>
> Example-1:
>     input =  1 + 1
>     output = 2
>
> Example-2:
>     input = 6-4 / 2 
>     output = 4
>
> Example-3:
> input = 2*(5+5*2)/3+(6/2+8)
> output = 21
>
> Example-4:
>     input = (2+6* 3+5- (3*14/7+2)*5)+3
>     output = -12
>
> Note: Do not use the 'eval' built-in library function.
>
>
> */
>
>
> import java.util.*;
>
> class  Calculator
> {
> 	public int calculate(String s) {
>         Stack<String> stack = new Stack<>();
>         s = s.replaceAll(" ", "").replaceAll("-2147483648", "+2147483647+1");
>         Converter converter = new Converter();
> 		
> 		//Converting into postfix
> 		String postfix = converter.convert(s);
>         for (String token : postfix.split(",")) {
>             if (!isOperator(token)) {
>                 stack.push(token);
>             } else {
>                 int i2 = Integer.valueOf(stack.pop());
>                 int i1 = Integer.valueOf(stack.pop());
>                 stack.push(String.valueOf(evaluate(i1, token, i2)));
>             }
>         }
>         return Integer.valueOf(stack.pop());
>     }
>
> 	// Check currect character is an operator or not 
>     private boolean isOperator(String s) {
>         return s.equals("+") || s.equals("-") || s.equals("*") || s.equals("/");
>     }
>
> 	// TO evaluate POSTFIX Expression
>     private int evaluate(int i1, String op, int i2) {
>         int ans = 0;
>         switch (op) {
>             case "+":
>                 ans = i1 + i2;
>                 break;
>             case "-":
>                 ans = i1 - i2;
>                 break;
>             case "*":
>                 ans = i1 * i2;
>                 break;
>             case "/":
>                 ans = (int) Math.floor((double) i1 / i2);
>                 break;
>         }
>         return ans;
>     }
>    
> 	//Converter for INFIX to POSTFIX Expression
> 	private static class Converter {
>         private final Map<Character, Integer> operators;
>
>         private Converter() {
>             operators = new HashMap<>();
>             operators.put('+', 1);
>             operators.put('-', 1);
>             operators.put('*', 2);
>             operators.put('/', 2);
>         }
>
>         private String convert(String s) {
>             Stack<Character> stack = new Stack<>();
>             int index = 0;
>             StringBuilder res = new StringBuilder();
>             while (index < s.length()) {
>                 int current = index;
>                 while (current < s.length() && Character.isDigit(s.charAt(current))) {
>                     current++;
>                 }
>                 if (index != current) {
>                     res.append(s.substring(index, current)).append(",");
>                 } else {
>                     char operator = s.charAt(current);
>                     if (operator == '(') {
>                         stack.push(operator);
>                     } else if (operator == ')') {
>                         while (!stack.isEmpty() && stack.peek() != '(') {
>                             res.append(stack.pop()).append(",");
>                         }
>                         stack.pop();
>                     } else {
>                         while (!stack.isEmpty() && operators.containsKey(stack.peek()) && operators.get(stack.peek()) >= operators.get(operator)) {
>                             res.append(stack.pop()).append(",");
>                         }
>                         stack.push(operator);
>                     }
>                     current++;
>                 }
>                 index = current;
>             }
>             while (!stack.isEmpty()) {
>                 res.append(stack.pop()).append(",");
>             }
>             return res.toString();
>         }
>     }
>
> 	public static void main(String args[])
>     {
> 		Scanner sc=new Scanner(System.in);
> 		String s=sc.nextLine();
> 		Calculator cl= new Calculator();
> 		System.out.println(cl.calculate(s));
>     }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%203%20Solutions/Calculator.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 3 Solutions/Calculator.java
