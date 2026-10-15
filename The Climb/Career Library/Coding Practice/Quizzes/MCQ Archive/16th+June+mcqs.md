---
kind: "study-reference"
title: "16th+June+mcqs"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/16th+June+mcqs.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 16th+June+mcqs

[[The Climb/Career Library/Career Library]]

1)

Consider the following declaration of a ‘two-dimensional array in C:

char a[100][100];  

Assuming that the main memory is byte-addressable and that the array is stored
starting from memory address 0, the address of a[40][50] is 

(A) 4040
(B) 4050
(C) 5040
(D) 5050


















Answer: (B)

Explanation:

Address of a[40][50] = Base address + 40*100*element_size + 50*element_size
                      = 0 + 4000*1 + 50*1
                     = 4050

Based on row major or column major
if row major then the result will be 4050
if column major then 
            Address of a[40][50] = Base address + 50*100*element_size + 40*element_size
                      = 0 + 5000*1 + 40*1
                     = 5040


2)
Predict the output of the below C program:

#include <stdio.h> 
#define SIZE(arr) sizeof(arr) / sizeof(*arr); 
void fun(int* arr, int n) 
{ 
    int i; 
    *arr += *(arr + n - 1) += 10; 
} 
  
void printArr(int* arr, int n) 
{ 
    int i; 
    for(i = 0; i < n; ++i) 
        printf("%d ", arr[i]); 
} 
  
int main() 
{ 
    int arr[] = {10, 20, 30}; 
    int size = SIZE(arr); 
    fun(arr, size); 
    printArr(arr, size); 
    return 0; 
} 

(A) 20 30 40
(B) 20 20 40
(C) 50 20 40
(D) Compile-time error







Answer: (C)


Explanation: 

The crux of the question lies in the expression: *arr += *(arr + n – 1) += 10;
The composite operator (here +=) has right to left associativity. First 10 is 
added to the last element of the array. 
The result is then added to the first element of the array.




3)Predict output of following C program

int main() 
{ 
    int i; 
    int arr[5] = {1}; 
    for (i = 0; i < 5; i++) 
        printf("%d ", arr[i]); 
    return 0; 
} 

(A) 1 followed by four garbage values
(B) 1 0 0 0 0
(C) 1 1 1 1 1
(D) 0 0 0 0 0







Answer: (B)

Explanation: 

In C/C++, if we initialize an array with fewer members, all remaining members
are automatically initialized as 0.

For example, the following statement initializes an array of size 1000 with values as 0.

     int arr[1000] = {0};  


 

 4)In C, fseek() should be preferred over rewind() mainly because

(A) rewind() doesn’t work for empty files
(B) rewind() may fail for large files
(C) In rewind, there is no way to check if the operations completed successfully
(D) All of the above









Answer: (C)




5)

What is time complexity of fun()?


int fun(int n) 
{ 
  int count = 0; 
  for (int i = n; i > 0; i /= 2) 
     for (int j = 0; j < i; j++) 
        count += 1; 
  return count; 
} 

(A) O(n^2)
(B) O(nLogn)
(C) O(n)
(D) O(nLognLogn)








Answer: (C)

Explanation: For a input integer n, the innermost statement of fun() is executed following times.

n + n/2 + n/4 + … 1

So time complexity T(n) can be written as

T(n) = O(n + n/2 + n/4 + … 1) = O(n)

The value of count is also n + n/2 + n/4 + .. + 1





6)

Consider the following C program

int main()  
{  
   int x, y, m, n;  
   scanf ("%d %d", &x, &y);  
   /* x > 0 and y > 0 */
   m = x; n = y;  
   while (m != n)  
   {  
      if(m>n)  
         m = m - n;  
      else
         n = n - m;  
   }  
   printf("%d", n);  
} 

What does the program compute? 
(A) x + y using repeated subtraction
(B) x mod y using repeated subtraction
(C) the greatest common divisor of x and y
(D) the least common multiple of x and y








