---
kind: "study-reference"
title: "18th+June+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/18th+June+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 18th+June+MCQ's

[[The Climb/Career Library/Career Library]]

1)

Output of following C program?

#include <stdio.h> 
int f1() { printf ("hello"); return 1;} 
int f2() { printf ("welcome"); return 1;} 
  
int main() 
{ 
  int p = f1() + f2(); 
  return 0; 
} 

(A) hellowelcome
(B) welcomehello
(C) Compiler Dependent
(D) Compiler Error














Answer: (C)

Explanation: 

The operator ‘+’ doesn’t have a standard defined order of evaluation for its operands. 
Either f1() or f2() may be executed first. 
So a compiler may choose to output either hellowelcome or welcomehello.



2)

Predict the output of following C program

#include <stdio.h> 
int main() 
{ 
    char a = '\012'; 
  
    printf("%d", a); 
  
    return 0; 
} 

(A) Compiler Error
(B) 12
(C) 10
(D) Empty









Answer: (C)

Explanation: 

The value ‘\012’ means the character with value 12 in octal, which is decimal 10.
Note: It is equivalent to char a = 012 and int a = ‘\012’ and int a = 012. 




3)


#include <stdio.h> 
int main() 
{ 
    if (sizeof(int) > -1) 
        printf("Yes"); 
    else
        printf("No"); 
    return 0; 
} 

(A) Yes
(B) No
(C) Compiler Error
(D) Runtime Error











Answer: (B)

Explanation: 

In C, when an integer value is compared with an unsigned it, the int is promoted to unsigned. 
Negative numbers are stored in 2’s complement form and unsigned value of the 2’s complement form is much higher than the sizeof int.




4)

Predict the output of the following program:

#include <stdio.h> 
int main() 
{ 
    char str[] = "%d %c", arr[] = "GreatQuee"; 
    printf(str, 0[arr], 2[arr + 3]); 
    return 0; 
} 

(A) G Q
(B) 71 81
(C) 71 Q
(D) Compile-time error










Answer: (C)

Explanation:

The statement printf(str, 0[arr], 2[arr + 3]); boils down to:
printf("%d %c, 0["GreatQuee"], 2["GreatQuee" + 3]);
Which is further interpreted as:
printf("%d %c, *(0 + "GreatQuee"), *(2 + "GreatQuee" + 3));
Which prints the ascii value of 'G' and character 'Q'.



5)

Predict the output of following C program, assume that a character takes 1 byte and pointer takes 4 bytes.

#include <stdio.h> 
int main() 
{ 
    char *str1 = "helloworld"; 
    char str2[] = "helloworld"; 
    char *str3='K';
  
    printf("sizeof(str1) = %d, sizeof(str2) = %d, sizeof(str3) = %d ", sizeof(str1), sizeof(str2),sizeof(str3)); 
  
    return 0; 
} 

(A) sizeof(str1) = 11, sizeof(str2) = 11, sizeof(str3) = 1
(B) sizeof(str1) = 4, sizeof(str2) = 11, sizeof(str3) = 4
(C) sizeof(str1) = 4, sizeof(str2) = 4, sizeof(str3) = 1
(D) sizeof(str1) = 11, sizeof(str2) = 4, sizeof(str3) = 4







Answer: (B)

Explanation: str1,str3 is a pointer and str2 is an array.




6)


#include<iostream> 
using namespace std; 
int x = 1; 
void fun() 
{ 
    int x = 2; 
    { 
        int x = 3; 
        cout << x << endl; 
	cout << ::x << endl;
    } 
} 
int main() 
{ 
    fun(); 
    return 0; 
} 

(A) 3 1
(B) 2 3
(C) 3 3
(D) 0 3





Answer: (A)

Explanation: 

The value of ::x is 1. 
And only x refers to the block in which it is defined, which is 3 here 

The scope resolution operator when used with a variable name, always refers to global variable.




7)
In the following CPP program f() is overloaded.?

#include<iostream>
using namespace std;
void f(unsigned int x) {
cout<<"one "<<x;
}

void f(signed int x) { 
   cout<<"two "<<x;
}

int main() {
f(20);
return 1;
}

A)Compilation fails
B) one 20
C) two 20
D) Run time error/Segmentation fault











Answer : C





8)  What is the output of the following program?

#include<iostream>
using namespace std;

class Base {
public:
   void f() {
      cout<<"Base\n";
   }
};

class Derived:private Base {
public:
   void f() {
      cout<<"Derived\n";
   }
};
main() {
   Base *p = new Derived(); 
   p->f();
}

A - Base
B - Derived
C - Compile error
D - None of the above.
















Answer : C

Explaination
Here Base is privately Inherited 



9)

What is the output of the following program?

#include<iostream>
using namespace std;

void main() {
   char s[] = "Fine";
	*s = 'N';
   
   cout<<s<<endl;
}

