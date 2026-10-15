---
kind: "study-reference"
title: "2nd+June+MCQs"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/2nd+June+MCQs.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 2nd+June+MCQs

[[The Climb/Career Library/Career Library]]

1)

Suppose that in a C program snippet, followings statements are used.

i) sizeof(int); 
ii) sizeof(int*); 
iii) sizeof(int**); 

Assuming size of pointer is 4 bytes and size of int is also 4 bytes, pick the most correct answer from the given options.

(A) Only i) would compile successfully and it would return size as 4.
(B) i), ii) and iii) would compile successfully and size of each would be same i.e. 4
(C) i), ii) and iii) would compile successfully but the size of each would be different and would be decided at run time.
(D) ii) and iii) would result in compile error but i) would compile and result in size as 4.

















Answer: (B)

Explanation: Size of all pointer types is same.

And whether it is a ‘pointer to char’ or ‘pointer to int’ or ‘pointer to pointer to int’, the size always remain same.



2)
In the context of the following printf() in C, pick the best statement.

i) printf("%d",8); 
ii) printf("%d",090); 
iii) printf("%d",00200); 
iv) printf("%d",0007000); 

(A) Only i) would compile. And it will print 8.
(B) Both i) and ii) would compile. i) will print 8 while ii) will print 90
(C) All i), ii), iii) and iv) would compile successfully and they will print 8, 90, 200 & 7000 respectively.
(D) Only i), iii) and iv) would compile successfully. They will print 8, 128 and 3584 respectively.













Answer: (D)



3)

A typical "switch" body looks as follows:

switch (controlling_expression) 
{ 
  case label1: 
    /*label1 statements*/
    break; 
  case label2: 
    /*label1 statements*/
    break; 
  default: 
    /*Default statements*/
} 

Which of the following statement is not correct statement?
(A) "switch" body may not have any "case" label at all and it would still compile.
(B) "switch" body may not have the "default" label and it would still compile.
(C) "switch" body may contain more than one "case" labels where the label value of these "case" is same and it would still compile. 
      If "switch" controlling expression results in this "case" label value, the "case" which is placed first would be executed.
(D) "switch" body may not have any "break" statement and it would still compile.
(E) "switch" body can have the "default" label at first i.e. before all the other "case" labels. It would still compile.




Answer: (C)

Explanation: In "switch" body, two "case" can’t result in same value. Though having only "case" or only "default" is okay. In fact, "switch" body can be empty also.




4)

Choose the best statement with respect to following three program snippets in C Language

/*Program Snippet 1 with for loop*/
for (i = 0; i < 10; i++) 
{ 
   /*statement1*/
   continue; 
   /*statement2*/
} 
  
/*Program Snippet 2 with while loop*/
i = 0; 
while (i < 10) 
{ 
   /*statement1*/
   continue; 
   /*statement2*/
   i++; 
} 
  
/*Program Snippet 3 with do-while loop*/
i = 0; 
do
{ 
   /*statement1*/
   continue; 
   /*statement2*/
   i++; 
}while (i < 10); 

(A) All the loops are equivalent i.e. any of the three can be chosen and they all will perform exactly same.
(B) continue can’t be used with all the three loops in C.
(C) After hitting the continue; statement in all the loops, the next expression to be executed would be controlling expression (i.e. i < 10) in all the 3 loops.
(D) None of the above is correct.





Answer: (D)



5) output of the following  in  C 
#include <stdio.h> 
int main() 
{ 
   const int x; 
   x = 10; 
   printf("%d", x); 
   return 0; 
} 

(A) Compiler Error
(B) 10
(C) 0
(D) Runtime Error






Answer: (A)



6)

#include<iostream> 
using namespace std; 
  
int &fun() 
{ 
    int x = 10; 
    return x; 
} 
int main() 
{ 
    fun() = 30; 
    cout << fun(); 
    return 0; 
} 

(A) May cause runtime error
(B) May cause compiler error
(C) Always works fine.
(D) 0





Answer: (A)




7)Which of the following overloaded functions are NOT allowed in C++?

1) Function declarations that differ only in the return type

    int fun(int x, int y);
         void fun(int x, int y); 

2) Functions that differ only by static keyword in return type
         int fun(int x, int y);
         static int fun(int x, int y); 

3)Parameter declarations that differ only in a pointer * versus an array []

int fun(int *ptr, int n);
int fun(int ptr[], int n); 

4) Two parameter declarations that differ only in their default arguments

int fun( int x, int y); 
int fun( int x, int y = 10); 

(A) All of the above
(B) All except 2)
(C) All except 1)
(D) All except 2 and 4