Answer: (C)

Explanation: This is an implementation of Euclid’s algorithm to find GCD





7)
Is it fine to call delete twice for a pointer?

#include<iostream> 
using namespace std; 
  
int main() 
{ 
    int *ptr = new int; 
    delete ptr; 
    delete ptr; 
    return 0; 
}

(A) Yes
(B) No







Answer: (B)

Explanation: It is undefined behavior to call delete twice on a pointer.
Anything can happen, the program may crash or produce nothing. 



8)

What happens when a function throws an error but doesn’t specify it in the list of exceptions it can throw.

For example, what is the output of following program?

#include <iostream> 
using namespace std; 
  
// Ideally it should have been "int fun() (int)" 
int fun() 
{ 
    throw 10; 
} 
  
int main() 
{ 
    try
    { 
        fun(); 
    } 
    catch (int ) 
    { 
        cout << "Caught"; 
    } 
    return 0; 
} 

(A) Compiler Error
(B) No compiler Error. Output is “Caught”
(C) Segmentation fault
(D) None of these










Answer: (B)

Explanation: 

C++ compiler doesn’t check enforce a function to list the exceptions that it can throw. 

In Java, it is enforced.

It is up to the programmer to specify. Being a civilized programmer, a programmer should specify the list.



9)

Consider the function f defined below.

struct item  
{  
  int data;  
  struct item * next;  
};  
  
int f(struct item *p)  
{  
  return ( 
          (p == NULL) ||  
          (p->next == NULL) ||  
          (( P->data <= p->next->data) && f(p->next)) 
         );  
}  

For a given linked list p, the function f returns 1 if and only if 

(A) not all elements in the list have the same data value.
(B) the elements in the list are sorted in non-decreasing order of data value
(C) the elements in the list are sorted in non-increasing order of data value
(D) None of them






Answer: (B)

Explanation:
The function f() works as follows
1) If linked list is empty return 1
2) Else If linked list has only one element return 1
3) Else if node->data is smaller than equal to node->next->data and same thing holds for rest of the list then return 1
4) Else return 0



10)

Given:
1. class Loopy {
2. public static void main(String[] args) {
3. int[] x = {7,6,5,4,3,2,1};
4. // insert code here
5. System.out.print(y + " ");
6. }
7. } }
Which, inserted independently at line 4, compiles? (Choose all that apply.)

