---
kind: "study-reference"
title: "3rd+June+MCQ's+without+answers"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/3rd+June+MCQ's+without+answers.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 3rd+June+MCQ's+without+answers

[[The Climb/Career Library/Career Library]]

1)
what is the following function fun(int x, int y) calculate  in  C?


int fun(int x, int y) 
{ 
    if (y == 0)   return 0; 
    return (x + fun(x, y-1)); 
} 

(A) x + y
(B) x + x*y
(C) x*y
(D) xy

ans:C




2) What does the following C expression do? x = (x<<1) + x + (x>>1);

(A) Multiplies an integer with 7
(B) Multiplies an integer with 3.5
(C) Multiplies an integer with 3
(D) Multiplies an integer with 8

ans:B


3)Suppose there are 11 items in sorted order in an array. 

How many searches are required on the average, if binary search is employed and all searches are successful in finding the item?

(A) 3.00
(B) 3.46
(C) 2.81
(D) 3.33



4)

Suppose that we have numbers between 1 and 1000 in a binary search tree and we want to search for the number 365. 

Which of the following sequences could not be the sequence of nodes examined ?
(A) 4, 254, 403, 400, 332, 346, 399, 365
(B) 926, 222, 913, 246, 900, 260, 364, 365
(C) 927, 204,913, 242, 914, 247, 365
(D) 4, 401, 389, 221, 268, 384, 383, 280, 365







5)

Assuming int size is 4 bytes, what is going to happen when we compile and run the following program?

#include<stdio.h>
int main() 
{ 
  printf("hello\n"); 
  main(); 
  return 0; 
} 

(A) We can’t use main() inside main() and compiler will catch it by showing compiler error.
(B) hello would be printed in 2147483647 times i.e. (2 to the power 31) – 1.
(C) It’ll print hello infinite times i.e. the program will continue to run forever until it’s terminated by other means such as CTRL+C or CTRL+Z etc.
(D) hello would be printed only once. Because when main() is used inside main(), it’s ignored by compiler at run time. 
     This is to make sure that main() is called only once.
(E) hello would be printed until stack overflow happens for this program.






6)Suppose a, b, c and d are int variables. For ternary operator in C ( ? : ), pick the best statement.

(A) a>b ? : ; is valid statement i.e. 2nd and 3rd operands can be empty and they are implicitly replaced with non-zero value at run-time.
(B) a>b ? c=10 : d=10; is valid statement. Based on the value of a and b, either c or d gets assigned the value of 10.
(C) a>b ? (c=10,d=20) : (c=20,d=10); is valid statement. Based on the value of a and b, either c=10,d=20 gets executed or c=20,d=10 gets executed.
(D) All of the above are valid statements for ternary operator.





7)
Anyone of the followings can be used to declare a node for a singly linked list.

If we use the first declaration, “struct node * nodePtr;” would be used to declare pointer to a node. 
If we use the second declaration, “NODEPTR nodePtr;” can be used to declare pointer to a node.

/* First declaration */
struct node { 
int data; 
struct node * nextPtr; 
}; 
  
/* Second declaration */
typedef struct node{ 
int data; 
NODEPTR nextPtr; 
} * NODEPTR; 

(A) TRUE
(B) FALSE
(C) Based on the Application 
(D) None of these




8) Output of the following in CPP

#include <iostream> 
using namespace std; 
  
int main() 
{ 
    try
    { 
        try
        { 
            throw 20; 
        } 
        catch (int n) 
        { 
            cout << "Inner Catch\n"; 
            throw; 
        } 
    } 
    catch (int x) 
    { 
        cout << "Outer Catch\n"; 
    } 
    return 0; 
} 

(A) Outer Catch

(B) Inner Catch

(C)
Inner Catch
Outer Catch

(D) Compiler Error






9)Which of the following is true about templates in CPP

1) Template is a feature of C++ that allows us to write one code for different data types.
2) We can write one function that can be used for all data types including user defined types. Like sort(), max(), min(), ..etc.
3) We can write one class or struct that can be used for all data types including user defined types. Like Linked List, Stack, Queue ..etc.
4) Template is an example of compile time polymorphism.

(A) 1 and 2
(B) 1, 2 and 3
(C) 1, 2 and 4
(D) 1, 2, 3 and 4






10) 

Can destructors be virtual in C++?
(A) Yes
(B) No
(C) compiler dependent
(D) None of these 









11)How can we make a C++ class such that objects of it can only be created using new operator?

If user tries to create an object directly, the program produces compiler error.

(A) Not possible
(B) By making destructor private
(C) By making constructor private
(D) By making both constructor and destructor private




12)

Given:

1. public class Electronic implements Device
{ public void doIt() { } }
2.
3. abstract class Phone1 extends Electronic { }
4.
5. abstract class Phone2 extends Electronic
{ public void doIt(int x) { } }
6.
7. class Phone3 extends Electronic implements Device
{ public void doStuff() { } }
8.
9. interface Device { public void doIt(); }

What is the result? (Choose all that apply.)
A. Compilation succeeds
B. Compilation fails with an error on line 1
C. Compilation fails with an error on line 3
D. Compilation fails with an error on line 5
E. Compilation fails with an error on line 7
F. Compilation fails with an error on line 9




13)

Given:
public abstract interface Frobnicate { public void twiddle(String s); }

Which is a correct class? (Choose all that apply.)

A. public abstract class Frob implements Frobnicate {
public abstract void twiddle(String s) { }
}

B. public abstract class Frob implements Frobnicate { }

C. public class Frob extends Frobnicate {
public void twiddle(Integer i) { }
}

D. public class Frob implements Frobnicate {
public void twiddle(Integer i) { }
}

E. public class Frob implements Frobnicate {
public void twiddle(String i) { }
public void twiddle(Integer s) { }
}





14)Given:
class Top {
public Top(String s) { System.out.print("B"); }
}
public class Bottom2 extends Top {
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





15)

In the relational model, cardinality is termed as:
(A) A number of tuples. 
(B) A number of attributes.
(C) A number of tables.
(D) A number of constraints.






16)The database schema is written in
(A) HLL 
(B) DML
(C) DDL
(D) DCL






17)You want to retrieve all employees, whether or not they have matching departments in the departments table. 

Which query would you use?

A) SELECT last_name, department_name
FROM employees e LEFT OUTER
JOIN departments d ON (e.department_id = d.department_id);

B) SELECT last_name, department_name
FROM employees e RIGHT OUTER
JOIN departments d ON (e.department_id = d.department_id);

C) SELECT last_name, department_name
FROM employees e FULL OUTER
JOIN departments d ON (e.department_id = d.department_id);


D) None of these







18)
which among the following is a static relationship

a) association
b) subtypes
c) cloning
d) all of these






19) which among the following represent ths relationship between instances of  a classes 

a) conceptual
b) association
c) specification
d) implementation




20) Which of the following term is best defined by the statement:

”a structural relationship that specifies that objects of one thing are connected to objects of another”?

a) Association
b) Aggregation
c) Realization
d) Generalization



## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/3rd%2BJune%2BMCQ's%2Bwithout%2Banswers.txt) · CODING RESOURCES/Quiz Mcqs/3rd+June+MCQ's+without+answers.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