Answer: (A)




8)

Which of the following is true in CPP?

(A) Static methods cannot be overloaded.
(B) Static data members can only be accessed by static methods.
(C) Non-static data members can be accessed by static methods.
(D) Static methods can only access static members (data and methods)













Answer: (D)





9)Which of the following is aggregate function in SQL?
(A) Avg
(B) Select
(C) Ordered by
(D) distinct







Answer: (A)


10)What does below SQL statement describe?

SELECT CustomerName, Address + ‘, ‘ + City + ‘, ‘ + Country AS Address
 FROM Customers;

    (A) Alias named Address column will be created and under this Address, City and Country will be printed as combined statement.
    (B) Alias named Address will be created for Country columns
    (C) Alias named Address column will be created and under this all CustomerName, address, city and country will be printed as combined statement
    (D) All of these are wrong 















Answer: A



11) Logical operators used in SQL are

    (A) AND, OR , NOT
    (B) &&, ||, !
    (C) $,|,!
    (D) None of these










Answer: A



12)Which is called as a virtual table in SQL?

   (A) INNER JOIN
   (B) JOIN
   (C) VIEW
   (D) None of these












   Answer: C



 13)Which method names follow the JavaBeans standard? (Choose all that apply.)

A. addSize
B. getCust
C. deleteRep
D. isColorado
E. putDimensions














Answer:
B and D use the valid prefixes 'get' and 'is'.


A is incorrect because 'add' can be used only with Listener methods. 
C and E are incorrect because 'delete' and 'put' are not standard JavaBeans name prefixes.




14)Given:
1. class Voop {
2. public static void main(String[] args) {
3. doStuff(1);
4. doStuff(1,2);
5. }
6. // insert code here
7. }

Which, inserted independently at line 6, will compile? (Choose all that apply.)
A. static void doStuff(int... doArgs) { }
B. static void doStuff(int[] doArgs) { }
C. static void doStuff(int doArgs...) { }
D. static void doStuff(int... doArgs, int y) { }
E. static void doStuff(int x, int... doArgs) { }









Answer:
A and E use valid var-args syntax.
B and C are invalid var-arg syntax, and D is invalid because the var-arg must be the last
of a method's arguments.




15)Given:
1. enum Animals {
2. DOG("woof"), CAT("meow"), FISH("burble");
3. String sound;
4. Animals(String s) { sound = s; }
5. }
6. class TestEnum {
7. static Animals a;
8. public static void main(String [] args) {
9. System.out.println(a.DOG.sound + " " + a.FISH.sound);
10. }
11. }

What is the result?
A. woof burble
B. Multiple compilation errors
C. Compilation fails due to an error on line 2
D. Compilation fails due to an error on line 3
E. Compilation fails due to an error on line 4
F. Compilation fails due to an error on line 9

Answer:
A is correct; enums can have constructors and variables.
B, C, D, E, and F are incorrect; these lines all use correct syntax.








16)

Given two files:

1. package pkgA;
2. public class Foo {
3. int a = 5;
4. protected int b = 6;
5. public int c = 7;
6. }

3. package pkgB;
4. import pkgA.*;
5. public class Baz {
6. public static void main(String[] args) {
7. Foo f = new Foo();
8. System.out.print(" " + f.a);
9. System.out.print(" " + f.b);
10. System.out.print(" " + f.c);
11. }
12. }

What is the result? (Choose all that apply.)
A. 5 6 7
B. 5 followed by an exception
C. Compilation fails with an error on line 7
D. Compilation fails with an error on line 8
E. Compilation fails with an error on line 9
F. Compilation fails with an error on line 10













Answer:
D and E are correct. 
Variable a has default access, so it cannot be accessed from outside the package. 
Variable b has protected access in pkgA.
A, B, C, and F are incorrect based on the above information.


17)
Which of the following allows objects to change type within the subtyping structure
	a)	Static classification
	b)	Dynamic classification
	c)	Depends on the scenario
	d)	None of these












Ans – b



18)Interaction diagram captures the behavior of a __________

a)	Multiple Use case
b)	Single Use case
c)	Only selected Use cases
d)	None of these














Ans-b



19)
Generalization is a

a) has a relationship
b) is a relationship
c) depends on scenario
d) none of these














ans-b




20)What can be requested from any object of the class to affect behavior?
a) object
b) attribute
c) operation
d) instance


















Answer: c
Explanation: An operation is the implementation of a service that can be requested from any object of the class to affect behavior.

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/2nd%2BJune%2BMCQs.txt) · CODING RESOURCES/Quiz Mcqs/2nd+June+MCQs.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
