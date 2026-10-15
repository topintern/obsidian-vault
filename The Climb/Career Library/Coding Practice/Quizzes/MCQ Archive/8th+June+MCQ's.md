---
kind: "study-reference"
title: "8th+June+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/8th+June+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 8th+June+MCQ's

[[The Climb/Career Library/Career Library]]

1)

But given the following definitions (along-with initialization) of 2D arrays

int array2D[2][4] = {1,2,3,4,5,6,7,8}; /* (i) */
int array2D[][4] = {1,2,3,4,5,6,7,8}; /* (ii) */
int array2D[2][] = {1,2,3,4,5,6,7,8}; /* (iii) */
int array2D[][] = {1,2,3,4,5,6,7,8}; /* (iv) */

Pick the correct statements.
(A) Only (i) is correct.
(B) Only (i) and (ii) are correct.
(C) Only (i), (ii) and (iii) are correct.
(D) All (i), (ii), (iii) and (iv) are correct.

















Answer: (B)

Explanation: 
First of all, C language doesn’t provide any true support for 2D array or multidimensional arrays. 

A 2D array is simulated via 1D array of arrays. So a 2D array of int is actually a 1D array of array of int. 

Another important point is that array size can be derived from its initialization but that’s applicable for first dimension only. 

It means that 2D array need to have an explicit size of 2nd dimension. 
Similarly, for a 3D array, 2nd and 3rd dimensions need to have explicit size. 
That’s why only (i) and (ii) are correct. 

But array2D[2][] and array2D[][] are of incomplete type because their complete size can’t derived even from the initialization.



2)
Pick the best statement for the below program:

#include <stdio.h> 
  
int main() 
{ 
 struct {int i; char c;} myVar = {.c ='A',.i = 100}; 
 printf("%d %c",myVar.i, myVar.c); 
 return 0; 
} 

(A) Compile error because struct type (containing two fields of dissimilar type i.e. an int and a char) has been mentioned along with definition of myVar of that struct type.
(B) Compile error because of incorrect syntax of initialization of myVar. Basically, member of operator (i.e. dot .) has been used without myVar.
(C) Compile error for not only B but for incorrect order of fields in myVar i.e. field c has been initialized first and then field i has been initialized.
(D) No compile error and it’ll print 100 A.







Answer: (D)



3)Predict the output of the below program:

#include <stdio.h> 
#define EVEN 0 
#define ODD 1 

int main() 
{ 
    int i = 3; 
    switch (i & 1) 
    { 
        case EVEN: printf("Even"); 
                break; 
        case ODD: printf("Odd"); 
                break; 
        default: printf("Default"); 
    } 
    return 0; 
} 

(A) Even
(B) Odd
(C) Default
(D) Compile-time error


Answer: (B)

Explanation: 
The expression i & 1 returns 1 if the rightmost bit is set and returns 0 if the rightmost bit is not set. 
As all odd integers have their rightmost bit set, the control goes to the block labeled ODD.




4)
#include<stdio.h> 
int main() 
{ 
    char str[] = "helloKmit"; 
    printf("%s %s %s\n", &str[5], &5[str], str+5); 
    printf("%c %c %c\n", *(str+6), str[6], 6[str]); 
    return 0; 
} 

(A) Runtime Error
(B) Compiler Error
(C) mit mit mit
      m m m
(D) Kmit Kmit Kmit
      m m m












Answer: (D)

Explanation: The program has no error. All of the following expressions mean same thing
&str[5]
&5[str]
str+5
Since compiler converts the array operation in pointers before accessing the array elements, all above result in same address.

Similarly, all of the following expressions mean same thing.
*(str+6)
str[6]
6[str]




5)
#include<stdio.h> 
int f(int *a, int n) 
{ 
  if(n <= 0) return 0; 
  else if(*a % 2 == 0) return *a + f(a+1, n-1); 
  else return *a - f(a+1, n-1); 
} 
   
int main() 
{ 
  int a[] = {12, 7, 13, 4, 11, 6}; 
  printf("%d", f(a, 6)); 
  getchar(); 
  return 0; 
}

(A) -9
(B) 5
(C) 15
(D) 19






Answer: (C)

Explanation: f() is a recursive function which adds f(a+1, n-1) to *a if *a is even. 
If *a is odd then f() subtracts f(a+1, n-1) from *a. 

