---
kind: "study-reference"
title: "4th+June+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/4th+June+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 4th+June+MCQ's

[[The Climb/Career Library/Career Library]]

1)

In the following program snippet, both s1 and s2 would be variables of structure
type defined as below and there won’t be any compilation issue.

typedef struct Student 
{ 
 int rollno; 
 int total; 
} Student; 
  
Student s1; 
struct Student s2; 

(A) TRUE
(B) FALSE
(C) Compiler Dependent
(D) None of these

















Answer: (A)

Explanation: At first, it may seem that having same ‘struct tag name’ and
‘typedef name’ would cause issue here. 
But it’s perfectly fine for both of them having same name. s1 is defined using
typedef name Student while s2 is defined using struct tag name Student.



2)
#include<stdio.h> 
  
int foo(int a) 
{ 
 printf("%d",a); 
 return 0; 
} 
  
int main() 
{ 
 foo; 
 return 0; 
} 

(A) It’ll result in compile error because foo is used without parentheses.
(B) No compile error and some garbage value would be passed to foo function. This would make foo to be executed with output “garbage integer”.
(C) No compile error but foo function wouldn’t be executed. The program wouldn’t print anything.
(D) No compile error and ZERO (i.e. 0) would be passed to foo function. This would make foo to be executed with output 0.






Answer: (C)

Explanation: 
In C, if a function name is used without parentheses, 
the reference to the function name simply generates a pointer to the function,
which is then discarded. 
So the above program would compile but won’t print anything.


3)Suppose someone writes increment macro (i.e. which increments the value by one) in following ways:

#define INC1(a) ((a)+1) 
  
#define INC2 (a) ((a)+1) 
  
#define INC3( a ) (( a ) + 1) 
  
#define INC4 ( a ) (( a ) + 1) 

Pick the correct statement for the above macros.
(A) Only INC1 is correct.
(B) All (i.e. INC1, INC2, INC3 and INC4) are correct.
(C) Only INC1 and INC3 are correct.
(D) Only INC1 and INC2 are correct.


Answer: (C)

Explanation: 

In C, for macros with arguments, there can’t be any space between macro name and open parenthesis. 
That’s why only INC1 and INC3 are correct. 
Basically, "#define INC2 (a) ((a)+1)" results in "INC2" expansion to "(a) ((a)+1)" which is not the desired expansion.




4)The average case occurs in the Linear Search Algorithm when:

(A) The item to be searched is in some where middle of the Array
(B) The item to be searched is not in the array
(C) The item to be searched is in the last of the array
(D) The item to be searched is either in the last or not in the array













Answer: (A)



5)
Consider the following code snippet for checking whether a number is power of 2 or not.

/* Incorrect function to check if x is power of 2*/

bool isPowerOfTwo (unsigned int x)  
{  
  return (!(x&(x-1)));  
}

What is wrong with above function?

(A) It does reverse of what is required
(B) It works perfectly fine for all values of x.
(C) It does not work for x = 0
(D) It does not work for x = 1







Answer: (C)



6)What does fun2() do in general?

int fun(int x, int y) 
{ 
    if (y == 0)   return 0; 
    return (x + fun(x, y-1)); 
} 
  
int fun2(int a, int b) 
{ 
    if (b == 0) return 1; 
    return fun(a, fun2(a, b-1)); 
} 

(A) x*y
(B) x+x*y
(C) x^y
(D) y^x





Answer: (C)

Explanation: The function multiplies x to itself y times which is x^y.



7)
Which of the following concepts provides facility of using object of one class inside another class?
A.	Encapsulation	
B.	Abstraction
C.	Composition
D.	Inheritance














Ans:- C



8)The pre-order and post order traversal of a Binary Tree generates the same output. The tree can have maximum

(A) Three nodes 		
(B) Two nodes
(C) One node
(D) Any number of nodes












Ans:C



9)

#include<iostream>
using namespace std;

int operate (int a, int b)
{
  return (a * b);
}

float operate (float a, float b)
{
  return (a/b);
}

int main()
{
    int x=5, y=2;
    float n=5.0, m=2.0;
    cout << operate(x,y) <<"\t";
		cout << operate (n,m);
		return 0;
}
 
a.       10.0      5.0
b.      5.0         2.5
c.       10.0      5
d.      10         2.5
e.      Compile Time Error Ambiguity in Function Call