A. for(int y : x) {
B. for(x : int y) {
C. int y = 0; for(y : x) {
D. for(int y=0, z=0; z<x.length; z++) { y = x[z];
E. for(int y=0, int z=0; z<x.length; z++) { y = x[z];
F. int y = 0; for(int z=0; z<x.length; z++) { y = x[z];







Answer:
A, D, and F are correct. 
A is an example of the enhanced for loop. 
D and F are examples of the basic for loop.



11)

Given:
class Emu {
static String s = "-";
public static void main(String[] args) {
try {
throw new Exception();
} catch (Exception e) {
try {
try { throw new Exception();
} catch (Exception ex) { s += "ic "; }
throw new Exception(); }
catch (Exception x) { s += "mc "; }
finally { s += "mf "; }
} finally { s += "of "; }
System.out.println(s);
} }
What is the result?
A. -ic of
B. -mf of
C. -mc mf
D. -ic mf of
E. -ic mc mf of
F. -ic mc of mf
G. Compilation fails












Answer:
E is correct. 

There is no problem nesting try / catch blocks. As is normal, 
when an exception is thrown, the code in the catch block runs, then the code in the finally block runs.



12)

Given:

3. class SubException extends Exception { }
4. class SubSubException extends SubException { }
5.
6. public class CC { void doStuff() throws SubException { } }
7.
8. class CC2 extends CC { void doStuff() throws SubSubException { } }
9.
10. class CC3 extends CC { void doStuff() throws Exception { } }
11.
12. class CC4 extends CC { void doStuff(int x) throws Exception { } }
13.
14. class CC5 extends CC { void doStuff() { } }

What is the result? (Choose all that apply.)

A. Compilation succeeds
B. Compilation fails due to an error on line 8
C. Compilation fails due to an error on line 10
D. Compilation fails due to an error on line 12
E. Compilation fails due to an error on line 14






Answer:
C is correct. 
An overriding method cannot throw a broader exception than the method it's overriding. 

Class CC4's method is an overload, not an override.



13)

Given:
3. public class Ebb {
4. static int x = 7;
5. public static void main(String[] args) {
6. String s = "";
7. for(int y = 0; y < 3; y++) {
8. x++;
9. switch(x) {
10. case 8: s += "8 ";
11. case 9: s += "9 ";
12. case 10: { s+= "10 "; break; }
13. default: s += "d ";
14. case 13: s+= "13 ";
15. }
16. }
17. System.out.println(s);
18. }
19. static { x++; }
20. }

What is the result?
A. 9 10 d
B. 8 9 10 d
C. 9 10 10 d
D. 9 10 10 d 13
E. 8 9 10 10 d 13
F. 8 9 10 9 10 10 d 13
G. Compilation fails





Answer:
D is correct. 
Did you catch the static initializer block? 
Remember that switches work on "fall-thru" logic, and that fall-thru logic also applies to the default case, 
which is used when no other case matches.




14)

Given:
3. class Infinity { }
4. public class Beyond extends Infinity {
5. static Integer i;
6. public static void main(String[] args) {
7. int sw = (int)(Math.random() * 3);
8. switch(sw) {
9. case 0: { for(int x = 10; x > 5; x++)
10. if(x > 10000000) x = 10;
11. break; }
12. case 1: { int y = 7 * i; break; }
13. case 2: { Infinity inf = new Beyond();
14. Beyond b = (Beyond)inf; }
15. }
16. }
17. }
And given that line 7 will assign the value 0, 1, or 2 to sw, which are true? (Choose all that apply.)
A. Compilation fails
B. A ClassCastException might be thrown
C. A StackOverflowError might be thrown
D. A NullPointerException might be thrown
E. An IllegalStateException might be thrown
F. The program might hang without ever completing
G. The program will always complete without exception








Answer:
D and F are correct. 

Because i was not initialized, case 1 will throw an NPE. 
Case 0 will initiate an endless loop, not a stack overflow. 
Case 2's downcast will not cause an exception.



15)

Given:
3. public class Circles {
4. public static void main(String[] args) {
5. int[] ia = {1,3,5,7,9};
6. for(int x : ia) {
7. for(int j = 0; j < 3; j++) {
8. if(x > 4 && x < 8) continue;
9. System.out.print(" " + x);
10. if(j == 1) break;
11. continue;
12. }
13. continue;
14. }
15. }
16. }

What is the result?
A. 1 3 9
B. 5 5 7 7
C. 1 3 3 9 9
D. 1 1 3 3 9 9
E. 1 1 1 3 3 3 9 9 9
F. Compilation fails





Answer:
D is correct. 

The basic rule for unlabeled continue statements is that the current iteration stops early and execution jumps to the next iteration. 
The last two continue statements are redundant!



16) Which is/are correct statements about primary key of a table?

    A)Primary keys can contain NULL values
    B) Primary keys cannot contain NULL values.
    C) A table can have only one primary key with single or multiple fields
    D) A table can have multiple primary keys with single or multiple fields












Answer: B and C



17)What is Granularity?

A) The size of data items
B) The size of database
C) The size of record
D) The size of file












Answer: B 

The size of database 




18)

A relational schema for a train reservation database is given below.
Passenger (pid, pname, age)
Reservation (pid, class, tid)

Table: Passenger
pid   pname   age
-----------------
 0    Sachin   65
 1    Rahul    66
 2    Sourav   67
 3    Anil     69

