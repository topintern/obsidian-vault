---
kind: "coding-problem"
title: "Screen Fitting (Day 97)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 97 Solutions/ScreenFitting.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Screen Fitting (Day 97)

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

> [!example]- Reference 1 · ScreenFitting.java
> ```java
> import java.util.Scanner;
>
> class ScreenFitting
> {
> 	static int wordsTyping(String[] sentence, int rows, int cols) {
>         int[] nextIndex = new int[sentence.length];
>         int[] times = new int[sentence.length];
>         for(int i=0;i<sentence.length;i++) {
>             int curLen = 0;
>             int cur = i;
>             int time = 0;
>             while(curLen + sentence[cur].length() <= cols) {
>                 curLen += sentence[cur++].length()+1;
>                 if(cur==sentence.length) {
>                     cur = 0;
>                     time ++;
>                 }
>             }
>             nextIndex[i] = cur;
>             times[i] = time;
>         }
>         int ans = 0;
>         int cur = 0;
>         for(int i=0; i<rows; i++) {
>             ans += times[cur];
>             cur = nextIndex[cur];
>         }
>         return ans;
>     }
> 		
> 	public static void main(String args[]){
> 	Scanner sc=new Scanner(System.in);
> 	int r=sc.nextInt();
> 	int c=sc.nextInt();
> 	sc.nextLine();
> 	String S=sc.nextLine();
> 	
> 	System.out.println(wordsTyping(S.split(" "), r,c));
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2097%20Solutions/ScreenFitting.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 97 Solutions/ScreenFitting.java
