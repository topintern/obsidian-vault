---
kind: "study-reference"
title: "11th+June+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/11th+June+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 11th+June+MCQ's

[[The Climb/Career Library/Career Library]]

1)

Consider the following three C functions :

[PI] 
int * g (void)  
{  
  int x= 10;  
  return (&x);  
}   
    
[P2] 
int * g (void)  
{  
  int * px;  
  *px= 10;  
  return px;  
}  
    
[P3] 
int *g (void)  
{  
  int *px;  
  px = (int *) malloc (sizeof(int));  
  *px= 10;  
  return px;  
} 

Which of the above three functions are likely to cause problems with pointers?
(A) Only P3
(B) Only P1 and P3
(C) Only P1 and P2
(D) P1, P2 and P3






Answer: (C)

Explanation: 

In P1, pointer variable x is a local variable to g(), and g() returns pointer to this variable. x may vanish after g() has returned as x exists on stack. 
So, &x may become invalid.
In P2, pointer variable px is being assigned a value without allocating memory to it.
P3 works perfectly fine. 
Memory is allocated to pointer variable px using malloc(). 
So, px exists on heap, it’s existence will remain in memory even after return of g() as it is on heap




2)
Assume that the size of char is 1 byte and negatives are stored in 2’s complement form

#include<stdio.h> 
int main() 
{ 
    char c = 125; 
    c = c+10; 
    printf("%d", c); 
    return 0; 
} 

(A) 135
(B) +INF
(C) -121
(D) -8





Answer: (C)

Explanation: 

125 is represented as 01111101 in binary and when we add 10 i.e 1010 in binary it becomes : 10000111. 
Now what does this number represent?
Firstly, you should know that char can store numbers only -128 to 127 since the most significant bit is kept for sign bit. 
Therefore 10000111 represents a negative number. 
To check which number it represents we find the 2’s complement of it and get 01111001
which is = 121 in decimal system. 
Hence, the number 10000111 represents -121.



3)


#include <stdio.h> 
int fun() 
{ 
  static int num = 16; 
  return num--; 
} 
  
int main() 
{ 
  for(fun(); fun(); fun()) 
    printf("%d ", fun()); 
  return 0; 
} 

(A) Infinite loop
(B) 13 10 7 4 1
(C) 14 11 8 5 2
(D) 15 12 8 5 2






Answer: (C)

Explanation:

Since num is static in fun(), the old value of num is preserved for subsequent functions calls. 

Also, since the statement return num– is postfix, it returns the old value of num, 
and updates the value for next function call.

fun() called first time: num = 16 // for loop initialization done;

In test condition, compiler checks for non zero value

fun() called again : num = 15

printf("%d \n", fun());:num=14 ->printed

Increment/decrement condition check

fun(); called again : num = 13

----------------

fun() called second time: num: 13 

In test condition,compiler checks for non zero value

fun() called again : num = 12

printf("%d \n", fun());:num=11 ->printed

fun(); called again : num = 10

--------

fun() called second time : num = 10 

In test condition,compiler checks for non zero value

fun() called again : num = 9

printf("%d \n", fun());:num=8 ->printed

fun(); called again   : num = 7

--------------------------------

fun() called second time: num = 7

In test condition,compiler checks for non zero value

fun() called again : num = 6

printf("%d \n", fun());:num=5 ->printed

fun(); called again   : num = 4

-----------

fun() called second time: num: 4 

In test condition,compiler checks for non zero value

fun() called again : num = 3

printf("%d \n", fun());:num=2 ->printed

fun(); called again   : num = 1

----------

fun() called second time: num: 1 

In test condition,compiler checks for non zero value

fun() called again : num = 0 => STOP 






4)


# include <stdio.h> 
int main() 
{ 
   int i = 0; 
   for (i=0; i<20; i++) 
   { 
     switch(i) 
     { 
       case 0: 
         i += 5; 
       case 1: 
         i += 2; 
       case 5: 
         i += 5; 
       default: 
         i += 4; 
         break; 
     } 
     printf("%d  ", i); 
   } 
   return 0; 
} 