Table : Reservation
pid  class  tid
---------------
 0    AC   8200
 1    AC   8201
 2    SC   8201
 5    AC   8203
 1    SC   8204
 3    AC   8202

What pids are returned by the following SQL query for the above instance of the tables?

SLECT pid
FROM Reservation ,
WHERE class ‘AC’ AND
    EXISTS (SELECT *
       FROM Passenger
       WHERE age > 65 AND
       Passenger. pid = Reservation.pid)

(A) 1, 0
(B) 1, 2
(C) 1, 3
(D) 1, 5














Answer: (C)

Explanation: 

When a subquery uses values from outer query, the subquery is called correlated subquery. 
The correlated subquery is evaluated once for each row processed by the outer query.




19)Consider the following relational schema:

Suppliers(sid:integer, sname:string, city:string, street:string)
Parts(pid:integer, pname:string, color:string)
Catalog(sid:integer, pid:integer, cost:real)

Consider the following relational query on the above database:

SELECT S.sname
    FROM Suppliers S
        WHERE S.sid NOT IN (SELECT C.sid
                            FROM Catalog C
                            WHERE C.pid NOT IN (SELECT P.pid  
                                                FROM Parts P
                                                WHERE P.color<> 'blue'))

Assume that relations corresponding to the above schema are not empty. Which one of the following is the correct interpretation of the above query?
(A) Find the names of all suppliers who have supplied a non-blue part.
(B) Find the names of all suppliers who have not supplied a non-blue part.
(C) Find the names of all suppliers who have supplied only blue parts.
(D) Find the names of all suppliers who have not supplied only blue parts.








Answer: (D)

Explanation: None option matched because given query returns suppliers who have
not supplied any blue parts. 

That means it can include other than blue parts.




20)

Consider the table employee(empId, name, department, salary) and the two queries Q1 ,Q2 below. 

Assuming that department 5 has more than one employee, and we want to find the employees who get 
higher salary than anyone in the department 5, which one of the statements is TRUE for any arbitrary employee table?

Q1 : Select e.empId
     From employee e
     Where not exists
        (Select * From employee s where s.department = “5” and 
                                        s.salary >=e.salary)
Q2 : Select e.empId
     From employee e
     Where e.salary > Any
    (Select distinct salary From employee s Where s.department = “5”)


(A) Q1 is the correct query
(B) Q2 is the correct query
(C) Both Q1 and Q2 produce the same answer.
(D) Neither Q1 nor Q2 is the correct query


Answer: (A)

Explanation: First note that they asked for Anyone (= All) not for Any.
Here, Everyone means all of the group.
Anyone means all or any part of the group.

Let the employee(empId, name, department, salary) have the following instance.

empId name department salary
———————————-


e1 ------- A-------- 1---------10000
e2 -------B ------- 5 ---------5000
e3 -------C ------- 5----------7000
e4 -------D ------- 2----------2000
e5 -------E ------- 3----------6000

Now the actual result should contain empId : e1 , e3 and e5 ( because they have salary greater than anyone employee in the department ‘5’)

——————————————————–
Now Q1 :

Note : EXISTS(empty set) gives FALSE, and NOT EXISTS(empty set) gives TRUE.

Select e.empId
From employee e
Where not exists
(Select * From employee s where s.department = “5” and
s.salary >=e.salary)

Q1 will result only empId e1.
———————————————————
whereas Q2 :

Select e.empId
From employee e
Where e.salary > Any
(Select distinct salary From employee s Where s.department = “5”)

Q2 will result empId e1, e3 and e5.
——————————————————–
Hence Q1 is the correct query.

Note that if we use ALL in place of Any in second query then this will be correct.

Option (A) is correct.

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/16th%2BJune%2Bmcqs.txt) · CODING RESOURCES/Quiz Mcqs/16th+June+mcqs.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
