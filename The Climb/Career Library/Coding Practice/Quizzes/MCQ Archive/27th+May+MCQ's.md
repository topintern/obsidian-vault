---
kind: "study-reference"
title: "27th+May+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/27th+May+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 27th+May+MCQ's

[[The Climb/Career Library/Career Library]]

1)

#include "stdio.h" 
int main() 
{ 
    char arr[100]; 
    printf("%d", scanf("%s", arr)); 
    /* Suppose that input value given 
        for above scanf is "welcome" */
    return 1; 
} 

(A) 9
(B) 1
(C) 10
(D) 100















Answer: (B)



2)

#include <stdio.h> 
int foo(int* a, int* b) 
{ 
    int sum = *a + *b; 
    *b = *a; 
    return *a = sum - *b; 
} 
int main() 
{ 
    int i = 0, j = 1, k = 2, l; 
    l = i++ || foo(&j, &k); 
    printf("%d %d %d %d", i, j, k, l); 
    return 0; 
} 

(A) 1 2 1 1
(B) 1 1 2 1
(C) 1 2 2 1
(D) 1 2 2 2







Answer: (A)


3)
#include <stdio.h> 
#define PRINT(i, limit) do \ 
                        { \ 
                            if (i++ < limit) \ 
                            { \ 
                                printf("hello\n"); \ 
                                continue; \ 
                            } \ 
                        }while(0) 
  
int main() 
{ 
    int i = 0; 
    PRINT(i, 3); 
    return 0; 
} 

How many times "hello" is printed in the above program ?
(A) 1
(B) 3
(C) 4
(D) Compile-time error








Answer: (A)



4)

In below program, what would you put in place of “?” to print "welcome"?
#include <stdio.h> 
int main()  
{  
  char arr[] = "hellowelcome";  
  printf("%s", ?);  
  return 0;  
} 

(A) arr
(B) (arr+5)
(C) (arr+4)
(D) Not possible











Answer: (B)




5)
output of the following code in C Programming Language 

#include<stdio.h> 
struct Graph 
{ 
  int x, y, z; 
}; 
  
int main() 
{ 
  struct Graph p1 = {.y = 0, .z = 1, .x = 2}; 
  printf("%d %d %d", p1.x, p1.y, p1.z); 
  return 0; 
} 

(A) Compiler Error
(B) 2 0 1
(C) 0 1 2
(D) 2 1 0






Answer: (B)



6)

#include <iostream> 
using namespace std; 
  
class B; 
class A { 
    int a; 
public: 
    A():a(0) { } 
    void show(A& x, B& y); 
}; 
  
class B { 
private: 
    int b; 
public: 
    B():b(0) { } 
    friend void A::show(A& x, B& y); 
}; 
  
void A::show(A& x, B& y) { 
    x.a = 10; 
    cout << "A::a=" << x.a << " B::b=" << y.b; 
} 
  
int main() { 
    A a; 
    B b; 
    a.show(a,b); 
    return 0; 
} 

(A) Compiler Error
(B) A::a=10 B::b=0
(C) A::a=0 B::b=0
(D) None of these


Answer: (B)




7)
#include<iostream> 
   
using namespace std; 
class P { 
public: 
   void print()  { cout <<" Inside P"; } 
}; 
   
class Q : public P { 
public: 
   void print() { cout <<" Inside Q"; } 
}; 
   
class R: public Q { }; 
   
int main(void) 
{ 
  R r;  
  r.print(); 
  return 0; 
} 

(A) Inside P
(B) Inside Q
(C) Compiler Error: Ambiguous call to print()
(D) None of these



Answer: (B)


8)Which of the following is true about new when compared with malloc.

1) new is an operator, malloc is a function
2) new calls constructor, malloc doesn’t
3) new returns appropriate pointer, malloc returns void * and pointer needs to typecast to appropriate type.

(A) 1 and 3
(B) 2 and 3
(C) 1 and 2
(D) All 1, 2 and 3


Answer: (D)



9)Given the basic ER and relational models, which of the following is INCORRECT?

(A) An attribute of an entity can have more than one value
(B) An attribute of an entity can be composite
(C) In a row of a relational table, an attribute can have more than one value
(D) In a row of a relational table, an attribute can have exactly one value or a NULL value


Answer: (C)



10)
Which of the following statements are TRUE about an SQL query?
P : An SQL query can contain a HAVING clause even if it does not have a GROUP BY clause
Q : An SQL query can contain a HAVING clause only if it has a GROUP BY clause
R : All attributes used in the GROUP BY clause must appear in the SELECT clause
S : Not all attributes used in the GROUP BY clause need to appear in the SELECT clause

(A) P and R
(B) P and S
(C) Q and R
(D) Q and S


Answer: (B)



11)

Table A
Id   Name    Age
----------------
12   Arun    60
15   Shreya  24
99   Rohit   11


