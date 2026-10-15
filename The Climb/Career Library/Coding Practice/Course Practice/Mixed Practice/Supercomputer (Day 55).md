---
kind: "coding-problem"
title: "Supercomputer (Day 55)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 55 Solutions/Supercomputer.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: false
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Supercomputer (Day 55)

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

> [!example]- Reference 1 · Supercomputer.txt
> ```java
> URL: https://www.hackerrank.com/challenges/two-pluses/problem
> /*
> Ema built a quantum computer! Help her test its capabilities by solving the problem below.
> Given a grid of size n*m, each cell in the grid is either good or bad.
>
> A valid plus is defined here as the crossing of two segments (horizontal and vertical) of equal lengths. 
> These lengths must be odd, and the middle cell of its horizontal segment must cross the middle cell of its vertical 
> segment.
>
> Find the two largest valid pluses that can be drawn on good cells in the grid, and return an integer 
> denoting the maximum product of their areas. In the above diagrams, our largest pluses have areas of 5 and 9.
> The product of their areas is 5*9=45.
>
> Note: The two pluses cannot overlap, and the product of their areas should be maximal.
>
> Input Format:
> 	- The first line contains two space-separated integers, n and m.
> 	- Each of the next  lines contains a string of  characters where each character is either G (good) or B (bad). 
> 	  These strings represent the rows of the grid. If the yth character in the xth line is G, then (x,y) is a good cell. 
> 	  Otherwise it's a bad cell.
>
> Output Format:
> 	Find 2 pluses that can be drawn on good cells of the grid, and return an integer denoting the maximum product of their areas.
>
> Sample Input-1
> 			5 6
> 			GGGGGG
> 			GBBBGB
> 			GGGGGG
> 			GGBBGB
> 			GGGGGG
> Sample Output -1
> 			5
>
> Sample Input-2
> 			6 6
> 			BGBBGB
> 			GGGGGG
> 			BGBBGB
> 			GGGGGG
> 			BGBBGB
> 			BGBBGB
> Sample Output-2
> 			25
> Explanation
> For the explanation below, we will refer to a plus of length i as Pi.
>
> Sample-1
> 	There is enough good space to color one P3 plus and one P1 plus. Area(P3)=5 and Area(P1)=1.
> 	The product of their areas is 5*1 = 1.
>
> Sample-2
> 	There is enough good space to color two P3 pluses. Area(P3)=5. 
> 	The product of the areas of our two P3 pluses is 5*5 = 25.
>
> ========= Testcases Program-2 =========
> case =1
> input =5 6
> GGGGGG
> GBBBGB
> GGGGGG
> GGBBGB
> GGGGGG
> output =5
>
> case =2
> input =6 6
> BGBBGB
> GGGGGG
> BGBBGB
> GGGGGG
> BGBBGB
> BGBBGB
> output =25
>
> case =3
> input =6 7
> GGGGGGG
> BGBBBBG
> BGBBBBG
> GGGGGGG
> GGGGGGG
> BGBBBBG
> output =5
>
> case =4
> input =7 7
> GBGBGGB
> GBGBGGB
> GBGBGGB
> GGGGGGG
> GGGGGGG
> GBGBGGB
> GBGBGGB
> output =45
>
> case =5
> input =8 8
> GGGGGGGG
> GBGBGGBG
> GBGBGGBG
> GGGGGGGG
> GBGBGGBG
> GGGGGGGG
> GBGBGGBG
> GGGGGGGG
> output =81
>
> case =6
> input =9 9
> BGBBBBBGB
> BGBBBBBGB
> GGGGGGGGG
> BGBBBBBGB
> GGGGGGGGG
> BGBBBBBGB
> GGGGGGGGG
> GGGGGGGGG
> BGBBBBBGB
> output =25
>
> case =7
> input =8 9
> GGGGGGGGG
> GBBBGGBGG
> GBBBGGBGG
> GBBBGGBGG
> GBBBGGBGG
> GBBBGGBGG
> GBBBGGBGG
> GGGGGGGGG
> output =1
>
> case =8
> input =7 7
> BBGGBGG
> GGGGGGG
> GGGGGGG
> BBGGBGG
> BBGGBGG
> GGGGGGG
> BBGGBGG
> output =45
>
> */
>
> import java.awt.Point;
> import java.io.*;
> import java.util.HashSet;
>
> public class Supercomputer {
> 	
> 	public static boolean check(int i,int j,int len1,int p,int q,int len2)
> 	{
> 		HashSet<Point> set=new HashSet<Point>();
> 		set.add(new Point(i,j));
> 		for(int x=1;x<=len1;x++)
> 		{
> 			set.add(new Point(i+x,j));
> 			set.add(new Point(i-x,j));
> 			set.add(new Point(i,j+x));
> 			set.add(new Point(i,j-x));
> 		}
> 		if(set.contains(new Point(p,q))) return true;
> 		for(int x=1;x<=len2;x++)
> 		{
> 			if(set.contains(new Point(p+x,q))) return true;
> 			if(set.contains(new Point(p-x,q))) return true;
> 			if(set.contains(new Point(p,q+x))) return true;
> 			if(set.contains(new Point(p,q-x))) return true;
> 		}
> 		return false;
> 	}
> 	
> 	public static void main(String[] args) throws NumberFormatException, IOException {
> 		BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
> 		BufferedWriter out = new BufferedWriter(new OutputStreamWriter(System.out));
> 		String str[]=in.readLine().split(" ");
> 		int N=Integer.parseInt(str[0]);
> 		int M=Integer.parseInt(str[1]);
> 		char arr[][]=new char[N][M];
> 		for(int i=0;i<N;i++) arr[i]=in.readLine().toCharArray();
> 		int square[][]=new int[N][M];
> 		for(int i=0;i<N;i++)
> 		{
> 			for(int j=0;j<M;j++)
> 			{
> 				for(int x=0;x<15;x++)
> 				{
> 					if(i-x<0||i+x>=N||j-x<0||j+x>=M) break;
> 					if(arr[i+x][j]=='G'&&arr[i-x][j]=='G'&&arr[i][j+x]=='G'&&arr[i][j-x]=='G') square[i][j]++;
> 					else break;
> 				}
> 			}
> 		}
> 		//for(int i=0;i<N;i++) System.out.println(Arrays.toString(square[i]));
> 		long max=0;
> 		for(int i=0;i<N;i++)
> 		{
> 			for(int j=0;j<M;j++)
> 			{
> 				for(int p=0;p<N;p++)
> 				{
> 					for(int q=0;q<M;q++)
> 					{
> 						if((i==p&&j==q)) continue;
> 						int len1=(square[i][j])-1;
> 						int len2=(square[p][q])-1;
> 						//System.out.println(len1+":"+len2);
> 						for(int l1=0;l1<=len1;l1++)
> 							for(int l2=0;l2<=len2;l2++)
> 							{
> 								if(!check(i,j,l1,p,q,l2))
> 								{
> 									//System.out.println(l1+":"+a2);
> 									int a1=4*l1+1;
> 									int a2=4*l2+1;
> 									max=Math.max(max, (long)a1*a2);
> 								}
> 							}
> 					}
> 				}
> 			}
> 		}
> 		out.write(max+"\n");
> 		out.flush();
> 	}
> }
> ```

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2055%20Solutions/Supercomputer.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 55 Solutions/Supercomputer.txt
