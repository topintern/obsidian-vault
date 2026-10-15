---
kind: "study-reference"
title: "15th+June+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/15th+June+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 15th+June+MCQ's

[[The Climb/Career Library/Career Library]]


1)
Output of the following C Code
#include<stdio.h> 
int main() 
{ 
   typedef int i; 
   i a = 0; 
   printf("%d", a); 
   return 0; 
} 

(A) Compiler Error
(B) Runtime Error
(C) 0
(D) 1
















Answer: (C)

Explanation: There is no problem with the program. It simply creates a user defined type i and creates a variable a of type i.



2)

What is the output of below C program?

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

Explanation: 
The control in the logical OR goes to the second expression only if the first expression results in FALSE. 
The function foo() is called because i++ returns 0(post-increment) after incrementing the value of i to 1. 
The foo() function actually swaps the values of two variables and returns the value of second parameter. 
So, values of variables j and k gets exchanged and OR expression evaluates to be TRUE.




3)
output of the following C Code

#include<stdio.h> 
int main() 
{ 
   int n; 
   for (n = 9; n!=0; n--) 
     printf("n = %d", n--); 
   return 0; 
} 

What is the output?
(A) 9 7 5 3 1
(B) 9 8 7 6 5 4 3 2 1
(C) Infinite Loop
(D) 9 7 5 3







Answer: (C)

Explanation: 

The program goes in an infinite loop because n is never zero when loop condition (n != 0) is checked. n changes like 7 5 3 1 -1 -3 -5 -7 -9 …





4)

output of the following  C code
int main() 
{ 
    char a[2][3][3] = {'s','t','a','y','h','o','m','e'}; 
    printf("%s ", **a); 
    return 0; 
} 

(A) Compiler Error
(B)  stayhome followed by garbage characters
(C)  stayhome
(D) Runtime Error










Answer: (C)

Explanation: We have created a 3D array that should have 2*3*3 (= 18) elements, but we are initializing only 9 of them.

In C, when we initialize less no of elements in an array all uninitialized elements become '\0' in case of char and 0 in case of integers. 




5)
Which of the following is incorrect in C++ ?

(1)When we write overloaded function we must code the function for each usage.
(2)When we write function template we code the function only once.
(3)It is difficult to debug macros
(4)Templates are more efficient than macros


(A) (1) and (2)
(B) (1), (2) and (3)
(C) (3) and (4)
(D) All are correct.





Answer: (D)

Explanation:

When we write overloaded function we must code the function for each usage. Correct
When we write function template we code the function only once. Correct
It is difficult to debug macros Correct
Templates are more efficient than macros Correct

So, option (D) is correct. 



6)
What happens in C++ when an exception is thrown and not caught anywhere like following program.

#include <iostream> 
using namespace std; 
  
int fun() throw (int) 
{ 
    throw 10; 
} 
  
int main() { 
  
  fun(); 
  
  return 0; 
} 
  

(A) Compiler error
(B) Abnormal program termination
(C) Program doesn’t print anything and terminates normally
(D) None of these





Answer: (B)

Explanation: When an exception is thrown and not caught, the program terminates abnormally.




7)

#include <iostream> 
using namespace std; 
   
class A 
{ 
public: 
    virtual void fun() { cout << "A::fun() "; } 
}; 
   
class B: public A 
{ 
public: 
   void fun() { cout << "B::fun() "; } 
}; 
   
class C: public B 
{ 
public: 
   void fun() { cout << "C::fun() "; } 
}; 
   
int main() 
{ 
    B *bp = new C; 
    bp->fun(); 
    return 0; 
} 

(A) A::fun()
(B) B::fun()
(C) C::fun()
(D) None of these
(E) Compilation fails







Answer: (C)

Explanation: 

The important thing to note here is B::fun() is virtual even if we have not uses virtual keyword with it.
When a class has a virtual function, functions with same signature in all descendant classes automatically become virtual. 
We don’t need to use virtual keyword in declaration of fun() in B and C. 
They are anyways virtual.



8) IN CPP, When one object reference variable is assigned to another object reference variable then

(A) a copy of the object is created.
(B) a copy of the reference is created.
(C) a copy of the reference is not created.
(D) it is illegal to assign one object reference variable to another object reference variable.









