---
kind: "coding-problem"
title: "Lunchbox (Day 57)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 57 Solutions/Lunchbox.java"]
practice_status: "not-started"
last_practiced: null
source_solution_available: true
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Lunchbox (Day 57)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source description and tests

St. Martins School has decided to run a trial for a system that supplies the students 
with packed lunch boxes for lunchtime.

The system is designed as follows:
There are N premade lunch boxes for N Students, and they are placed on top of each other. 
The lunch boxes can be either in Rectangle shape or Circle in shape. 
Each student has his/her own preference for the type of lunchbox that they want. 
There are the correct number of circular and rectangular lunch boxes 
to satisy each student .

The Students stand in a random ordered line as soon as it is lunch time. 
If the student at the head of the line finds that the top tiffin in the stack is not of their 
preference they will go back and rejoin the queue at the end.

Estimate the number of students who will  not be able to eat lunch.

Input format:
Input1 : N, denoting the number of Children and lunch boxes. 
Input2 : An array of N elements, each element can be either 0(Rectangle) or 
1(circle) denoting the type of lunch box from top to bottom. 
Input3 : An array of N elements, each element denoting the preference 
0(Rectangle) or 1(Circle) of a student from 
the start till end of the queue.


Output Format: 
For the given input your code should output the number of students who will not be able to eat lunch

Sample Input1
4 - Number of children and lunch boxes
0 0 1 0 - Types of lunch boxes
1 0 0 0 - Preferences of a student 
Output1
0

Sample Input2
6
0 1 1 0 1 0
1 1 1 0 1 0
output2
1


========= Testcases Program-2 =========
case =1
input =6
0 1 1 0 1 0
1 1 1 0 1 0
output =1

case =2
input =4
0 0 1 0
1 0 0 0
output =0

case =3
input =8
1 0 0 1 0 0 1 0
0 0 0 1 0 0 0 1
output =2

case =4
input =15
1 0 1 1 1 0 1 0 1 1 1 0 1 1 0
0 0 0 0 0 0 1 0 1 1 1 1 1 1 1
output =3

case =5
input =12
1 1 1 0 1 0 1 1 1 0 1 1
1 1 0 1 0 0 0 1 0 0 1 0
output =5

case =6
input =18
0 0 0 1 1 0 1 1 1 0 1 0 0 1 0 1 1 0
0 0 0 1 1 0 1 0 1 0 1 1 0 1 1 0 0 0
output =2

case =7
input =10
1 0 1 0 0 1 1 1 0 1
0 0 1 0 1 0 0 0 0 1
output =4

case =8
input =15
0 1 1 1 0 0 0 0 1 1 0 1 0 1 0
0 0 1 0 0 1 0 1 0 1 0 1 0 1 1
output =0

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Reference solutions

These are imported source solutions, not verified answers or completed practice.

> [!example]- Reference 1 · Lunchbox.java
> ```java
> /*
> St. Martins School has decided to run a trial for a system that supplies the students 
> with packed lunch boxes for lunchtime.
>
> The system is designed as follows:
> There are N premade lunch boxes for N Students, and they are placed on top of each other. 
> The lunch boxes can be either in Rectangle shape or Circle in shape. 
> Each student has his/her own preference for the type of lunchbox that they want. 
> There are the correct number of circular and rectangular lunch boxes 
> to satisy each student .
>
> The Students stand in a random ordered line as soon as it is lunch time. 
> If the student at the head of the line finds that the top tiffin in the stack is not of their 
> preference they will go back and rejoin the queue at the end.
>
> Estimate the number of students who will  not be able to eat lunch.
>
> Input format:
> Input1 : N, denoting the number of Children and lunch boxes. 
> Input2 : An array of N elements, each element can be either 0(Rectangle) or 
> 1(circle) denoting the type of lunch box from top to bottom. 
> Input3 : An array of N elements, each element denoting the preference 
> 0(Rectangle) or 1(Circle) of a student from 
> the start till end of the queue.
>
>
> Output Format: 
> For the given input your code should output the number of students who will not be able to eat lunch
>
> Sample Input1
> 4 - Number of children and lunch boxes
> 0 0 1 0 - Types of lunch boxes
> 1 0 0 0 - Preferences of a student 
> Output1
> 0
>
> Sample Input2
> 6
> 0 1 1 0 1 0
> 1 1 1 0 1 0
> output2
> 1
>
>
> ========= Testcases Program-2 =========
> case =1
> input =6
> 0 1 1 0 1 0
> 1 1 1 0 1 0
> output =1
>
> case =2
> input =4
> 0 0 1 0
> 1 0 0 0
> output =0
>
> case =3
> input =8
> 1 0 0 1 0 0 1 0
> 0 0 0 1 0 0 0 1
> output =2
>
> case =4
> input =15
> 1 0 1 1 1 0 1 0 1 1 1 0 1 1 0
> 0 0 0 0 0 0 1 0 1 1 1 1 1 1 1
> output =3
>
> case =5
> input =12
> 1 1 1 0 1 0 1 1 1 0 1 1
> 1 1 0 1 0 0 0 1 0 0 1 0
> output =5
>
> case =6
> input =18
> 0 0 0 1 1 0 1 1 1 0 1 0 0 1 0 1 1 0
> 0 0 0 1 1 0 1 0 1 0 1 1 0 1 1 0 0 0
> output =2
>
> case =7
> input =10
> 1 0 1 0 0 1 1 1 0 1
> 0 0 1 0 1 0 0 0 0 1
> output =4
>
> case =8
> input =15
> 0 1 1 1 0 0 0 0 1 1 0 1 0 1 0
> 0 0 1 0 0 1 0 1 0 1 0 1 0 1 1
> output =0
>  
>  */
> import java.util.*;
>
> public class Lunchbox {
> 	
> 	public static void main(String args[]) {
> 		Scanner sc = new Scanner(System.in);
> 		int num = sc.nextInt();
> 		Queue<Integer> studentsPref = new LinkedList<>();
> 		Queue<Integer> lunch = new LinkedList<Integer>(); 
> 		for (int i = 0; i < num; i++) {
> 			lunch.add(sc.nextInt());
> 		}
> 		for (int i = 0; i < num; i++) {
> 			studentsPref.add(sc.nextInt());
> 		}
>
> 		int i = 0, j = 0;
> 		while (i < num) {
> 			j = 0;
> 			while (j < studentsPref.size()) {
> 				if (lunch.peek() != studentsPref.peek()) {
> 					int temp = studentsPref.poll();
> 					studentsPref.add(temp);
> 				} else {
> 					lunch.poll();
> 					studentsPref.poll();
> 					break;
> 				}
> 				j++;
> 			}
> 			i++;
> 		}
> 		System.out.println(studentsPref.size());
> 	}
> }
> ```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2057%20Solutions/Lunchbox.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 57 Solutions/Lunchbox.java