See below recursion tree for execution of f(a, 6).
.

 f(add(12), 6) /*Since 12 is first element. a contains address of 12 */
    |
    |
 12 + f(add(7), 5) /* Since 7 is the next element, a+1 contains address of 7 */
        |
        |
     7 - f(add(13), 4)
              |
              |
           13 - f(add(4), 3)
                     |
                     |
                  4 + f(add(11), 2)
                             |
                             |
                           11 - f(add(6), 1)
                                    |
                                    |
                                 6 + 0

So, the final returned value is 12 + (7 – (13 – (4 + (11 – (6 + 0))))) = 15




6)


#include <stdio.h> 
int fun(int n, int *f_p) 
{ 
    int t, f; 
    if (n <= 1) 
    { 
        *f_p = 1; 
        return 1; 
    } 
    t = fun(n- 1,f_p); 
    f = t+ * f_p; 
    *f_p = t; 
    return f; 
} 
  
int main() 
{ 
    int x = 15; 
    printf (" %d \n", fun(5, &x)); 
    return 0; 
} 

(A) 6
(B) 8
(C) 14
(D) 15





Answer: (B)

Explanation:

Let x is stored at location 2468 i.e. &x = 2468

(dots are use just to ensure alignment)
x = 15
fun(5, 2468)
...{t = fun(4, 2468)
.......{t = fun(3, 2468)
...........{t = fun(2,2468)
...............{t = fun(1, 2468)
...................{// x=1
........................return 1}
................t = 1
................f = 2 //1+1 //since *f_p is x
................x = t = 1
................return 2}
...........t = 2
...........f = 2+1
...........x = t = 2
...........return 3}
........t = 3
........f = 3+2
........x = t = 3
........return 5}
....t = 5
....f = 5+3
....x = t = 5
....return 8}

which implies fun (5,2468) is 8.




7)

 	
What happens when we try to compile the class definition in following code snippet?

class Birds {};
class Peacock : protected Birds {};

A. 	It will not compile because class body of Birds is not defined.
B. 	It will not compile because class body of Peacock is not defined.
C. 	It will not compile because a class cannot be protectedly inherited from other class.
D. 	It will compile succesfully.













Answer: Option D



8)Output of following program? 

Assume that the size of int is 4 bytes and size of double is 8 bytes, and there is no alignment done by the compiler.

#include<iostream> 
#include<stdlib.h> 
using namespace std; 
  
template<class T, class U, class V=double> 
class A  { 
    T x; 
    U y; 
    V z; 
    static int count; 
}; 
  
int main() 
{ 
   A<int, int> a; 
   A<double, double> b; 
   cout << sizeof(a) << endl; 
   cout << sizeof(b) << endl; 
   return 0; 
} 

(A)
16
24

(B)
8
16

(C)
20
28

(D) Compiler Error: template parameters cannot have default values.


Answer: (A)
Explanation: templates can also have default parameters. The rule is same all default values must be on the rightmost side.
Since count is static, it is not counted in sizeof. 



9)

#include <iostream> 
using namespace std; 
  
class Test { 
public: 
   Test() { cout << "Constructing an object of Test " << endl; } 
  ~Test() { cout << "Destructing an object of Test "  << endl; } 
}; 
  
int main() { 
  try { 
    Test t1; 
    throw 10; 
  } catch(int i) { 
    cout << "Caught " << i << endl; 
  } 
} 

(A) Caught 10

(B)
Constructing an object of Test 
Caught 10

(C)
Constructing an object of Test 
Destructing an object of Test 
Caught 10

(D) Compiler Error




Answer: (C)

Explanation: When an object is created inside a try block, destructor for the object is called before control is transferred to catch block.




10) Predict the output of following C++ program?

#include<iostream> 
using namespace std; 
  
class Test 
{ 
private: 
  int x; 
public: 
  Test() {x = 0;} 
  void destroy()  { delete this; } 
  void print() { cout << "x = " << x; } 
}; 
  
int main() 
{ 
  Test obj; 
  obj.destroy(); 
  obj.print(); 
  return 0; 
} 

(A) x = 0
(B) undefined behavior/segmentation fault
(C) compiler error
(D) None of these





Answer: (B)

Explanation:
delete operator works only for objects allocated using operator new.
If the object is created using new, then we can do delete this, otherwise behavior is undefined/segmentation fault



11) Given:

3. class A { }
4. class B extends A { }
5. public class ComingThru {
6. static String s = "-";
7. public static void main(String[] args) {
8. A[] aa = new A[2];
9. B[] ba = new B[2];
10. sifter(aa);
11. sifter(ba);
12. sifter(7);
13. System.out.println(s);
14. }
15. static void sifter(A[]... a2) { s += "1"; }
16. static void sifter(B[]... b1) { s += "2"; }
17. static void sifter(B[] b1) { s += "3"; }
18. static void sifter(Object o) { s += "4"; }
19. }
What is the result?
A. -124
B. -134
C. -424
D. -434
E. -444
F. Compilation fails