A - Fine
B - Nine
C - Compile error
D - Runtime error








Answer : B

Explaination
*s=’N’, changes the character at base address to ‘N’.



10)A class can contain objects of other classes and this phenomenon is called_________ .

a. Relationship
b. Object Association
c. Containership
d. None of these 










Ans- C



11)
Given:
3. public class OverAndOver {
4. static String s = "";
5. public static void main(String[] args) {
6. try {
7. s += "1";
8. throw new Exception();
9. } catch (Exception e) { s += "2";
10. } finally { s += "3"; doStuff(); s += "4";
11. }
12. System.out.println(s);
13. }
14. static void doStuff() { int x = 0; int y = 7/x; }
15. }
What is the result?
A. 12
B. 13
C. 123
D. 1234
E. Compilation fails
F. 123 followed by an exception
G. 1234 followed by an exception
H. An exception is thrown with no other output










Answer:
H is correct. 

It's true that the value of String s is 123 at the time that the divide-byzero exception is thrown, 
but finally() is not guaranteed to complete, and in this case
finally() never completes, so the System.out.println (S.O.P.) never executes.



12)Given:

3. public class Wind {
4. public static void main(String[] args) {
5. foreach:
6. for(int j=0; j<5; j++) {
7. for(int k=0; k< 3; k++) {
8. System.out.print(" " + j);
9. if(j==3 && k==1) break foreach;
10. if(j==0 || j==2) break;
11. }
12. }
13. }
14. }

What is the result?
A. 0 1 2 3
B. 1 1 1 3 3
C. 0 1 1 1 2 3 3
D. 1 1 1 3 3 4 4 4
E. 0 1 1 1 2 3 3 4 4 4
F. Compilation fails









Answer:

C is correct. 
A break breaks out of the current innermost loop and continues. 
A labeled break breaks out of and terminates the current loops.





13)

Given:
3. public class Gotcha {
4. public static void main(String[] args) {
5. // insert code here
6.
7. }
8. void go() {
9. go();
10. }
11. }

And given the following three code fragments:

I. new Gotcha().go();

II. try { new Gotcha().go(); }
catch (Error e) { System.out.println("ouch"); }

III. try { new Gotcha().go(); }
catch (Exception e) { System.out.println("ouch"); }

When fragments I - III are added, independently, at line 5, which are true? (Choose all that apply.)

A. Some will not compile
B. They will all compile
C. All will complete normally
D. None will complete normally
E. Only one will complete normally
F. Two of them will complete normally










Answer:
B and E are correct. 

First off, go() is a badly designed recursive method, guaranteed to cause a
StackOverflowError. 
Since Exception is not a superclass of Error, catching an Exception will not
help handle an Error, so fragment III will not complete normally.
Only fragment II will catch the Error.



14)

Given:
3. public class Clumsy {
4. public static void main(String[] args) {
5. int j = 7;
6. assert(++j > 7);
7. assert(++j > 8): "hi";
8. assert(j > 10): j=12;
9. assert(j==12): doStuff();
10. assert(j==12): new Clumsy();
11. }
12. static void doStuff() { }
13. }

Which are true? (Choose all that apply.)
A. Compilation succeeds
B. Compilation fails due to an error on line 6
C. Compilation fails due to an error on line 7
D. Compilation fails due to an error on line 8
E. Compilation fails due to an error on line 9
F. Compilation fails due to an error on line 10









Answer: E is correct. 

When an assert statement has two expressions, the second expression must return a value. 
The only two-expression assert statement that doesn’t return a value is on line 9.



15)
Given:

1. public class Frisbee {
2. // insert code here
3. int x = 0;
4. System.out.println(7/x);
5. }
6. }

