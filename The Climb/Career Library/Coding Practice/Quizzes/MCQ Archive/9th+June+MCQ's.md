---
kind: "study-reference"
title: "9th+June+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/9th+June+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 9th+June+MCQ's

[[The Climb/Career Library/Career Library]]

1)
Predict the output of following C program

int main() 
{ 
    char a[2][3][3] = {'h','e','l','l','o','k','m','i','t'}; 
    printf("%s ", **a); 
    return 0; 
} 

(A) Compiler Error
(B) hellokmit followed by garbage characters
(C) hellokmit
(D) Runtime Error


















Answer: (C)

Explanation: 
We have created a 3D array that should have 2*3*3 (= 18) elements, but we are
initializing only 9 of them. 

In C, when we initialize less no of elements in an array all uninitialized
elements become '\0' in case of char and 0 in case of integers.


2)Predict the output of following C program, assume that a character takes 1
byte and pointer takes 4 bytes.

#include <stdio.h> 
int main() 
{ 
    char *str1 = "HelloKmit"; 
    char str2[] = "HelloKmit"; 
  
    printf("sizeof(str1) = %d, sizeof(str2) = %d",  sizeof(str1), sizeof(str2)); 
  
    return 0; 
} 

(A) sizeof(str1) = 10, sizeof(str2) = 10
(B) sizeof(str1) = 4, sizeof(str2) = 10
(C) sizeof(str1) = 4, sizeof(str2) = 4
(D) sizeof(str1) = 10, sizeof(str2) = 4











Answer: (B)

Explanation: str1 is a pointer and str2 is an array.



3)
 Pick the best statement for the below program In C:

#include<stdio.h>
int main() 
{ 
 union {int i1; int i2;} myVar = {.i2 =100}; 
 printf("%d %d",myVar.i1, myVar.i2); 
 return 0; 
} 

(A) Compile error due to incorrect syntax of initialization.
(B) No compile error and it’ll print “0 100”.
(C) No compile error and it’ll print “100 100”.
(D) None of these















Answer: (C)

Explanation: 
Since fields/members of union share same memory, both i1 and i2 refer to same location. 
Also, since both i1 and i2 are of same type, initializing one would initialize
the other as well implicitly. 
So answer is C.



4)
Pick the best statement for the following program snippet:
#include<stdio.h>

void foo(void) 
{ 
 static int staticVar; 
 staticVar++; 
 printf("foo: %d\n",staticVar); 
} 
  
void bar(void) 
{ 
 static int staticVar; 
 staticVar++; 
 printf("bar: %d\n",staticVar); 
} 
  
int main() 
{ 
 foo(), bar(), foo(); 
 return 0; 
} 

(A) Compile error because same static variable name is used in both foo and bar. 
      Since these static variables retain their values even after function is over, same name can’t be used in both the functions.
(B) Compile error because semicolon isn’t used while calling foo() and bar() in side main function.
(C) No compile error and only one copy of staticVar would be used across both the functions and that’s why final value of that single staticVar would be 3.
(D) No compile error and separate copies of staticVar would be used in both the functions. 
      That’s why staticVar in foo() would be 2 while staticVar in bar() would be 1.





Answer: (D)

Explanation: 
Here, even though life of static variables span across function calls but their
scope is respective to their function body only. 
That’s why staticVar of each function has separate copies whose life span across
function calls. 
And d is correct.




5)

Predict the output of the following CPP Program

#include <iostream> 
using namespace std; 
  
class Test { 
  static int count; 
  int id; 
public: 
  Test() { 
    count++; 
    id = count; 
    cout << "Constructing object number " << id << endl; 
    if(id == 4) 
       throw 4; 
  } 
  ~Test() { cout << "Destructing object number " << id << endl; } 
}; 
  
int Test::count = 0; 
  
int main() { 
  try { 
    Test array[5]; 
  } catch(int i) { 
    cout << "Caught " << i << endl; 
  } 
} 

(A)

Constructing object number 1
Constructing object number 2
Constructing object number 3
Constructing object number 4
Destructing object number 1
Destructing object number 2
Destructing object number 3
Destructing object number 4
Caught 4

(B)

Constructing object number 1
Constructing object number 2
Constructing object number 3
Constructing object number 4
Destructing object number 3
Destructing object number 2
Destructing object number 1
Caught 4