Answer:
D is correct. 
In general, overloaded var-args methods are chosen last. Remember that arrays are objects. 
Finally, an int can be boxed to an Integer and then "widened" to an Object.



12)

class Mixer {
Mixer() { }
Mixer(Mixer m) { m1 = m; }
Mixer m1;
public static void main(String[] args) {
Mixer m2 = new Mixer();
Mixer m3 = new Mixer(m2); m3.go();
Mixer m4 = m3.m1; m4.go();
Mixer m5 = m2.m1; m5.go();
}
void go() { System.out.print("hi "); }
}

What is the result?
A. hi
B. hi hi
C. hi hi hi
D. Compilation fails
E. hi, followed by an exception
F. hi hi, followed by an exception






Answer:
F is correct. 
The m2 object’s m1 instance variable is never initialized, so when m5 tries to
use it a NullPointerException is thrown.



13)
Given:
class Fizz {
int x = 5;
public static void main(String[] args) {
final Fizz f1 = new Fizz();
Fizz f2 = new Fizz();
Fizz f3 = FizzSwitch(f1,f2);
System.out.println((f1 == f3) + " " + (f1.x == f3.x));
}

static Fizz FizzSwitch(Fizz x, Fizz y) {
final Fizz z = x;
z.x = 6;
return z;
} }

What is the result?
A. true true
B. false true
C. true false
D. false false
E. Compilation fails
F. An exception is thrown at runtime






Answer:
A is correct. 

The references f1, z, and f3 all refer to the same instance of Fizz. 
The final modifier assures that a reference variable cannot be referred to a different object, 
but final doesn’t keep the object’s state from changing.



14)

Given:
class Bird {
{ System.out.print("b1 "); }
public Bird() { System.out.print("b2 "); }
}
class Raptor extends Bird {
static { System.out.print("r1 "); }
public Raptor() { System.out.print("r2 "); }
{ System.out.print("r3 "); }
static { System.out.print("r4 "); }
}
class Hawk extends Raptor {
public static void main(String[] args) {
System.out.print("pre ");
new Hawk();
System.out.println("hawk ");
}
}

What is the result?
A. pre b1 b2 r3 r2 hawk
B. pre b2 b1 r2 r3 hawk
C. pre b2 b1 r2 r3 hawk r1 r4
D. r1 r4 pre b1 b2 r3 r2 hawk
E. r1 r4 pre b2 b1 r2 r3 hawk
F. pre r1 r4 b1 b2 r3 r2 hawk
G. pre r1 r4 b2 b1 r2 r3 hawk
H. The order of output cannot be predicted
I. Compilation fails

Answer:
D is correct. Static init blocks are executed at class loading time, instance init blocks run
right after the call to super() in a constructor. When multiple init blocks of a single type
occur in a class, they run in order, from the top down.



15)
The _______ is the physical path over which a message travels.
		
A)Protocol
B)Medium
C)Signal
D)All of these











Ans-B




16)The information to be communicated in a data communications system is the _______.
		
A)	Medium
B)	Protocol
C)	Message
D)	Transmission










Ans-C



17) An unauthorized user is a network _______ issue.
		
A)	Performance
B)	Reliability
C)	Security
D)	All of these














Ans- C



18)Some of the tasks in the general problem-solving model are listed below. Which of the following list these tasks in the correct sequence?
		
A)	Problem definition, Finding solutions, Problem redefinition.
B)	Data gathering, Finding solutions, Finding ideas.
C)	Problem definition, Data gathering, Problem redefinition.
D)	Problem definition, Finding Solutions, Testing, Development
















Ans- C


19)Which of the following best describes the term life cycle model?
		
A)It describes the way requirements for an application change at different stages in the life of the organization.
B)It describes how a computerized information system is used during its lifetime.
C)It describes the phases through which a development project passes from the inception of the idea to completion of the product and its eventual decommissioning.
D) None of these









Ans- C



20)Which of the following is a true statement regarding a systems development project?
		
A)A systems development project is only concerned with developing a software system.
B)A systems development project is only concerned with developing systems for controlling devices or machines.
C)A systems development project may not involve software development.
D)A systems development project is only concerned with deployment only 













Ans-C

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/8th%2BJune%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/8th+June+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
