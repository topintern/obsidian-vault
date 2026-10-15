---
kind: "coding-problem"
title: "Parallel Courses (Day 14)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 14 Solutions/ParallelCourses.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Parallel Courses (Day 14)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

There are N courses, labelled from 1 to N.

We are given relations[i] = [X, Y], representing a prerequisite relationship between course X and course Y: course X has to be studied before course Y.

In one semester you can study any number of courses as long as you have studied all the prerequisites for the course you are studying.

Return the minimum number of semesters needed to study all courses.  If there is no way to study all the courses, return -1.

 

Example 1:



Input:3
2
1 3
2 3
Output: 2

### Explanation: 

In the first semester, courses 1 and 2 are studied. In the second semester, course 3 is studied.
Example 2:



Input:3
3
1 2
2 3
3 1
Output: -1

### Explanation: 

No course can be studied because they depend on each other.

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · ParallelCourses.java
> ```java
> /*
>  * 
>  *
>  There are N courses, labelled from 1 to N.
>
> We are given relations[i] = [X, Y], representing a prerequisite relationship between course X and course Y: course X has to be studied before course Y.
>
> In one semester you can study any number of courses as long as you have studied all the prerequisites for the course you are studying.
>
> Return the minimum number of semesters needed to study all courses.  If there is no way to study all the courses, return -1.
>
>  
>
> Example 1:
>
>
>
> Input:3
> 2
> 1 3
> 2 3
> Output: 2
> Explanation: 
> In the first semester, courses 1 and 2 are studied. In the second semester, course 3 is studied.
> Example 2:
>
>
>
> Input:3
> 3
> 1 2
> 2 3
> 3 1
> Output: -1
> Explanation: 
> No course can be studied because they depend on each other.
>
>
>  */
>
> package Elite2020;
>
> import java.io.BufferedReader;
> import java.io.IOException;
> import java.io.InputStreamReader;
> import java.util.*;
>
> public class ParallelCourses {
> 	
> 	 public static  int minimumSemesters(int N, int[][] relations) {
> 	        Map<Integer, List<Integer>> g = new HashMap<>(); // key: prerequisite, value: course list. 
> 	        int[] inDegree = new int[N + 1]; // inDegree[i]: number of prerequisites for i.
> 	        for (int[] r : relations) {
> 	            g.computeIfAbsent(r[0], l -> new ArrayList<>()).add(r[1]); // construct graph.
> 	            ++inDegree[r[1]]; // count prerequisites for r[1].
> 	        }
> 	        Queue<Integer> q = new LinkedList<>(); // save current 0 in-degree vertices.
> 	        for (int i = 1; i <= N; ++i)
> 	            if (inDegree[i] == 0)
> 	                q.offer(i);
> 	        int semester = 0;
> 	        while (!q.isEmpty()) { // BFS traverse all currently 0 in degree vertices.
> 	            for (int sz = q.size(); sz > 0; --sz) { // sz is the search breadth.
> 	                int c = q.poll();
> 	                --N;
> 	                if (!g.containsKey(c)) continue; // c's in-degree is currently 0, but it has no prerequisite.
> 	                for (int course : g.remove(c))
> 	                    if (--inDegree[course] == 0) // decrease the in-degree of course's neighbors.
> 	                        q.offer(course); // add current 0 in-degree vertex into Queue.
> 	            }
> 	            ++semester; // need one more semester.
> 	        }
> 	        return N == 0 ? semester : -1;
> 	    }
>
> 	 
> 	 public static void main(String args[] ) throws IOException {
> 		 BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>
> 			String str ;
> 			String[] rel;
> 		    int courses,nrelations;
> 		    courses = Integer.parseInt(br.readLine());
> 			nrelations=Integer.parseInt(br.readLine());
> 			int[][] relations=new int[nrelations][2];
>
> 		       for(int i=0; i<nrelations; i++)
> 		       {
> 		    	   str = br.readLine();
> 		    	   rel = str.split(" ");
> 		    	   relations[i]=Arrays.asList(rel).stream().mapToInt(Integer::parseInt).toArray();
> 		       }
> 		       
>
> 	    	   
> 		       System.out.println(minimumSemesters(courses,relations));
> 	}
> 	 
> 	 
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2014%20Solutions/ParallelCourses.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 14 Solutions/ParallelCourses.java