Ans:- d




10)Given:
class Clidder {
private final void flipper() { System.out.println("Clidder"); }
}
public class Clidlet extends Clidder {
public final void flipper() { System.out.println("Clidlet"); }
public static void main(String [] args) {
new Clidlet().flipper();
} }
What is the result?
A. Clidlet
B. Clidder
C. Clidder
Clidlet
D. Clidlet
Clidder
E. Compilation fails





Answer:
A is correct. Although a final method cannot be overridden, in this case, the method
is private, and therefore hidden. The effect is that a new, accessible, method flipper is
created. Therefore, no polymorphism occurs in this example, the method invoked is simply
that of the child class, and no error occurs.



11)Which statement(s) are true? (Choose all that apply.)

A. Cohesion is the OO principle most closely associated with hiding implementation details

B. Cohesion is the OO principle most closely associated with making sure that classes know
about other classes only through their APIs

C. Cohesion is the OO principle most closely associated with making sure that a class is
designed with a single, well-focused purpose

D. Cohesion is the OO principle most closely associated with allowing a single object to be
seen as having many types












Answer:
Answer C is correct.



12)

Given the following,
1. class X { void do1() { } }
2. class Y extends X { void do2() { } }
3.
4. class Chrome {
5. public static void main(String [] args) {
6. X x1 = new X();
7. X x2 = new Y();
8. Y y1 = new Y();
9. // insert code here
10. }
11. }

Which, inserted at line 9, will compile? (Choose all that apply.)
A. x2.do2();
B. (Y)x2.do2();
C. ((Y)x2).do2();
D. None of the above statements will compile










Answer:
C is correct. 
Before you can invoke Y’s do2 method you have to cast x2 to be of type Y.
Statement B looks like a proper cast but without the second set of parentheses, 
the compiler thinks it’s an incomplete statement.



13)Given:

1. ClassA has a ClassD
2. Methods in ClassA use public methods in ClassB
3. Methods in ClassC use public methods in ClassA
4. Methods in ClassA use public variables in ClassB

Which is most likely true? (Choose the most likely.)

A. ClassD has low cohesion
B. ClassA has weak encapsulation
C. ClassB has weak encapsulation
D. ClassB has strong encapsulation
E. ClassC is tightly coupled to ClassA








Answer:
C is correct. 
Generally speaking, public variables are a sign of weak encapsulation.
A, B, D, and E are incorrect, because based on the information given, 
none of these statements can be supported.





14)Given:

3. class Dog {
4. public void bark() { System.out.print("woof "); }
5. }
6. class Hound extends Dog {
7. public void sniff() { System.out.print("sniff "); }
8. public void bark() { System.out.print("howl "); }
9. }
10. public class DogShow {
11. public static void main(String[] args) { new DogShow().go(); }
12. void go() {
13. new Hound().bark();
14. ((Dog) new Hound()).bark();
15. ((Dog) new Hound()).sniff();
16. }
17. }

What is the result? (Choose all that apply.)
A. howl howl sniff
B. howl woof sniff
C. howl howl followed by an exception
D. howl woof followed by an exception
E. Compilation fails with an error at line 14
F. Compilation fails with an error at line 15








Answer:
F is correct. Class Dog doesn’t have a sniff method.




15)

Given:

3. public class Redwood extends Tree {
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
A is correct, 
a ClassCastException will be thrown when the code attempts to downcast a Tree to a Redwood.



16)

You have run an SQL statement that asked the DBMS to display data in a table named USER_TABLES. 
The results include columns of data labeled "TableName," "NumberOfColumns" and "PrimaryKey." 

You are looking at ________ .

A.user data.
B.Metadata
C.A report
D.indexes





Ans-B



17)

Which of the following is NOT a type of SQL constraint?

A.PRIMARY KEY
B.ALTERNATE KEY
C.UNIQUE
D.FOREIGN KEY









Ans-B




18)

In the description of a class, a protected operation is shown by 
A.  -
B.  +
C.  #
D.?





Answer: C


19).

In a class, a public operation is shown by 
A.  -
B.  +
C.  #
D.?








Answer: B



20)

Which view addresses the performance, scalability and throughput of the system?

A. Use Case
B. Design
C. Process 
D. Implementation








Answer: C

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/4th%2BJune%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/4th+June+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