(A) 5 10 15 20
(B) 7 12 17 22
(C) 16 21
(D) Compiler Error






Answer: (C)

Explanation: 

Initially i = 0. 
Since case 0 is true i becomes 5, and since there is no break statement till last
statement of switch block, i becomes 16. 
Now in next iteration no case is true, so execution goes to default and i becomes 21.





5)

Which of the following is true about exception handling in C++?

1) There is a standard exception class like Exception class in Java.
2) All exceptions are unchecked in C++, i.e., compiler doesn’t check if the 
exceptions are caught or not.
3) In C++, a function can specify the list of exceptions that it can throw
using comma separated list like following.

  void fun(int a, char b) throw (Exception1, Exception2, ..) 

(A) 1 and 3
(B) 1, 2 and 3
(C) 1 and 2
(D) 2 and 3






Answer: (B)




6)
#include <iostream>
using namespace std;
struct sec 
{
    int a;
    char b;
};
int main()
{
    struct sec s ={25,50};
    struct sec *ps =(struct sec *)&s;
    cout << ps->a << " " << ps->b;
    return 0;
}

a) 25 2
b) 25 3
c) 25 4
d) 26 2




Answer: a


7)Which of the followings is/are automatically added to every class, if we do not write our own.

(A) Copy Constructor
(B) Assignment Operator
(C) A constructor without any parameter
(D) All of the above













Answer: (D)


Explanation: 
In C++, if we do not write our own, then compiler automatically creates a default constructor, a copy constructor and a assignment operator for every class. 





8). What is the general syntax for accessing the namespace variable?

a) namespace::operator
b) namespace,operator
c) namespace#operator
d) namespace$operator














Answer: a

Explanation: 

To access variables from namespace we use following syntax.

namespace :: variable;
General syntax:

namespace X{ int a;}
cout<<X::a; 



9)What will be the output of the following C++ code?


#include <iostream>
using namespace std;

namespace first
{
    int var = 5;
}

namespace second
{
    double var = 3.1416;
}

int main ()
{
    int a;
    a = first::var + second::var;
    cout << a;
    return 0;
}

a) 8.31416
b) 8
c) 9
d) compile time error













Answer: b
Explanation: As we are getting two variables from namespace variable and we are adding that.




10) What will be the output of the following C++ code?

#include <iostream>
using namespace std;

namespace first
{
    int x = 5;
    int y = 10;
}

namespace second
{
    double x = 3.1416;
    double y = 2.7183;
}

int main ()
{
    using first::x;
    using second::y;
    bool a, b;
    a = x > y;
    b = first::y < second::x;
    cout << a << " " << b;
    return 0;
}

a) 1 1
b) 0 1
c) 0 0
d) 1 0






Answer: d

Explanation: 
We are inter mixing the variable and comparing it which is bigger and smaller 
and according to that we are printing the output.




11)

Given:
1. class Comp2 {
2. public static void main(String[] args) {
3. float f1 = 2.3f;
4. float[][] f2 = {{42.0f}, {1.7f, 2.3f}, {2.6f, 2.7f}};
5. float[] f3 = {2.7f};
6. Long x = 42L;
7. // insert code here
8. System.out.println("true");
9. }
10. }


And the following five code fragments:
F1. if(f1 == f2)
F2. if(f1 == f2[2][1])
F3. if(x == f2[0][0])
F4. if(f1 == f2[1,1])
F5. if(f3 == f2[2])

What is true?

A. One of them will compile, only one will be true
B. Two of them will compile, only one will be true
C. Two of them will compile, two will be true
D. Three of them will compile, only one will be true
E. Three of them will compile, exactly two will be true
F. Three of them will compile, exactly three will be true






Answer:

D is correct. 

Fragments F2, F3, and F5 will compile, and only F3 is true.
A, B, C, E, and F are incorrect.
F1 is incorrect because you can’t compare a primitive to an array. 
F4 is incorrect syntax to access an element of a two-dimensional array.



