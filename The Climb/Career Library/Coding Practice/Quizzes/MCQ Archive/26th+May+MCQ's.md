---
kind: "study-reference"
title: "26th+May+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/26th+May+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 26th+May+MCQ's

[[The Climb/Career Library/Career Library]]

1)
#include <stdio.h> 
int main() 
{ 
    static int i=5; 
    if(--i){ 
        main(); 
        printf("%d ",i); 
    } 
} 

(A) 4 3 2 1
(B) 1 2 3 4
(C) 0 0 0 0
(D) Compiler Error


Answer: (C)



2)

The most appropriate matching for the following pairs (GATE CS 2000)

X: m=malloc(5); m= NULL;        1: using dangling pointers
Y: free(n); n->value=5;             2: using uninitialized pointers
Z: char *p; *p = ’a’;                  3. lost memory is:

(A) X—1 Y—3 Z-2
(B) (X—2 Y—1 Z-3
(C) X—3 Y—2 Z-1

(D) X—3 Y—1 Z-2


Answer: (D)


3)

#include <stdio.h> 
int fun(char *str1) 
{ 
  char *str2 = str1; 
  while(*++str1); 
  return (str1-str2); 
} 
  
int main() 
{ 
  char *str = "abcdefghi"; 
  printf("%d", fun(str)); 
  return 0; 
} 

(A) 10
(B) 9
(C) 8
(D) Random Number


Answer: (B)



4)

#include <stdio.h> 
int var = 20; 
int main() 
{ 
    int var = var; 
    printf("%d ", var); 
    return 0; 
} 

(A) Garbage Value
(B) 20
(C) Compiler Error
(D) None of these


Answer: (A)

Explanation: First var is declared, then value is assigned to it. As soon as var is declared as a local variable, it hides the global variable var.




5)
#include <stdio.h> 
struct sample { 
    int a = 0; 
    char b = 'A'; 
    float c = 10.5; 
}; 
int main() 
{ 
    struct sample s; 
    printf("%d, %c, %f", s.a, s.b, s.c); 
    return 0; 
} 


a) Error
b) 0, A, 10.5
c) 0, A, 10.500000
d) No Error, No Output


Answer: a

Explanation: Error: Can not initialize members here.



6)

#include<iostream> 
using namespace std; 
class Point { 
public: 
    Point() { cout << "Constructor called"; } 
}; 
  
int main() 
{ 
   Point t1, *t2; 
   return 0; 
} 

(A) Compiler Error
(B) Constructor called
      Constructor called
(C) Constructor called
(D) None of these
(E) Segmentation fault


Answer: (C)

Explanation: Only one object t1 is constructed here. t2 is just a pointer variable, not an object



7)
#include <iostream> 
using namespace std; 
   
int i; 
   
class A 
{ 
public: 
    ~A() 
    { 
        i=10; 
    } 
}; 
   
int foo() 
{ 
    i=3; 
    A ob; 
    return i; 
} 
   
int main() 
{ 
    cout << foo() << endl; 
    return 0; 
} 

(A) 0
(B) 3
(C) 10
(D) None of the above


Answer: (B)




8)Which of the following operators are overloaded by default by the compiler in every user defined classes even if user has not written?

1) Comparison Operator ( == )
2) Assignment Operator ( = ) 

(A) Both 1 and 2
(B) Only 1
(C) Only 2
(D) None of these


Answer: (C)

Explanation: Assign operator is by default available in all user defined classes even if user has not implemented. The default assignement does shallow copy.

But comparison operator “==” is not overloaded.



9)
#include<iostream> 
using namespace std; 
  
class Test 
{ 
private: 
  int x; 
public: 
  Test(int x = 0) { this->x = x; } 
  void change(Test *t) { this = t; } 
  void print() { cout << "x = " << x << endl; } 
}; 
  
int main() 
{ 
  Test obj(5); 
  Test *ptr = new Test (10); 
  obj.change(ptr); 
  obj.print(); 
  return 0; 
} 

(A) x = 5
(B) x = 10
(C) Compiler Error
(D) Runtime Error


Answer: (C)



10)
What is the return value of f(p, p) if the value of p is initialized to 5 before the call? 
Note that the first parameter is passed by reference, whereas the second parameter is passed by value.

int f(int &x, int c) {
   c  = c - 1;
   if (c == 0) return 1;
   x = x + 1;
   return f(x, c) * x;
} 

(A) 3024
(B) 6561
(C) 55440
(D) 161051


Answer: (B)

Explanation: Since c is passed by value and x is passed by reference, all functions will have same copy of x, but different copies of c.

