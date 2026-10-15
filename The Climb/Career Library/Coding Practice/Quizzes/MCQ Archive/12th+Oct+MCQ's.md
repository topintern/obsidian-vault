---
kind: "study-reference"
title: "12th+Oct+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/12th+Oct+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 12th+Oct+MCQ's

[[The Climb/Career Library/Career Library]]

1)
What is the value printed by the following C program?
#include<stdio.h>
int f(int * a, int n)
{
if (n<=0)return 0;
else if(*a%2==0) 
return *a+f(a+1,n-1);
else return * a-f(a+1, n-1);
}
int main ()
{
int a[]={12, 7, 13, 4, 11, 6};
printf("%d",f(a,6));
return 0;
}

(A) -9 	
(B) 5
(C) 15	
(D) 19









Ans:- C

2) void f(char *s)
{
char *s1;
char c;
s1=s+(strlen(s)-1);
while(s<s1)
	{
	 c=*s;
	 *s=*s1;
	 *s1=c;
	 s++;
	 s1--;
   printf("%s %s\n",s,s1);
	}
printf("%s %s",s,s1);
}
 
 main()
{
f("hello");
}

A)	hello hello
B)	hell hell
C)	leh leh
D)	olleh olleh
E)	None of these






Ans:- C

3)void main()
{
 int a=0xff;
 if(a<<4>>12)
	 printf("zemoso");
 else
	 printf("labs");
}

a)	zemoso
b)	labs
c)	Compilation error
d)	None of these





Ans:- B 

4)	
import java.util.*;
class Test {
public static void main(String[] args) {
// insert code here
x.add("one");
x.add("two");
x.add("TWO");
System.out.println(x.poll());
}
}
Which, inserted at // insert code here, will compile? (Choose all that apply.)
A. List<String> x = new LinkedList<String>();
B. TreeSet<String> x = new TreeSet<String>();
C. HashSet<String> x = new HashSet<String>();
D. Queue<String> x = new PriorityQueue<String>();
E. ArrayList<String> x = new ArrayList<String>();
F. LinkedList<String> x = new LinkedList<String>();





Answer:
D and F are correct. 

5)
4. public class Frodo extends Hobbit {
5. public static void main(String[] args) {
6. Short myGold = 7;
7. System.out.println(countGold(myGold, 6));
8. }
9. }
10. class Hobbit {
11. static int countGold(int x, int y) { return x + y; }
12. }


What is the result?
A. 13
B. Compilation fails due to multiple errors
C. Compilation fails due to an error on line 6
D. Compilation fails due to an error on line 7
E. Compilation fails due to an error on line 11




Ans- A

6)class Top 
{
public Top(String s) 
{ 
System.out.print("B"); 
}
}

public class Bottom2 extends Top 
{
public Bottom2(String s) { System.out.print("D"); }
public static void main(String [] args) {
new Bottom2("C");
System.out.println(" ");
} }
What is the result?
A. BD
B. DB
C. BDC
D. DBC
E. Compilation fails



Answer:
 E is correct. 



7) 3. public class Redwood extends Tree {
4. public static void main(String[] args) {
5. new Redwood().go();
6. }
7. void go() {
8. go2(new Tree(), new Redwood());
9. go2((Redwood) new Tree(), new Redwood());
10. }
11. void go2(Tree t1, Redwood r1) {
12. Redwood r2 = (Redwood)t1;
13. Tree t2 = (Tree)r1;
14. }
15. }
16. class Tree { }
What is the result? (Choose all that apply.)

A. An exception is thrown at runtime
B. The code compiles and runs with no output
C. Compilation fails with an error at line 8
D. Compilation fails with an error at line 9
E. Compilation fails with an error at line 12
F. Compilation fails with an error at line 13


Answer:
 A is correct

8)Given:
3. class Alpha {
4. static String s = " ";
5. protected Alpha() { s += "alpha "; }
6. }
7. class SubAlpha extends Alpha {
8. private SubAlpha() { s += "sub "; }
9. }
10. public class SubSubAlpha extends Alpha {
11. private SubSubAlpha() { s += "subsub "; }
12. public static void main(String[] args) {
13. new SubSubAlpha();
14. System.out.println(s);
15. }
16. }
What is the result?
A. subsub
B. sub subsub
C. alpha subsub
D. alpha sub subsub
E. Compilation fails
F. An exception is thrown at runtime

Answer:
 C is correct

9) When do we use a HAVING clause?
a) To limit the output of a query
b) To limit the output of a query using an aggregate function only
c) When GROUP by is used
d) both To limit the output of a query using an aggregate function and When GROUP by is used







Ans: b