And given the following four code fragments:
I. public static void main(String[] args) {
II. public static void main(String[] args) throws Exception {
III. public static void main(String[] args) throws IOException {
IV. public static void main(String[] args) throws RuntimeException {

If the four fragments are inserted independently at line 4, which are true? (Choose all that apply.)
A. All four will compile and execute without exception
B. All four will compile and execute and throw an exception
C. Some, but not all, will compile and execute without exception
D. Some, but not all, will compile and execute and throw an exception
E. When considering fragments II, III, and IV, of those that will compile, adding a try/catch block around line 6 will cause compilation to fail










Answer: D is correct. 

If you're going to throw an IOException, you have to import the java.io package or declare the exception with a fully qualified name.
E is incorrect because it's okay to both handle and declare an exception. 



16)

Given:
2. class MyException extends Exception { }
3. class Tire {
4. void doStuff() { }
5. }
6. public class Retread extends Tire {
7. public static void main(String[] args) {
8. new Retread().doStuff();
9. }
10. // insert code here
11. System.out.println(7/0);
12. }
13. }

And given the following four code fragments:

I. void doStuff() {
II. void doStuff() throws MyException {
III. void doStuff() throws RuntimeException {
IV. void doStuff() throws ArithmeticException {

When fragments I - IV are added, independently, at line 10, which are true? (Choose all that apply.)

A. None will compile
B. They will all compile
C. Some, but not all, will compile
D. All of those that compile will throw an exception at runtime
E. None of those that compile will throw an exception at runtime
F. Only some of those that compile will throw an exception at runtime







Answer: C and D are correct. 

An overriding method cannot throw checked exceptions that are broader than those thrown by the overridden method. 
However an overriding method can throw RuntimeExceptions not thrown by the overridden method.




17)

Consider the following relational schema:

  employee(empId, empName, empDept)
  customer(custId, custName, salesRepId, rating)

salesRepId is a foreign key referring to empId of the employee relation. 
Assume that each employee makes a sale to at least one customer. 

What does the following query return?

SELECT empName
       FROM employee E
       WHERE NOT EXISTS ( SELECT custId
                          FROM customer C
                          WHERE C.salesRepId = E.empId
                            AND C.rating <> 'GOOD');

(A) Names of all the employees with at least one of their customers having a ‘GOOD’ rating.
(B) Names of all the employees with at most one of their customers having a ‘GOOD’ rating.
(C) Names of all the employees with none of their customers having a ‘GOOD’ rating.
(D) Names of all the employees with all their customers having a ‘GOOD’ rating.








Answer: (D)

Explanation: 

If any employee has received rating other than ‘GOOD’ from any of their customers, then there will be some rows returned by the inner query;
And NOT EXISTS will return false so those employees won’t be printed.
Only those employees which have got rating ‘GOOD’ from all of their customers will be printed.




18)

Consider the relation account (customer, balance) where customer is a primary key and there are no null values. 

We would like to rank customers according to decreasing balance. 

The customer with the largest balance gets rank 1. ties are not broke but ranks are skipped: 
if exactly two customers have the largest balance they each get rank 1 and rank 2 is not assigned

Query1:
  select A.customer, count(B.customer)
  from account A, account B
  where A.balance <=B.balance
  group by A.customer

Query2:
  select A.customer, 1+count(B.customer)
  from account A, account B
  where A.balance < B.balance
  group by A.customer 

Consider these statements about Query1 and Query2.

1. Query1 will produce the same row set as Query2 for some but not all databases.
2. Both Query1 and Query2 are correct implementation of the specification
3. Query1 is a correct implementation of the specification but Query2 is not
4. Neither Query1 nor Query2 is a correct implementation of the specification
5. Assigning rank with a pure relational query takes less time than scanning in decreasing balance order assigning ranks using ODBC. 

Which two of the above statements are correct?
(A) 2 and 5
(B) 1 and 3
(C) 1 and 4
(D) 3 and 5









Answer: (C)

Explanation: 

Query 1 and Query 2 will give the same result if all the customers have distinct balance. 

So, for some databases, the result of query 1 and query 2 will be same.

 Now, let us consider a fact that all the entries in the database have the same value for balance. 
 Ideally, all the customers should have rank 1, but both the queries will give all the customers a rank equal to the number of customers in the database.
 So, both the queries do not give us the required output.

 Thus, C is the correct choice.



 19)

 In an inventory management system implemented at a trading corporation, 
 there are several tables designed to hold all the information. 
 Amongst these, the following two tables hold information on which items are supplied by which suppliers, 
 and which warehouse keeps which items along with the stock-level of these items.

Supply = (supplierid, itemcode)
Inventory = (itemcode, warehouse, stocklevel)

For a specific information required by the management, following SQL query has been written

Select distinct STMP.supplierid
From Supply as STMP
Where not unique (Select ITMP.supplierid
                  From Inventory, Supply as ITMP
                  Where STMP.supplierid = ITMP.supplierid
                  And ITMP.itemcode = Inventory.itemcode
                  And Inventory.warehouse = 'Nagpur');

For the warehouse at Nagpur, this query will find all suppliers who
(A) do not supply any item
(B) supply exactly one item
(C) supply one or more items
(D) supply two or more items










Answer: (D)

Explanation: 

Here [not unique] in nested query ensures that only for those suppliers it return True which supplies more than 1 item 
in which case supplier id in inner query will be repeated for that supplier.

Hence, answer is (D) supply two or more items.





20)In SQL, relations can contain null values, and comparisons with null values are treated as unknown. 

Suppose all comparisons with a null value are treated as false. 
Which of the following pairs is not equivalent? 

(a) x = 5, not (not (x = 5)
(b) x = 5, x > 4 and x < 6, where x is an integer
(c) x < 5, not(x = 5)
(d) None of the above










Answer (c)

Explanation:
It doesn’t need much explanation. For all values smaller than 5, x < 5 will always be true but x = 5 will be false.

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/18th%2BJune%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/18th+June+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