Answer: (B)

Explanation: 

When one object reference variable is assigned to another object reference variable then a copy of the reference is created.




9)

What is the time complexity of fun()?

int fun(int n) 
{ 
  int count = 0; 
  for (int i = 0; i < n; i++) 
     for (int j = i; j > 0; j--) 
        count = count + 1; 
  return count; 
}  

(A) Theta (n)
(B) Theta (n^2)
(C) Theta (n*Logn)
(D) Theta (nLognLogn)






Answer: (B)

Explanation: 

The time complexity can be calculated by counting number of times the expression "count = count + 1;" is executed. 

The expression is executed 0 + 1 + 2 + 3 + 4 + …. + (n-1) times.

Time complexity = Theta(0 + 1 + 2 + 3 + .. + n-1) = Theta (n*(n-1)/2) = Theta(n^2)



10)

Given:
4. public class SpecialOps {
5. public static void main(String[] args) {
6. String s = "";
7. Boolean b1 = true;
8. Boolean b2 = false;
9. if((b2 = false) | (21%5) > 2) s += "x";
10. if(b1 || (b2 = true)) s += "y";
11. if(b2 == true) s += "z";
12. System.out.println(s);
13. }
14. }

Which are true? (Choose all that apply.)
A. Compilation fails
B. x will be included in the output
C. y will be included in the output
D. z will be included in the output
E. An exception is thrown at runtime





Answer:
C is correct. 
First of all, boxing takes care of the Boolean. 
Line 9 uses the modulus operator,which returns the remainder of the division, which in this case is 1. 
Also, line 9 sets b2 to false, and it doesn't test b2's value. 
Line 10 sets b2 to true, and it doesn’t test its value;
however, the short circuit operator keeps the expression b2 = true from being executed.



11)

Given:
3. public class Spock {
4. public static void main(String[] args) {
5. int mask = 0;
6. int count = 0;
7. if( ((5<7) || (++count < 10)) | mask++ < 10 ) mask = mask + 1;
8. if( (6 > 8) ^ false) mask = mask + 10;
9. if( !(mask > 1) && ++count > 1) mask = mask + 100;
10. System.out.println(mask + " " + count);
11. }
12. }

Which two answers are true about the value of mask and the value of count at line 10?
(Choose two.)
A. mask is 0
B. mask is 1
C. mask is 2
D. mask is 10
E. mask is greater than 10
F. count is 0
G. count is greater than 0





Answer:

C and F are correct. 
At line 7 the || keeps count from being incremented, but the | allows mask to be incremented. 
At line 8 the ^ returns true only if exactly one operand is true. 
At line 9 mask is 2 and the && keeps count from being incremented.


12)

Given:
3. interface Vessel { }
4. interface Toy { }
5. class Boat implements Vessel { }
6. class Speedboat extends Boat implements Toy { }
7. public class Tree {
8. public static void main(String[] args) {
9. String s = "0";
10. Boat b = new Boat();
11. Boat b2 = new Speedboat();
12. Speedboat s2 = new Speedboat();
13. if((b instanceof Vessel) && (b2 instanceof Toy)) s += "1";
14. if((s2 instanceof Vessel) && (s2 instanceof Toy)) s += "2";
15. System.out.println(s);
16. }
17. }

What is the result?
A. 0
B. 01
C. 02
D. 012
E. Compilation fails
F. An exception is thrown at runtime







Answer:
D is correct. 
First, remember that instanceof can look up through multiple levels of an inheritance tree. 
Also remember that instanceof is commonly used before attempting a downcast, 
so in this case, after line 15, it would be possible to say Speedboat s3 =(Speedboat)b2;.



13)

Given:

class Plane {
static String s = "-";
public static void main(String[] args) {
new Plane().s1();
System.out.println(s);
}
void s1() {
try { s2(); }
catch (Exception e) { s += "c"; }
}
void s2() throws Exception {
s3(); s += "2";
s3(); s += "2b";
}
void s3() throws Exception {
throw new Exception();
} }

What is the result?
A. -
B. -c
C. -c2
D. -2c
E. -c22b
F. -2c2b
G. -2c2bc
H. Compilation fails






