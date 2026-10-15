---
kind: "study-reference"
title: "29th+May+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/29th+May+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 29th+May+MCQ's

[[The Climb/Career Library/Career Library]]


1)

#include <stdio.h> 
  
int main() 
{ 
    int *ptr; 
    int x; 
  
    ptr = &x; 
    *ptr = 0; 
  
    printf(" x = %d\n", x); 
    printf(" *ptr = %d\n", *ptr); 
  
    *ptr += 5; 
    printf(" x  = %d\n", x); 
    printf(" *ptr = %d\n", *ptr); 
  
    (*ptr)++; 
    printf(" x = %d\n", x); 
    printf(" *ptr = %d\n", *ptr); 
  
    return 0; 
} 

(A) 
x = 0
*ptr = 0
x = 5
*ptr = 5
x = 6
*ptr = 6

(B) 
x = garbage value
*ptr = 0
x = garbage value
*ptr = 5
x = garbage value
*ptr = 6

(C)
x = 0
*ptr = 0
x = 5
*ptr = 5
x = garbage value
*ptr = garbage value

(D) 
x = 0
*ptr = 0
x = 0
*ptr = 0
x = 0
*ptr = 0


Answer: (A)



2)
#include <stdio.h> 
  
void print(int n, int j) 
{ 
   if (j >= n) 
      return; 
   if (n-j > 0 && n-j >= j) 
       printf("%d %d\n", j, n-j); 
   print(n, j+1); 
} 
  
int main() 
{ 
    int n = 8; 
    print(n, 1); 
} 

(A) 
1 7
2 6
3 5
4 4
4 4

(B)
1 7
2 6
3 5
4 4

(C)
1 7
2 6
3 5

(D)
1 2
3 4
5 6
7 8


Answer: (B)


3)

Consider the following recursive function fun(x, y). 

What is the value of fun(4, 3)

int fun(int x, int y)  
{ 
  if (x == 0) 
    return y; 
  return fun(x - 1,  x + y); 
}  

(A) 13
(B) 12
(C) 9
(D) 10


Answer: (A)



4)

What is the other name of Dijkstra algorithm?
(A) single-source shortest path problem
(B) multiple-source shortest path problem
(C) multiple-destination shortest path problem
(D) single-destination shortest path problem


Answer: (A)




5)

Consider the following pseudo code. Assume that IntQueue is an integer queue. 
What does the function fun do?

void fun(int n) 
{ 
    IntQueue q = new IntQueue(); 
    q.enqueue(0); 
    q.enqueue(1); 
    for (int i = 0; i < n; i++) 
    { 
        int a = q.dequeue(); 
        int b = q.dequeue(); 
        q.enqueue(b); 
        q.enqueue(a + b); 
        print(a); 
    } 
} 

(A) Prints numbers from 0 to n-1
(B) Prints numbers from n-1 to 0
(C) Prints first n Fibonacci numbers
(D) Prints first n Fibonacci numbers in reverse order.


Answer: (C)

Explanation: 
The function prints first n Fibonacci Numbers. 
Note that 0 and 1 are initially there in q. 
In every iteration of loop sum of the two queue items is enqueued and the front item is dequeued.



6)
#include <stdio.h> 
  
  int main (void) 
  { 
  int shifty; 
  shifty = 0570; 
  shifty = shifty >>4; 
  shifty = shifty <<6; 
  printf("the value of shifty is %o",shifty); 
  } 

(A) the value of shifty is 15c0
(B) the value of shifty is 4300
(C) the value of shifty is 5700
(D) the value of shifty is 2700


Answer: (D)

Explanation: Given, shifty = 0570; here shifty is a octal number as it starts with 0.

(0570)8 = (000 101 111 000)2

Right shift by 4 places:


shifty = shifty >>4;
shifty = (000 000 010 111)2

Left shift by 6 places:

shifty = shifty <<6
shifty = (010 111 000 000)2
       = (2700)8

So, option (D) is correct.




7)
#include<stdlib.h> 
#include<stdio.h> 
#include<iostream> 
  
using namespace std; 
  
class Test { 
    int x; 
public: 
    void* operator new(size_t size); 
    void operator delete(void*); 
    Test(int i) { 
        x = i; 
        cout << "Constructor called \n"; 
    } 
    ~Test() { cout << "Destructor called \n"; } 
}; 
  
  
void* Test::operator new(size_t size) 
{ 
    void *storage = malloc(size); 
    cout << "new called \n"; 
    return storage; 
} 
  
void Test::operator delete(void *p ) 
{ 
    cout<<"delete called \n"; 
    free(p); 
} 
  