10)Statment 1 :-    (INNER) JOIN: Returns records that have matching values in both tables
 Statment 2 :-     LEFT (OUTER) JOIN: Return all records from the left table, and the matched records from the right table
 Statment 3 :-     RIGHT (OUTER) JOIN: Return all records from the right table, and the matched records from the left table
 Statment 4 :-     FULL (OUTER) JOIN: Return all records when there is a match in either left or right table


A) Statement-1 is true, Statement 2,3,4 are false
B) Statement 1,2 is true, Statement 3,4 are false
C) Statement 1,2,3 is true , Statement 4 is false
D) Statement 1,2,3,4 are all true




Ans: D


11)
Given the following Managers Table 

Managers –
Id 	Name 	Salary
1 	Harpreet 	20000
2 	Ravi 		30000
3 	Vinay 	10000
4 	Ravi 		30000
5 	Harpreet 	20000
6 	Vinay 	10000
7 	Rajeev 	40000
8 	Vinay 	10000
9 	Ravi 		30000
10 	Sanjay 	50000

what will be the rows of the table after the following query is executed 

DELETE M1 
From managers M1, managers M2 
Where M2.Name = M1.Name AND M1.Id>M2.Id; 

A)
Id 	Name 	Salary
1 	Harpreet 	20000
2 	Ravi 		30000
3 	Vinay 	10000
7 	Rajeev 	40000
10 	Sanjay 	50000

B)
Id 	Name 	Salary
1 	Harpreet 	20000
2 	Ravi 		30000
3 	Vinay 	10000
4 	Ravi 		30000
5 	Harpreet 	20000
6 	Vinay 	10000
7 	Rajeev 	40000
8 	Vinay 	10000
9 	Ravi 		30000
10 	Sanjay 	50000

C) 
Id 	Name 	Salary
1 	Harpreet 	20000
2 	Ravi 		30000
4 	Ravi 		30000
5 	Harpreet 	20000
7 	Rajeev 	40000
9 	Ravi 		30000
10 	Sanjay 	50000

D)
Managers –
Id 	Name 	Salary
1 	Harpreet 	20000
3 	Vinay 	10000
5 	Harpreet 	20000
6 	Vinay 	10000
7 	Rajeev 	40000
8 	Vinay 	10000
10 	Sanjay 	50000



Ans-A

12)
Consider the following C program that attempts to locate an element x in an array Y[] using binary search. 

The program is erroneous. 

1.   f(int Y[10], int x) { 
2.     int i, j, k; 
3.     i = 0; j = 9; 
4.     do { 
5.             k =  (i + j) /2; 
6.             if( Y[k] < x)  i = k; else j = k; 
7.         } while(Y[k] != x && i < j); 
8.     if(Y[k] == x) printf ("x is in the array ") ; 
9.     else printf (" x is not in the array ") ; 
10. } 

On which of the following contents of Y and x does the program fail?

(A) Y is [1 2 3 4 5 6 7 8 9 10] and x < 10
(B) Y is [1 3 5 7 9 11 13 15 17 19] and x < 1
(C) Y is [2 2 2 2 2 2 2 2 2 2] and x > 2
(D) Y is [2 4 6 8 10 12 14 16 18 20] and 2 < x < 20 and x is even

Answer: (C)

Explanation: 
The above program doesn’t work for the cases where element to be searched is the last element of Y[] or greater than the last element (or maximum element) in Y[]. 
For such cases, program goes in an infinite loop because i is assigned value as k in all iterations, and i never becomes equal to or greater than j. 
So while condition never becomes false.

13)
Which of the following standard algorithms is not a Greedy algorithm?

(A) Dijkstra’s shortest path algorithm
(B) Prim’s algorithm
(C) Kruskal algorithm
(D) Huffman Coding
(E) Bellmen Ford Shortest path algorithm



Answer: (E)

14)
Which of the following sorting algorithms in its typical implementation gives best performance when applied on an array which is sorted or almost sorted 
(maximum 1 or two elements are misplaced).

(A) Quick Sort
(B) Heap Sort
(C) Merge Sort
(D) Insertion Sort




Answer: (D)

Explanation: Insertion sort takes linear time when input array is sorted or almost sorted (maximum 1 or 2 elements are misplaced).

15)
Given relations R(w,x) and S(y,z), the result of

SELECT DISTINCT w, x
FROM R, S

Is guaranteed to be same as R, if
(A) R has no duplicates and S is non-empty
(B) R and S have no duplicates
(C) S has no duplicates and R is non-empty
(D) R and S have the same number of tuples

Answer: (A)

Explanation: 
The query selects all attributes of r. 
Since we have distinct in query, result can be equal to r only if r doesn’t have duplicates.
If we do not give any attribute on which we want to join two tables, then the queries like above become equivalent to Cartesian product. 
Cartesian product of two sets will be empty if any of the two sets is empty. 
So, s should have atleast one record to get all rows of r.

So, option (A) is correct.

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/12th%2BOct%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/12th+Oct+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
