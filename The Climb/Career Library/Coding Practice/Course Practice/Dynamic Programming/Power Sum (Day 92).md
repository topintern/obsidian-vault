---
kind: "coding-problem"
title: "Power Sum (Day 92)"
collection: "Course Practice"
topic: "Dynamic Programming"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 92 Solutions/PowerSum.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Power Sum (Day 92)

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

> [!example]- Reference 1 · PowerSum.java
> ```java
> import java.util.Scanner;
>
> public class PowerSum {
> 	int count=0;
> 	int sum;
> 	int pow;
>     public static void main(String[] args) {
> 		Scanner in=new Scanner(System.in);
> 		int x=in.nextInt();
> 		int n=in.nextInt();
>         PowerSum p=new PowerSum();
>         p.sum=x;
>         p.pow=n;
>         int N=(int)Math.pow(x, (1.0/n));
>         p.getcount(p.sum,N,true);
>         p.getcount(p.sum,N,false);
>         System.out.println(p.count);
>         in.close();
> 	}
>     void getcount(int sum1,int n,boolean lenyani){
>     	
>     	if(lenyani==true){
>     		sum1=sum1-(int)Math.pow(n, pow);
>     	
>     	}
>     	if(sum1<0) return;
>     	if(sum1==0){
>     		count++;
>     		return;
>     	}
>     	if(n==1) return;
>     	getcount(sum1,n-1,true);
>     	getcount(sum1,n-1,false);
>     }
>  
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2092%20Solutions/PowerSum.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 92 Solutions/PowerSum.java