(C)

Constructing object number 1
Constructing object number 2
Constructing object number 3
Constructing object number 4
Destructing object number 4
Destructing object number 3
Destructing object number 2
Destructing object number 1
Caught 4

(D)

Constructing object number 1
Constructing object number 2
Constructing object number 3
Constructing object number 4
Destructing object number 1
Destructing object number 2
Destructing object number 3
Caught 4







Answer: (B)

Explanation: The destructors are called in reverse order of constructors. 
Also, after the try block, the destructors are called only for completely constructed objects.




6)


#include <iostream> 
using namespace std; 
  
template <int i> 
void fun() 
{ 
   i = 20; 
   cout << i; 
} 
  
int main() 
{ 
   fun<10>(); 
   return 0; 
} 

(A) 10
(B) 20
(C) Compiler Error
(D) None of these










Answer: (C)

Explanation: Compiler error in line “i = 20;”

Non-type parameters must be const, so they cannot be modified.




7)
Can static functions be virtual?
Will the following program compile?

#include<iostream>  
using namespace std;     
  
class Test 
{ 
   public: 
      virtual static void fun()  { } 
}; 

(A) Yes
(B) No
(C) Will compile followed by a Segmentation fault
(D) None of these







Answer: (B)

Explanation: 
Static functions are class specific and may not be called on objects. 
Virtual functions are called according to the pointed or referred object.




8)The following postfix expression with single digit operands is evaluated using a stack:

              8 2 3 ^ / 2 3 * + 5 1 * - 

Note that ^ is the exponentiation operator. 

The top two elements of the stack after the first * is evaluated are:

(A) 6, 1
(B) 5, 7
(C) 3, 2
(D) 1, 5







Answer: (A)

1. While there are input tokens left
    o Read the next token from input.
    o If the token is a value
       + Push it onto the stack.
    o Otherwise, the token is an operator 
      (operator here includes both operators, and functions).
       * It is known a priori that the operator takes n arguments.
       * If there are fewer than n values on the stack
        (Error) The user has not input sufficient values in the expression.
       * Else, Pop the top n values from the stack.
       * Evaluate the operator, with the values as arguments.
       * Push the returned results, if any, back onto the stack.
2. If there is only one value in the stack
    o That value is the result of the calculation.
3. If there are more values in the stack
    o (Error)  The user input has too many values.

First three tokens are values, so they are simply pushed. After pushing 8, 2 and
3, the stack is as follows
    8, 2, 3
When ^ is read, top two are popped and power(2^3) is calculated
    8, 8
When / is read, top two are popped and division(8/8) is performed
    1
Next two tokens are values, so they are simply pushed. After pushing 2 and 3, the stack is as follows
    1, 2, 3
When * comes, top two are popped and multiplication is performed.
    1, 6


9)Convert the following infix to postfix  expression

a+b*(c^d-e)^(f+g*h)-i


(A) abcd^ef-gh*^+*i+-
(B) abcd^e-fgh*+^*+i-
(C) abc^de-fgh+*^*+i-
(D) abcd-e^fgh+**^+i-


Ans- B



10)


Given an Prefix convert to Postfix 

Prefix :  *+AB-CD

A) AB-CD+*
B) AB*CD-+
C) AB+CD*-
D) AB+CD-*



Ans- D

Explanation : Prefix to Infix :  (A+B) * (C-D)
                   Infix to Postfix :  AB+CD-*


Algorithm for Prefix to Postfix:

    Read the Prefix expression in reverse order (from right to left)
    If the symbol is an operand, then push it onto the Stack
    If the symbol is an operator, then pop two operands from the Stack
    Create a string by concatenating the two operands and the operator
    after them.
    string = operand1 + operand2 + operator
    And push the resultant string back to Stack
    Repeat the above steps until end of Prefix expression.



11)

To evaluate an expression without any embedded function calls:

(A) One stack is enough
(B) Two stacks are needed
(C) As many stacks as the height of the expression tree are needed
(D) A Turing machine is needed in the general case





Answer: (A)

Explanation:
Any expression can be converted into Postfix or Prefix form.

Prefix and postfix evaluation can be done using a single stack.