f(5, 5) = f(x, 4)*x = f(x, 3)*x*x = f(x, 2)*x*x*x = f(x, 1)*x*x*x*x = 1*x*x*x*x = x^4


Since x is incremented in every function call, it becomes 9 after f(x, 2) call. So the value of expression x^4 becomes 9^4 which is 6561. 





11) 

Forward engineering in UML is the process of transforming ________

A). a code into a model 
B). a code into design n 
C). a model into a code
D). a model into test 


Ans-C





12) ________ is graphically rendered as a dashed line. 
A) Generalization 
B) Association 
C) Dependency 
D) Realization 


Ans- C



13) Following is C like pseudo code of a function that takes a number as an argument, and uses a stack S to do processing.

void fun(int n) 
{ 
    Stack S;  // Say it creates an empty stack S 
    while (n > 0) 
    { 
      // This line pushes the value of n%2 to stack S 
      push(&S, n%2); 
  
      n = n/2; 
    } 
  
    // Run while Stack S is not empty 
    while (!isEmpty(&S)) 
      printf("%d ", pop(&S)); // pop an element from S and print it 
} 

What does the above function do in general?
(A) Prints binary representation of n in reverse order
(B) Prints binary representation of n
(C) Prints the value of Logn
(D) Prints the value of Logn in reverse order


Answer: (B)



14)Consider the following two sequences :

X = < B, C, D, C, A, B, C >, and 
Y = < C, A, D, B, C, B > 

The length of longest common subsequence of X and Y is :

(A) 5
(B) 3
(C) 4
(D) 2


Answer: (C)


15)
You are given a list of 5 integers and these integers are in the range from 1 to 6. 
There are no duplicates in list. 
One of the integers is missing in the list. 
Which of the following expression would give the missing number.
^ is bitwise XOR operator.
~ is bitwise NOT operator.

Let elements of list can be accessed as list[0], list[1], list[2], list[3], list[4]
(A) list[0] ^ list[1] ^ list[2] ^ list[3] ^ list[4]
(B) list[0] ^ list[1] ^ list[2] ^ list[3] ^ list[4] ^ 1 ^ 2 ^ 3 ^ 4 ^ 5 ^ 6
(C) list[0] ^ list[1] ^ list[2] ^ list[3] ^ list[4] ^ 1 ^ 2 ^ 3 ^ 4 ^ 5
(D) ~(list[0] ^ list[1] ^ list[2] ^ list[3] ^ list[4])


Answer: (B)

Explanation: XOR of all list elements and numbers from 1 to 6 gives the missing number.



16)
Consider the polynomial p(x) = a0 + a1x + a2x^2 +a3x^3, where ai != 0, for all i. 
The minimum number of multiplications needed to evaluate p on an input x is:

(A) 3
(B) 4
(C) 6
(D) 9


Answer: (A)

Explanation: Multiplications can be minimized using following order for evaluation of the given expression.
p(x) = a0 + x(a1 + x(a2 + a3x))





17)

import static java.lang.System.*; 
    
class StaticImportDemo 
{ 
   public static void main(String args[]) 
   {       
        out.println("welcome to programming"); 
   } 
} 

(A) Compiler Error
(B) Runtime Error
(C) welcome to programming
(D) None of the above


Answer: (C)



18)
abstract class demo 
{ 
    public int a; 
    demo() 
    { 
        a = 10; 
    } 
  
    abstract public void set(); 
      
    abstract final public void get(); 
  
} 
  
class Test extends demo 
{ 
  
    public void set(int a) 
    { 
        this.a = a; 
    } 
  
    final public void get() 
    { 
        System.out.println("a = " + a); 
    } 
  
    public static void main(String[] args) 
    { 
        Test obj = new Test(); 
        obj.set(20); 
        obj.get(); 
    } 
} 
  

(A) a = 10
(B) a = 20
(C) Compilation error
(D) None of these


Answer: (C)



19)class Test 
{ 
	public static void main (String[] args) 
	{ 
		char arr1[] = {'1'}; 
		char arr2[] = {'1'}; 
		if (arr1 == arr2) 
			System.out.println("Same"); 
		else
			System.out.println("Not same"); 
	} 
} 


A) Same
B) Not same
C) Compilation fails
D) None of these

Ans - B



20)

class Test {  
    public static void main(String[] args) {  
      for(int i = 0; 0; i++)  
      {  
          System.out.println("Hello");  
          break;  
      }  
    }  
}  

(A) Hello
(B) Empty Output
(C) Compiler error
(D) Runtime error


Answer: (C)



## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/26th%2BMay%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/26th+May+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