Answer:
B is correct. 
Once s3() throws the exception to s2(), s2() throws it to s1(), 
and no more of s2()’s code will be executed.



14)

Given:

try { int x = Integer.parseInt("two"); }

Which could be used to create an appropriate catch block? (Choose all that apply.)
A. ClassCastException
B. IllegalStateException
C. NumberFormatException
D. IllegalArgumentException
E. ExceptionInInitializerError
F. ArrayIndexOutOfBoundsException








Answer:
C and D are correct. 
Integer.parseInt can throw a NumberFormatException, and
IllegalArgumentException is its superclass (i.e., a broader exception).




15)
void main()
{
    fork() ; fork() ; printf ("yes");
}

If we execute this core segment, how many times the string yes will be printed ?
(A) Only once
(B) 2 times
(C) 4 times
(D) 8 times





Answer: (C)

Explanation: Number of times YES printed is equal to number of process created.

Total Number of Processes = 2^n where n is number of fork system calls. So here n = 2, 2^2 = 4

fork ();   // Line 1
fork ();   // Line 2

       P1      
    /     \     
  P1      C1    
 /  \    /  \   
P1  C2  C1  C3   
                

So, there are total 4 processes (3 new child processes and one original process).



16)
A computer has 1000 K of main memory. 

The jobs arrive and finish in the sequence

Job 1 requiring 200 K arrives
Job 2 requiring 350 K arrives
Job 3 requiring 300 K arrives
Job 1 finishes
Job 4 requiring 120 K arrives
Job 5 requiring 150 K arrives
Job 6 requiring 80 K arrives

Among best fit and first fit, which performs better for this sequence?
(A) First fit
(B) Best fit
(C) Both perform the same
(D) None of the above


Answer: (A)

Explanation: 

Main memory = 1000K


Job 1 requiring 200 K arrives
Job 2 requiring 350 K arrives
Job 3 requiring 300 K arrives and assuming continuous allocation:

Free memory = 1000 - 850(200 + 350 + 300) = 150 K (till these jobs first fit and best fit are same)
Since, job 1 finishes, Free memory = 200 K and 150 K

Case 1: First fit

Job 4 requiring 120 K arrives
Since 200 K will be the first slot, so Job 4 will acquire this slot only. Remaining memory = 200 – 120 = 80 K

Job 5 requiring 150 K arrives
It will acquire 150 K slot

Job 6 requiring 80 K arrives
It will occupy 80 K slot, so, all jobs will be allocated successfully.

Case 2: Best fit

Job 4 requiring 120 K arrives
It will occupy best fit slot which is 150 K. So, remaining memory = 150 - 120 = 30 K

Job 5 requiring 150 K arrives
It will occupy 200 K slot. So, free space = 200 - 150 = 50 K

Job 6 requiring 80 K arrives
There is no continuous 80 K memory free. So, it will not be able to allocate.

So, first fit is better.
Option (A) is correct.



17) What is meant by the term ‘thread of control’ in the context of concurrent behaviour?
		
A)	A thread of control is a weak part of the control system.
B)	A thread of control is the mechanism that controls concurrent behaviour.
C)	A thread of control is an execution pathway that may occur simultaneously 
with other execution pathways.
D)	None of these
	











Ans- C


18)  Which of the following is an appropriate way of managing complex behaviour 
on an interaction sequence diagram?

A)	A group of objects can be represented by a single lifeline.
B)	Some messages are omitted to reduce the complexity.
C)	Some objects are omitted from the diagram to reduce the complexity.
D)	None of these








Ans- A


19) Collaboration diagrams differ from interaction sequence diagrams in the following way?
		
A)	Collaboration diagrams cannot show the design detail that can be shown on 
a sequence diagram.
B)	Collaboration diagrams only show the collaboration and not the sequence 
in which the messages are sent.
C)	Collaboration diagrams show the links between the objects.
D)	None of these








Ans-C


20)	Which of the following is a disadvantage of collaboration diagrams?
		
A)	A collaboration diagram can only be used during analysis.
B)	A collaboration diagram cannot include guard conditions.
C)	A collaboration diagram is difficult to read if there are many messages between two objects.
D)	None of these












Ans-C

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/15th%2BJune%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/15th+June+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
