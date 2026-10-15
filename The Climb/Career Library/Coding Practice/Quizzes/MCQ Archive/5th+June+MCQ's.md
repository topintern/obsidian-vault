---
kind: "study-reference"
title: "5th+June+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/5th+June+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 5th+June+MCQ's

[[The Climb/Career Library/Career Library]]

1)

Find out the correct statement for the following program.
#include <stdio.h>
  
int * gPtr; 
  
int main() 
{ 
 int * lPtr = NULL; 
  
 if(gPtr == lPtr) 
 { 
   printf("Equal!"); 
 } 
 else
 { 
  printf("Not Equal"); 
 } 
  
 return 0; 
} 

(A) It’ll always print Equal.
(B) It’ll always print Not Equal.
(C) Since gPtr isn’t initialized in the program, it’ll print sometimes Equal and at other times Not Equal.
(D) Segmentation fault



Answer: (A)

Explanation: It should be noted that global variables such gPtr (which is a
global pointer to int) are initialized to ZERO. 
That’s why gPtr (which is a global pointer and initialized implicitly) and lPtr
(which a is local pointer and initialized explicitly) would have same value 
i.e. correct answer is a.




2)Pick the best statement for the below:

int arr[50] = {0,1,2,[47]=47,48,49}; 

(A) This isn’t allowed in C and it’ll give compile error
(B) This is allowed in C as per standard. 
(C)  Segementation fault
(D) None of these







Answer: (B)
Basically, it’ll initialize arr[0], arr[1], arr[2], arr[47], arr[48] and arr[49] to 0,1,2,47,48 and 49 respectively. 

The remaining elements of the array would be initialized to 0.




3)
Pick the best statement for the below program:

#include<stdio.h>
  
int main() 
{ 
 struct {int a[2], b;} arr[] = {[0].a = {1}, [1].a = {2}, [0].b = 1, [1].b = 2}; 
  
 printf("%d %d %d and",arr[0].a[0],arr[0].a[1],arr[0].b); 
 printf("%d %d %d\n",arr[1].a[0],arr[1].a[1],arr[1].b); 
  
 return 0; 
} 

(A) Compile error because struct type (containing two fields i.e. an array of int and an int) has been specified along with the definition of array arr[] of this struct type.
(B) Compile error because of incorrect syntax for initialization of array arr[].
(C) No compile error and two elements of arr[] would be defined and initialized. Output would be "1 0 1 and 2 0 2".
(D) No compile error and two elements of arr[] would be defined and initialized. Output would be "1 X 1 and 2 X 2" where X is some garbage random number.










Answer: (C)

Explanation: In C, designators can be used to provide explicit initialization. 
For an array, elements which aren’t initialized explicitly in program are set as ZERO. 
That’s why correct answer is C.




4)
#include<stdio.h> 
void print(int n) 
{ 
    if (n > 4000) 
        return; 
    printf("%d ", n); 
    print(2*n); 
    printf("%d ", n); 
} 
  
int main() 
{ 
    print(1000); 
    getchar(); 
    return 0; 
} 

(A) 1000 2000 4000
(B) 1000 2000 4000 4000 2000 1000
(C) 1000 2000 4000 2000 1000
(D) 1000 2000 2000 1000







Answer: (B)



5)Number of comparisons required for an unsuccessful search of an element in a sequential search, organized, fixed length, symbol table of length L is

(A) L
(B) L/2
(C) (L+1)/2
(D) 2L











Answer: (A)

Explanation: 

In Sequential search, in order to find a particular element, each element of the table is searched sequentially until the desired element is not found.

So, in case of an unsuccessful search, 
the element would be searched until the last element and it would be a worst case when number of searches are equal to the size of the table.

So, option (A) is correct.



6)

Output of following program? Assume that the size of char is 1 byte and size of int is 4 bytes, and there is no alignment done by the compiler.

#include<iostream> 
#include<stdlib.h> 
using namespace std; 
  
template<class T, class U> 
class A  { 
    T x; 
    U y; 
    static int count; 
}; 
  
int main()  { 
   A<char, char> a; 
   A<int, int> b; 
   cout << sizeof(a) << endl; 
   cout << sizeof(b) << endl; 
   return 0; 
} 

(A)
6
12

(B)
2
8

(C) Compiler Error: There can not be more than one template arguments.

(D)
8
8


Answer: (B)

Explanation: Since count is static, it is not counted in sizeof.




7)

Would destructor be called, if yes, then due to which vector?

#include <iostream> 
#include <vector> 
using namespace std; 
  
class a 
{ 
public : 
    ~a() 
    { 
        cout << "destroy"; 
    } 
}; 
int main() 
{ 
   vector <a*> *v1  = new vector<a*>; 
   vector <a> *v2  = new vector<a>; 
   return 0; 
}

(A) v1
(B) v2
(C) v1 and v2
(D) no destructor call









Answer: (D) 



