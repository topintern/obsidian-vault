---
kind: "coding-problem"
title: "Exp (Day 1)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 1/exp.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Exp (Day 1)

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

> [!example]- Reference 1 · exp.java
> ```java
> import java.util.*;
> import java.io.*;
>
>
> class exp{
> 	static int prec(char a)
> 	{
> 		if(a=='*' || a=='/')
> 		return 1;
> 	    else
> 	    return 0;
> 	}
> public static void main(String[] args) {
> 	Stack<Character> o=new Stack<Character>();
> 	Stack<Integer> n=new Stack<Integer>();
> 	String s;
> 	Scanner sc=new Scanner(System.in);
> 	s=sc.nextLine();
> 	int c=0;
>     for (int i=0;i<s.length() ;i++ ) {
>     	if(s.charAt(i)!=' ' && s.charAt(i)!='+'&& s.charAt(i)!='-' && s.charAt(i)!='*' && s.charAt(i)!='/' && s.charAt(i)!='(' && s.charAt(i)!=')')
>     	{
>     		c++;
>     		if(c>1)
>     		{
>               n.push(Integer.parseInt(String.valueOf(n.pop())+Character.toString(s.charAt(i))));
>     		}
>     		else
>     		n.push(Character.getNumericValue(s.charAt(i)));
>     	 
>
>
>         }
>         if(s.charAt(i)=='(')
>         {
>         	o.push(s.charAt(i));
>         }
>         if(s.charAt(i)==')')
>         {
>         	while(o.peek()!='(')
>         	{
>
>         		char a=o.pop();
>         		int q=n.pop();
>         		int p=n.pop();
>         		switch(a)
>         		{
>         			case '+':n.push((p+q));
>         			         break;
>         			case '-':n.push((p-q));
>         			         break;
>         			case '*':n.push((p*q));
>         			         break;
>         			case '/':n.push((p/q));
>         			         break;
>         		}
>
>         	}
>
>    
>         	o.pop();
>         	
>
>         }
>         if(s.charAt(i)=='+'||s.charAt(i)=='-'||s.charAt(i)=='*'||s.charAt(i)=='/')
>         {
>         	c=0;
>         	while(!o.isEmpty() && o.peek()!='(' && prec(s.charAt(i))<prec(o.peek()))
>         	{
>         		
>         		char a=o.pop();
>         		int q=n.pop();
>         		int p=n.pop();
>         		switch(a)
>         		{
>         			case '+':n.push((p+q));
>         			         break;
>         			case '-':n.push((p-q));
>         			         break;
>         			case '*':n.push((p*q));
>         			         break;
>         			case '/':n.push((p/q));
>         			         break;
>         		}
>         	
>
>         	}
>
>         	o.push(s.charAt(i));
>         }
>         
>        
>         }
>        
>     
> 	        while(!o.isEmpty())
>         {
>            char a=o.pop();
>         		
>         		int q=n.pop();
>         		int p=n.pop();
>         		
>         		switch(a)
>         		{
>         			case '+':n.push((p+q));
>         			         break;
>         			case '-':n.push((p-q));
>         			         break;
>         			case '*':n.push((p*q));
>         			         break;
>         			case '/':n.push((p/q));
>         			         break;
>         		}
>         		
>
> 	
>         }
>         System.out.println(n.pop());
>
>         
>         
> }
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%201/exp.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 1/exp.java
