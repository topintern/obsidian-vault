---
kind: "coding-problem"
title: "Remove Interval (Day 12)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Elite Day 12 Solutions/RemoveInterval.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Remove Interval (Day 12)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

Given a sorted list of disjoint intervals, each interval intervals[i] = [a, b] 
represents the set of real numbers x such that a <= x < b.

We remove the intersections between any interval in intervals and the interval toBeRemoved.

Return a sorted list of intervals after all such removals.

Example 1:
	Input=	3
				0 2
				3 4
				5 7
				1 6
	Output=[[0, 1], [6, 7]]

Example 2:
	Input=	1
				0 5
				2 3
	Output=[[0, 2], [3, 5]]


----TestCase----
case =1
input =4
10 15
17 25
29 40
43 55
20 35
output =[[10, 15], [17, 20], [35, 40], [43, 55]]

case =2
input =6
10 15
17 25
29 40
43 55
56 65
72 90
75 85
output =[[10, 15], [17, 25], [29, 40], [43, 55], [56, 65], [72, 75], [85, 90]]

case =3
input =5
10 15
29 40
43 55
56 65
72 90
15 25
output =[[10, 15], [29, 40], [43, 55], [56, 65], [72, 90]]

case =4
input =5
1 4
5 7
8 11
12 15
16 20
6 16
output =[[1, 4], [5, 6], [16, 20]]

case =5
input =5
2 4
5 7
8 11
12 15
16 19
1 20
output =[]

case =6
input =5
10 20
30 40
50 60
70 80
90 100
25 75
output =[[10, 20], [75, 80], [90, 100]]

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · RemoveInterval.java
> ```java
> /*
>  * 
> Given a sorted list of disjoint intervals, each interval intervals[i] = [a, b] 
> represents the set of real numbers x such that a <= x < b.
>
> We remove the intersections between any interval in intervals and the interval toBeRemoved.
>
> Return a sorted list of intervals after all such removals.
>
> Example 1:
> 	Input=	3
> 				0 2
> 				3 4
> 				5 7
> 				1 6
> 	Output=[[0, 1], [6, 7]]
>
> Example 2:
> 	Input=	1
> 				0 5
> 				2 3
> 	Output=[[0, 2], [3, 5]]
>
>
> ----TestCase----
> case =1
> input =4
> 10 15
> 17 25
> 29 40
> 43 55
> 20 35
> output =[[10, 15], [17, 20], [35, 40], [43, 55]]
>
> case =2
> input =6
> 10 15
> 17 25
> 29 40
> 43 55
> 56 65
> 72 90
> 75 85
> output =[[10, 15], [17, 25], [29, 40], [43, 55], [56, 65], [72, 75], [85, 90]]
>
> case =3
> input =5
> 10 15
> 29 40
> 43 55
> 56 65
> 72 90
> 15 25
> output =[[10, 15], [29, 40], [43, 55], [56, 65], [72, 90]]
>
> case =4
> input =5
> 1 4
> 5 7
> 8 11
> 12 15
> 16 20
> 6 16
> output =[[1, 4], [5, 6], [16, 20]]
>
> case =5
> input =5
> 2 4
> 5 7
> 8 11
> 12 15
> 16 19
> 1 20
> output =[]
>
> case =6
> input =5
> 10 20
> 30 40
> 50 60
> 70 80
> 90 100
> 25 75
> output =[[10, 20], [75, 80], [90, 100]]
>  
> */
>
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.*;
>
> public class RemoveInterval {
> 	
> 	public static List<List<Integer>> removeInterval(int[][] intervals, int[] toBeRemoved) {
> 	    int removeStart = toBeRemoved[0], removeEnd = toBeRemoved[1];
> 	    List<List<Integer>> output = new ArrayList<List<Integer>>();
>
> 	    for (int[] interval : intervals) {
> 	      int start = interval[0], end = interval[1];
>
> 	      if (end <= removeStart || start >= removeEnd) {
> 	        // if current interval ends before toBeRemoved
> 	        // or starts after
> 	        output.add(new ArrayList<Integer>() {{add(start); add(end); }});
>
> 	      } else if (start < removeStart && end > removeEnd) {
> 	        // if the interval to be removed is inside 
> 	        // of the current interval
> 	        output.add(new ArrayList<Integer>() {{add(start); add(removeStart); }});
> 	        output.add(new ArrayList<Integer>() {{add(removeEnd); add(end); }});
>
> 	      } else if (start < removeStart && end <= removeEnd) {
> 	        // "left" overlap
> 	        output.add(new ArrayList<Integer>() {{add(start); add(removeStart); }});
>
> 	      } else if (start >= removeStart && end > removeEnd) {
> 	        // "right" overlap
> 	        output.add(new ArrayList<Integer>() {{add(removeEnd); add(end); }});
> 	      }
> 	    }
> 	    return output;
> 	  }
> 	
> 	
> 	public static void main(String args[] ) throws IOException {
> 		 BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 			String str ;
> 			String[] numbers;
> 			
> 			int n=Integer.parseInt(br.readLine());      
> 			int[][] intervals=new int[n][3];
>
> 		       for(int i=0; i<n; i++)
> 		       {
> 		    	   str = br.readLine();
> 		    	   numbers = str.split(" ");
> 		    	   intervals[i]=Arrays.asList(numbers).stream().mapToInt(Integer::parseInt).toArray();
> 		       }
> 		       str = br.readLine();
> 	    	   numbers = str.split(" ");
> 	    	   int removed[]=Arrays.asList(numbers).stream().mapToInt(Integer::parseInt).toArray(); 
>
> 		       System.out.println(removeInterval(intervals,removed));
> 	}
>
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Elite%20Day%2012%20Solutions/RemoveInterval.java) · CODING RESOURCES/ELITE FS COMPLETE/Elite Day 12 Solutions/RemoveInterval.java
