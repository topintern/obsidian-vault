---
kind: "coding-problem"
title: "play-game (Day 84)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 84 Solutions/play-game-English.pdf","CODING RESOURCES/ELITE FS COMPLETE/Day 84 Solutions/PlayGame.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# play-game (Day 84)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

********TestCases***********

case =1
input =10
963 446 52 677 817 609 996 312 927 634
output =3385

case =2
input =10
457 779 102 440 551 142 683 185 668 277
output =2348

case =3
input =10
446 24 708 709 385 852 240 259 922 535
output =2565

case =4
input =10
515 21 621 169 559 418 877 356 924 294
output =2808

case =5
input =10
213 883 302 330 420 447 632 917 43 601
output =2897

case =6
input =10
886 952 584 564 802 846 507 69 420 4
output =3418

case =7
input =10
321 386 740 595 161 176 606 64 577 316
output =2293

case =8
input =10
267 744 264 372 943 683 506 607 504 441
output =2892

case =9
input =10
3 559 416 40 263 747 634 135 817 34
output =2494

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · PlayGame.java
> ```java
> /*
>
> *********TestCases***********
>
> case =1
> input =10
> 963 446 52 677 817 609 996 312 927 634
> output =3385
>
> case =2
> input =10
> 457 779 102 440 551 142 683 185 668 277
> output =2348
>
> case =3
> input =10
> 446 24 708 709 385 852 240 259 922 535
> output =2565
>
> case =4
> input =10
> 515 21 621 169 559 418 877 356 924 294
> output =2808
>
> case =5
> input =10
> 213 883 302 330 420 447 632 917 43 601
> output =2897
>
> case =6
> input =10
> 886 952 584 564 802 846 507 69 420 4
> output =3418
>
> case =7
> input =10
> 321 386 740 595 161 176 606 64 577 316
> output =2293
>
> case =8
> input =10
> 267 744 264 372 943 683 506 607 504 441
> output =2892
>
> case =9
> input =10
> 3 559 416 40 263 747 634 135 817 34
> output =2494
>
> */
>
> import java.io.BufferedReader;
> import java.io.InputStreamReader;
> import java.util.Arrays;
> import java.util.StringTokenizer;
>
>
> public class PlayGame {
> 	
> 	static Long f[];
> 	static Long g[];
> 	
> 	static int n;
> 	static int a[];
>
> 	static long F(int i) {
> 		if (i >= n) return 0;
> 		if (f[i] != null) return f[i];
> 		
> 		f[i] = 0L;
> 		f[i] = Math.max(f[i], a[i] + G(i + 1));
> 		if (i + 1 < n) f[i] = Math.max(f[i], a[i] + a[i + 1] + G(i + 2));
> 		if (i + 2 < n) f[i] = Math.max(f[i], a[i] + a[i + 1] + a[i + 2] + G(i + 3));
> 		
> 		return f[i];
> 	}
> 	
> 	static long G(int i) {
> 		if (i >= n) return 0;
> 		if (g[i] != null) return g[i];
> 		
> 		g[i] = Long.MAX_VALUE;
> 		g[i] = Math.min(g[i], F(i + 1));
> 		g[i] = Math.min(g[i], F(i + 2));
> 		g[i] = Math.min(g[i], F(i + 3));
> 		
> 		return g[i];
> 	}
> 	
> 	public static void main(String[] args) throws Exception {
> 		BufferedReader cin = new BufferedReader(new InputStreamReader(System.in));
> 		StringTokenizer token = new StringTokenizer(cin.readLine());
> 		for (int T=Integer.parseInt(token.nextToken()); T>0; T--) {
> 			n = Integer.parseInt(cin.readLine());
> 			a = new int[n];
> 			token = new StringTokenizer(cin.readLine());
> 			for (int i=0; i<n; i++) a[i] = Integer.parseInt(token.nextToken());
> 			
> 			f = new Long[n];
> 			g = new Long[n];
> 			System.out.println(F(0));
> 		}
> 		
> 		cin.close();
> 	}
>
> }
> ```

## Original problem files

- [[The Climb/Career Library/_Attachments/Coding Practice/play-game-English-450098d1.pdf|play-game-English-450098d1.pdf]]

![[The Climb/Career Library/_Attachments/Coding Practice/play-game-English-450098d1.pdf#height=420]]

## Source provenance

- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2084%20Solutions/play-game-English.pdf) · CODING RESOURCES/ELITE FS COMPLETE/Day 84 Solutions/play-game-English.pdf
- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2084%20Solutions/PlayGame.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 84 Solutions/PlayGame.java