Table B
Id   Name   Age
----------------
15   Shreya  24
25   Hari    40
98   Rohit   20
99   Rohit   11


Table C
Id   Phone  Area
-----------------
10   2200   02  
99   2100   01

Consider the above tables A, B and C. How many tuples does the result of the following SQL query contains?

SELECT A.id 
FROM   A 
WHERE  A.age > ALL (SELECT B.age 
                    FROM   B 
                    WHERE  B. name = "arun") 

(A) 4
(B) 3
(C) 0
(D) 1


Answer: (B)

Explanation: 
The meaning of “ALL” is the A.Age should be greater than all the values returned by the subquery. 
There is no entry with name “arun” in table B. So the subquery will return NULL. 
If a subquery returns NULL, then the condition becomes true for all rows of A (See this for details). 
So all rows of table A are selected.




12)

Given:
1. public class TestOne {
2. public static void main (String[] args) throws Exception {
3. Thread.sleep(3000);
4. System.out.println("sleep");
5. }
6. }

What is the result?
A. Compilation fails.
B. An exception is thrown at runtime.
C. The code executes normally and prints "sleep".
D. The code executes normally, but nothing is printed.

Answer: C


13)
Given:

11. String test = "a1b2c3";
12. String[] tokens = test.split("\\d");
13. for(String s: tokens) System.out.print(s + " ");
What is the result?

A. a b c
B. 1 2 3
C. a1b2c3
D. a1 b2 c3
E. Compilation fails.
F. The code runs with no output.
G. An exception is thrown at runtime.

Answer: A



14) Given:

1. import java.util.*;
2. public class WrappedString {
3. private String s;
4. public WrappedString(String s) { this.s = s; }
5. public static void main(String[] args) {
6. HashSet<Object> hs = new HashSet<Object>();
7. WrappedString ws1 = new WrappedString("aardvark");
8. WrappedString ws2 = new WrappedString("aardvark");
9. String s1 = new String("aardvark");
10. String s2 = new String("aardvark");
11. hs.add(ws1); hs.add(ws2); hs.add(s1); hs.add(s2);
12. System.out.println(hs.size()); } }

What is the result?
A. 0
B. 1
C. 2
D. 3
E. 4
F. Compilation fails.
G. An exception is thrown at runtime.

Answer: D




15)The elements 32, 15, 20, 30, 12, 25, 16 are inserted one by one in the given order into a Max Heap. 

The resultant Max Heap if printed in  Level Order is 


A)32 30 25 15 12 20 16
B)32 25 30 12 15 20 16
C) 32 30 25 15 12 16 20
D) 32 25 30 12 15 16 20



Explanation:

32, 15, 20, 30, 12, 25, 16 

After insertion of 32, 15 and 20
          32
        /    \
      15      20
 
After insertion of 30
          32
        /    \
      15      20
     /
    30
Max Heap property is violated, so 30 is swapped with 15
          32
        /    \
      30      20
     /
    15

After insertion of 12
          32
        /    \
      30      20
     /  \
    15  12

After insertion of 25
          32
        /    \
      30      20
     /  \     /
    15  12   25

Max Heap property is violated, so 25 is swapped with 20
          32
        /    \
      30      25
     /  \     /
    15  12   20


After insertion of 16
          32
        /    \
      30      25
     /  \     /  \
    15  12   20  16 


Ans-A




16)The most appropriate matching for the following pairs

X: depth first search			1: heap
Y: breadth-first search		2: queue
Z: sorting					3: stack

is 

(A) X—1 Y—2 Z-3
(B) X—3 Y—1 Z-2
(C) X—3 Y—2 Z-1
(D) X—2 Y—3 Z-1


Answer: (C)



17)The average number of key comparisons done in a successful sequential search in a list of length it is
(A) log n
(B) (n-1)/2
(C) n/2
(D) (n+1)/2


Answer: (D)
Just say if you have to find a given element in sequential search,

It can be found in first try, then 1 comparison is required similarly...total comparisons can be 1+2+...+n = n(n+1)/2

Avg will be n(n+1)/2 divided by n ( total elements ) = n+1/2


18) The feature of the object oriented paradigm which helps code reuse is _______ .


(A). Object
(B). Class
(C). Inheritance
(D). Aggregation.


Answer: (C)




19) A  good structured design has low cohesion and high coupling arrangements.


a. True
b. False
c.  Depends on the Application you are working
d.  None of these

ANSWER: b



20) Interaction Diagram is a combined term for

a) Sequence Diagram + Collaboration Diagram
b) Activity Diagram + State Chart Diagram
c) Deployment Diagram + Collaboration Diagram
d) None of the mentioned


Answer: a

Explanation: Interaction diagram are used to formalize the dynamic behavior of the system. 

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/27th%2BMay%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/27th+May+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