int main() 
{ 
    Test *m = new Test(5); 
    delete m; 
    return 0; 
}

(A)

new called
Constructor called
delete called
Destructor called

(B)


new called
Constructor called
Destructor called
delete called

(C)

Constructor called
new called
Destructor called
delete called

(D)

Constructor called
new called
delete called
Destructor called


Answer: (B)


8)which of the following is a pure virtual function in CPP

A) void display() { }
B) virtual void display() { }
C) void display() = 0;
D) virtual void display() = 0;
C) abstract void display() = 0;


Ans - D



9) which of the following is considered as cascading input/output operators in CPP (Choose all that apply)

A) cin>>a>>b>>c
B) cout<<"hello"<<a<<endl;
C) Cascading operators are not supported in  CPP
D) cout<<a<<b<<c


Ans - A,B,D


10) 
In C++, const qualifier can be applied to

1) Member functions of a class
2) Function arguments
3) To a class data member which is declared as static
4) Reference variables

(A) Only 1, 2 and 3
(B) Only 1, 2 and 4
(C) All of these
(D) Only 1, 3 and 4


Answer: (C)




11)

Given the following class, which of the following is true? (Choose all that apply)

1: public class Snake {
2:
3: public void shed(boolean time) {
4:
5: if (time) {
6:
7: }
8: System.out.println(result);
9:
10: }
11: }

A. If String result = "done"; is inserted on line 2, the code will compile.
B. If String result = "done"; is inserted on line 4, the code will compile.
C. If String result = "done"; is inserted on line 6, the code will compile.
D. If String result = "done"; is inserted on line 9, the code will compile.
E. None of the above changes will make the code compile.

Ans-A,B



12)

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


Ans- A is correct;


13)
Given:
4. class Announce {
5. public static void main(String[] args) {
6. for(int __x = 0; __x < 3; __x++) ;
7. int #lb = 7;
8. long [] x [5];
9. Boolean []ba[];
10. enum Traffic { RED, YELLOW, GREEN };
11. }
12. }

What is the result? (Choose all that apply.)
A. Compilation succeeds
B. Compilation fails with an error on line 6
C. Compilation fails with an error on line 7
D. Compilation fails with an error on line 8
E. Compilation fails with an error on line 9
F. Compilation fails with an error on line 10

Answer:
C, D, and F are correct. Variable names cannot begin with a #, 
an array declaration can’t include a size without an instantiation, and 
enums can’t be declared within a method.
A, B, and E are incorrect based on the above information. 



14)

Given:
3. public class TestDays {
4. public enum Days { MON, TUE, WED };
5. public static void main(String[] args) {
6. for(Days d : Days.values() )
7. ;
8. Days [] d2 = Days.values();
9. System.out.println(d2[2]);
10. }
11. }

What is the result? (Choose all that apply.)

A. TUE
B. WED
C. The output is unpredictable
D. Compilation fails due to an error on line 4
E. Compilation fails due to an error on line 6
F. Compilation fails due to an error on line 8
G. Compilation fails due to an error on line 9


Answer:
B is correct. Every enum comes with a static values() method that returns an array
of the enum's values, in the order in which they are declared in the enum.

A, C, D, E, F, and G are incorrect based on the above information.




15)

What can UML interfaces be used for?

a) To provide concrete classes with the stereotype "interface"
b) To program in Java and C++, but not in C#
c) To define executable logic that can be reused in several classes
d) To specify required services for types of objects

ans- d


16) Inheritance relationships are represented in the UML notation by

a)  Lines with solid diamond at one end
b)  Lines with hollow diamond at one end
c)  Lines with hollow triangular arrow at one end
d)  Lines with solid triangular arrow at both ends

Ans - c) Lines with hollow triangular arrow at one end



17) Key elements of use-case diagrams are

a) People, computer
b) Actors, use cases
c) People, classes and objects
d)  Uses, cases

Ans  b) : Actors, use cases




18)Identify the correct statement regarding "view" in SQL

A) Views allow the same data to be seen by different users in different ways at the same time
B) Views can provice logical data independence
C) View provides automatic security for hidden data
D) All of these


Ans- D


19)Choose the correct order of operations in a SELECT statement

A) HAVING,GROUP BY, WHERE
B) WHERE,GROUP BY, HAVING
C) WHERE, HAVING, GROUP BY
D) HAVING, WHERE, GROUP BY


Ans- B


20) which of the following SQL command deletes all records from table but does not delete the table ?

A) DROP
B) REMOVE
C) ERASE
D) DELETE

Ans- D



## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/29th%2BMay%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/29th+May+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