12)Given:

class Fork {
public static void main(String[] args) {
if(args.length == 1 | args[1].equals("test")) {
System.out.println("test case");
} else {
System.out.println("production " + args[0]);
}
}
}

And the command-line invocation:
java Fork live2

What is the result?
A. test case
B. production live2
C. test case live2
D. Compilation fails
E. An exception is thrown at runtime







Answer:
E is correct. 

Because the short circuit (||) is not used, both operands are evaluated. 
Since args[1] is past the args array bounds, an ArrayIndexOutOfBoundsException is thrown.




13)
Given:
class Feline {
public static void main(String[] args) {
Long x = 42L;
Long y = 44L;
System.out.print(" " + 7 + 2 + " ");
System.out.print(foo() + x + 5 + " ");
System.out.println(x + y + foo());
}
static String foo() { return "foo"; }
}

What is the result?

A. 9 foo47 86foo
B. 9 foo47 4244foo
C. 9 foo425 86foo
D. 9 foo425 4244foo
E. 72 foo47 86foo
F. 72 foo47 4244foo
G. 72 foo425 86foo
H. 72 foo425 4244foo
I. Compilation fails




Answer:
G is correct. 

Concatenation runs from left to right, and if either operand is a String, the operands are concatenated. 
If both operands are numbers they are added together. 
Unboxing works in conjunction with concatenation.




14)

Given:
3. public class Twisty {
4. { index = 1; }
5. int index;
6. public static void main(String[] args) {
7. new Twisty().go();
8. }
9. void go() {
10. int [][] dd = {{9,8,7}, {6,5,4}, {3,2,1,0}};
11. System.out.println(dd[index++][index++]);
12. }
13. }

What is the result? (Choose all that apply.)
A. 1
B. 2
C. 4
D. 6
E. 8
F. Compilation fails
G. An exception is thrown at runtime






Answer:
C is correct. 

Multidimensional arrays' dimensions can be inconsistent, the code uses an initialization block, 
and the increment operators are both post-increment operators.



15)

Given:

3. public class McGee {
4. public static void main(String[] args) {
5. Days d1 = Days.TH;
6. Days d2 = Days.M;
7. for(Days d: Days.values()) {
8. if(d.equals(Days.F)) break;
9. d2 = d;
10. }
11. System.out.println((d1 == d2)?"same old" : "newly new");
12. }
13. enum Days {M, T, W, TH, F, SA, SU};
14. }

What is the result?
A. same old
B. newly new
C. Compilation fails due to multiple errors
D. Compilation fails due only to an error on line 7
E. Compilation fails due only to an error on line 8
F. Compilation fails due only to an error on line 11
G. Compilation fails due only to an error on line 13









Answer:
A is correct. 

All of this syntax is correct. 
The for-each iterates through the enum using the values() method to return an array. 
Enums can be compared using either equals() or ==. 
Enums can be used in a ternary operator's Boolean test.




16) An IPv4 address consists of _______ bits.
		
A)	4
B)	8
C)	32
D)	64







Ans-C


17) 	An IPv6 address can have up to __________ colons.
		
A)	8
B)	7
C)	4
D)	none of these
	



Ans-B


18) An IPv6 address can have up to __________ hexadecimal digits.
		
A)	16
B)	32
C)	8
D)	none of these








Ans-B



19)Which is the correct UML definition of a collaboration?
		
A)	A collaboration describes the messages between objects.
B)	A collaboration describes objects that share functionality.
C)	A collaboration describes the structure of instances playing roles in a
behaviour and their relationships.
D)	None of these










Ans- C




20)	An interaction sequence diagram drawn during analysis differs from one drawn during design which of the following ways?

A)	It normally does not include design objects or detailed specifications of message signatures.
B)	It does not include boundary objects.
C)	It does not include control objects.
D)	None of these	









Ans- A


## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/11th%2BJune%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/11th+June+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