8)
#include<iostream> 
using namespace std; 
int main () 
{ 
       int cin; 
       cin >> cin; 
       cout << "cin" << cin; 
       return 0; 
} 


(A) error in using cin keyword
(B) cin+junk value/0 
(C) cin+input
(D) Runtime error










Answer: (B)


9)

A member function can always access the data in __________ , (in C++).
(A) the class of which it is member
(B) the object of which it is a member
(C) the public part of its class
(D) the private part of its class












Answer: (A)

Explanation: A member function can access it’s class member variables, irrespective of the access specifier in which the member variable is declared.
So, a member function can always access the data in the class of which it is a member.

So, option (A) is correct.



10)

Given:
3. public class Tenor extends Singer {
4. public static String sing() { return "fa"; }
5. public static void main(String[] args) {
6. Tenor t = new Tenor();
7. Singer s = new Tenor();
8. System.out.println(t.sing() + " " + s.sing());
9. }
10. }
11. class Singer { public static String sing() { return "la"; } }

What is the result?
A. fa fa
B. fa la
C. la la
D. Compilation fails
E. An exception is thrown at runtime






Answer:
 B is correct. The code is correct, but polymorphism doesn’t apply to static methods.



11)

Given:

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

C is correct. Watch out, SubSubAlpha extends Alpha! Since the code doesn’t attempt
to make a SubAlpha, the private constructor in SubAlpha is okay.


12. Given:

3. class Building {
4. Building() { System.out.print("b "); }
5. Building(String name) {
6. this(); System.out.print("bn " + name);
7. }
8. }
9. public class House extends Building {
10. House() { System.out.print("h "); }
11. House(String name) {
12. this(); System.out.print("hn " + name);
13. }
14. public static void main(String[] args) { new House("x "); }
15. }

What is the result?

A. h hn x
B. hn x h
C. b h hn x
D. b hn x h
E. bn x h hn x
F. b bn x h hn x
G. bn x b h hn x
H. Compilation fails












Answer:
C is correct. Remember that constructors call their superclass constructors, which execute first, 
and that constructors can be overloaded.




13) Given:

3. class Mammal {
4. String name = "furry ";
5. String makeNoise() { return "generic noise"; }
6. }
7. class Zebra extends Mammal {
8. String name = "stripes ";
9. String makeNoise() { return "bray"; }
10. }
11. public class ZooKeeper {
12. public static void main(String[] args) { new ZooKeeper().go(); }
13. void go() {
14. Mammal m = new Zebra();
15. System.out.println(m.name + m.makeNoise());
16. }
17. }

What is the result?
A. furry bray
B. stripes bray
C. furry generic noise
D. stripes generic noise
E. Compilation fails
F. An exception is thrown at runtime





Answer:
A is correct. Polymorphism is only for instance methods.




14)

You’re designing a new online board game in which Floozels are a type of Jammers, 
Jammers can have Quizels,
Quizels are a type of Klakker, 
and Floozels can have several Floozets. 

Which of the following fragments represent this design? (Choose all that apply.)

A. import java.util.*;
interface Klakker { }
class Jammer { Set<Quizel> q; }
class Quizel implements Klakker { }
public class Floozel extends Jammer { List<Floozet> f; }
interface Floozet { }

B. import java.util.*;
class Klakker { Set<Quizel> q; }
class Quizel extends Klakker { }
class Jammer { List<Floozel> f; }
class Floozet extends Floozel { }
public class Floozel { Set<Klakker> k; }

C. import java.util.*;
class Floozet { }
class Quizel implements Klakker { }
class Jammer { List<Quizel> q; }
interface Klakker { }
class Floozel extends Jammer { List<Floozet> f; }

D. import java.util.*;
interface Jammer extends Quizel { }
interface Klakker { }
interface Quizel extends Klakker { }
interface Floozel extends Jammer, Floozet { }
interface Floozet { }


Answer:

A and C are correct. 

The phrase "type of" indicates an "is-a" relationship (extends or implements), and 
the phrase “have” is of course a "has-a" relationship (usually instance variables).



15)

In the relational model, relationships between relations or tables are created by using:

A.composite keys.
B.determinants.
C.candidate keys.
D.foreign keys.













Ans- D




16)

SQL views can be used to hide:

A.columns and rows only.
B.complicated SQL syntax only.
C.Both columns and rows as well as  complicated SQL syntax can be hidden by an SQL view.
D.None of these





Ans- C




17)

Which of the following is NOT a basic element of all versions of the E-R model?
A.Entities
B.Attributes
C.Relationships
D.Primary keys







Ans- D



18)

How many tables may be included with a join?
A.One
B.Two
C.Three
D.All of these





Ans- D




19) 

A ______________ is a physical element that exists at run time and represents a computational resource.
A. Node
B. Component
C. Object
D. Interface






Answer: A


20)

A use case diagram is used to model __________ of a system.
A. Structure
B. Behavior
C. State
D. Interface







Answer: B

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/5th%2BJune%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/5th+June+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