For example : Expression ’10 2 8 * + 3 -‘ is given.
PUSH 10 in the stack.
PUSH 2 in the stack.
PUSH 8 in the stack.
When operator ‘*’ occurs, POP 2 and 8 from the stack.
PUSH 2 * 8 = 16 in the stack.
When operator ‘+’ occurs, POP 16 and 10 from the stack.
PUSH 10 * 16 = 26 in the stack.
PUSH 3 in the stack.
When operator ‘-‘ occurs, POP 26 and 3 from the stack.
PUSH 26 – 3 = 23 in the stack.
So, 23 is the answer obtained using single stack.

 
Thus, option (A) is correct.



12)

Given:

3. class Dozens {
4. int[] dz = {1,2,3,4,5,6,7,8,9,10,11,12};
5. }
6. public class Eggs {
7. public static void main(String[] args) {
8. Dozens [] da = new Dozens[3];
9. da[0] = new Dozens();
10. Dozens d = new Dozens();
11. da[1] = d;
12. d = null;
13. da[1] = null;
14. // do stuff
15. }
16. }

Which two are true about the objects created within main(), and 
eligible for garbage collection when line 14 is reached?

A. Three objects were created
B. Four objects were created
C. Five objects were created
D. Zero objects are eligible for GC
E. One object is eligible for GC
F. Two objects are eligible for GC
G. Three objects are eligible for GC




Answer:
C and F are correct. 
da refers to an object of type "Dozens array," and 
each Dozens object that is created comes with its own "int array" object. 
When line 14 is reached,
only the second Dozens object (and its "int array" object) are not reachable.


13)

Given:
3. public class Ouch {
4. static int ouch = 7;
5. public static void main(String[] args) {
6. new Ouch().go(ouch);
7. System.out.print(" " + ouch);
8. }
9. void go(int ouch) {
10. ouch++;
11. for(int ouch = 3; ouch < 6; ouch++)
12. ;
13. System.out.print(" " + ouch);
14. }
15. }


What is the result?
A. 5 7
B. 5 8
C. 8 7
D. 8 8
E. Compilation fails
F. An exception is thrown at runtime


Answer:

E is correct. 
The parameter declared on line 9 is valid (although ugly), 
but the variable name ouch cannot be declared again on line 11 in the same scope
as the declaration on line 9.




14)

Given:
3. public class Bertha {
4. static String s = "";
5. public static void main(String[] args) {
6. int x = 4; Boolean y = true; short[] sa = {1,2,3};
7. doStuff(x, y);
8. doStuff(x);
9. doStuff(sa, sa);
10. System.out.println(s);
11. }
12. static void doStuff(Object o) { s += "1"; }
13. static void doStuff(Object... o) { s += "2"; }
14. static void doStuff(Integer... i) { s += "3"; }
15. static void doStuff(Long L) { s += "4"; }
16. }

What is the result?
A. 212
B. 232
C. 234
D. 312
E. 332
F. 334
G. Compilation fails


Answer:
A is correct.

It's legal to autobox and then widen. 
The first call to doStuff() boxes the int to an Integer then passes two objects. 
The second call cannot widen and then box (making the Long method unusable),
so it boxes the int to an Integer. 
As always, a var-args method will be chosen only if no non-var-arg method is possible. 
The third call is passing two objects—they are of type 'short array.'



15) Data can be ________.
		
(A)	Analog only
(B)	Digital only
(C)	Both Analog and Digital 
(D)	None of these

















Ans- C




16)_______ data are continuous and take continuous values.

(A)	Analog only
(B)	Digital only
(C)	Both Analog and Digital 
(D)	None of these

















Ans- (A)



17)	________ is the process of converting digital data to a digital signal.
		
A)	Block coding
B)	Line coding
C)	Scrambling
D)	None of these

























Ans-B




18)Which of these is the correct set of analysis class stereotypes in standard UML?
		
A)	Interface, control and entity.
B)	Boundary, control and entity.
C)	Interface, sequence and entity.
D)	None of these














Ans-B



19)What do boundary classes represent?
		
A)	Customers and suppliers of the business.
B)	People who will use the system.
C)	Interaction between the system and its actors.
D)	None of these	














Ans- C


20)What are entity classes?
		
A)	Classes that contain data.
B)	Classes that contain persistent data.
C)	Classes that represent something or some concept in the application domain.
D)	None of these








Ans- C

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/9th%2BJune%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/9th+June+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
