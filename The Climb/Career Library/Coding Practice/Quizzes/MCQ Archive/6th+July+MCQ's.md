---
kind: "study-reference"
title: "6th+July+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/6th+July+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 6th+July+MCQ's

[[The Climb/Career Library/Career Library]]

1) What does the following program do when the input is unsigned 16-bit integer?

#include <stdio.h>
int main( )
{
unsigned int num;
int i;
scanf ("%u", &num);
for ( i = 0; i<16; i++)
{
printf (“%d”, (num << i & 1 << 15 ) ? 1:0);
}
return 1;
}

(A) It prints all even bits from num
(B) It prints all odd bits from num
(C) It prints binary equivalent of num
(D) None of the above













Answer: (C)

2) Write the output of the following C program

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

So, option (D) is correct

3) The following three ‘C’ language statements is equivalent to which single statement?
y=y+1;
z=x+y;
x=x+1
(A) z = x + y + 2;
(B) z = (x++) + (++y);
(C) z = (x++) + (y++);
(D) z = (x++) + (++y) + 1;










Answer: (B)

Explanation: In ‘C’ language, there are two type of increment operators:

post increment:
b = a++;
b = a;
a = a + 1.
pre increment:
b = ++a;
a = a + 1
b = a;

y=y+1; //++y
z=x+y; //z = x + (++y)
x=x+1  //z = (x++) + (++y)

So, option (B) is correct.





4) Output of following C program?

#include<stdio.h> 
int main() 
{ 
    int i = 0; 
    for (printf("1st\n"); i < 2 && printf("2nd\n"); ++i && printf("3rd\n")) 
    { 
        printf("*\n"); 
    } 
    return 0; 
} 

(A) 1st
2nd
*
3rd
2nd
*

(B) 1st
2nd
*
3rd
2nd
*
3rd

(C) 1st
2nd
3rd
*
2nd
3rd

(D) 1st
2nd
3rd
*
1st
2nd
3rd




Answer: (B)

Explanation: It is just one by one execution of statements in for loop.
The initial statement is executed only once.
The second condition is printed before ‘*’ is printed. 
The second statement also has short circuiting logical && operator which
prints the second part only if ‘i’ is smaller than 2
The third statement is printed after ‘*’ is printed. 
This also has short circuiting logical && operator which prints the second 
part only if ‘++i’ is not zero.

5) Predict the output of the below program:

#include <stdio.h> 
int main() 
{ 
    int i = 3; 
    switch(i) 
    { 
        printf("Outside "); 
        case 1: printf("Hello"); 
            break; 
        case 2: printf("World"); 
            break; 
        defau1t: printf("Welcome"); 
    } 
    return 0; 
} 

(A) Outside Welcome
(B) HelloWorld
(C) Nothing gets printed
(D) None of these




Answer: (C)

Explanation: 

In a switch block, the control directly flows within the case labels(or dafault label). 
So, statements which do not fall within these labels, Outside is not printed. 
Please take a closer look at the default label. 
Its defau1t, not default which s interpreted by the compiler as a label used for goto statements. 
Hence, nothing is printed in the above program.

6) Predict the output of the following program:

#include <stdio.h> 
int main() 
{ 
    const int check = 20;
    const int  arr[] = {10, 20, 30}; 
    switch (check) 
    { 
        case arr[0]: printf("Hello "); 
       case arr[1]: printf("World "); 
       case arr[2]: printf("Welcome "); 
    } 
    return 0; 
} 

(A) Hello
(B) World Welcome
(C) Welcome
(D) Compile-time error




Answer: (D)

Explanation: 

The case labels must be constant inside switch block. 
Thats why the compile-time error: case label does not reduce to an integer constant is flashed.

7) Consider the following Employee table

ID   salary   DeptName
1    10000      EC
2    40000      EC
3    30000      CS
4    40000      ME
5    50000      ME
6    60000      ME 
7    70000      CS 

How many rows are there in the result of following query?

SELECT E.ID
FROM  Employee E
WHERE  EXISTS  (SELECT E2.salary
               FROM Employee E2
               WHERE E2.DeptName = 'CS'
               AND   E.salary > E2.salary)

(A) 0
(B) 4
(C) 5
(D) 6


Answer: (C)

Explanation: Background:

    WHERE EXISTS tests for the existence of any records in a subquery.
    EXISTS returns true if the subquery returns one or more records.
    EXISTS is commonly used with correlated subqueries.

Here in the above question, there is a correlated subquery because the subquery 
references the enclosing query (relation Employee renamed as E)
The subquery (SELECT E2.salary FROM Employee E2
WHERE E2.DeptName = ‘CS’)
Filters out E2 relation as (all tuples where DeptName is CS and the respective salaries)

Now the correlated query works as follows:
SELECT E.ID
FROM Employee E
WHERE EXISTS (SELECT E2.salary FROM Employee E2
WHERE E2.DeptName = ‘CS’
AND E.salary > E2.salary)

It takes one tuple from the Employee Relation and displays its ID if the WHERE 
EXISTS returns true i.e. the subquery returns one or more records. 
This happens in the case when the tuple from the Employee Relation E has the 
value of the salary attribute greater than any one of the values of the salary 
attribute filtered out above.
So tuples filtered out would be all the tuples that have their salary attribute 
value greater than the salary values of at least one from the E2 relation (30000 and 70000).

ID salary DeptName
2 40000 EC
4 40000 ME
5 50000 ME
6 60000 ME
7 70000 CS

Finally it displays their ID’s and the output would be:
2
4
5
6
7

Hence option (C) 5 rows.

8) Consider the followng relations : 

Students 
Roll No   Student Name
   1		  Raj
   2		  Rohit
   3		  Raj

 (Roll No is Primary Key) 

 Performance
 Roll No	Course  Marks
    1		  Math	  80
    1     English 70
    2		  Math		75
    3		  English	80
    2		  Physics 65
    3		  Math	  80

Here in Performance table Roll No is a foreign key and Course is a Primary Key

SELECT S.Student_Name, sum(P.Marks)
     FROM Student S, Performance P
     WHERE S.Roll_No = P.Roll_No
     GROUP BY S.Student_Name 

The number of rows that will be returned by the SQL query is _________
(A) 0
(B) 1
(C) 2
(D) 3


Answer: (C)

Explanation: Below is result of given query. Note that there are only two 
student names and query prints sum(P.Marks) for every student.

  Student_Name     Marks
      Raj			    310
     Rohit			  140     

9)
A company maintains records of sales made by its salespersons and pays them 
commission based on each individual’s total sales made in a year. 
This data is maintained in a table with following schema:
salesinfo = (salespersonid, totalsales, commission)
In a certain year, due to better business results, the company decides to 
further reward its salespersons by enhancing the commission paid to them as per
the following formula:
If commission < = 50000, enhance it by 2%
If 50000 < commission < = 100000, enhance it by 4%
If commission > 100000, enhance it by 6%
The IT staff has written three different SQL scripts to calculate enhancement 
for each slab, each of these scripts is to run as a separate transaction as follows:
  
 T1 	

Update salesinfo
Set commission = commission * 1.02
Where commission < = 50000;

 
 T2 	

Update salesinfo
Set commission = commission * 1.04
Where commission > 50000 and commission is < = 100000;

 
 T3 	

Update salesinfo
Set commission = commission * 1.06
Where commission > 100000;

 

Which of the following options of running these transactions will update the 
commission of all salespersons correctly
(A) Execute T1 followed by T2 followed by T3
(B) Execute T2, followed by T3; T1 running concurrently throughout
(C) Execute T3 followed by T2; T1 running concurrently throughout
(D) Execute T3 followed by T2 followed by T1




Answer: (D)

Explanation: T3 followed by T2 followed by T1 

If this sequence is not followed then it may happen that Officer of one slab 
get benefited twice.

Say an officer is having commission as 99,999,He must be get updated commision 
according to T2. But then 99,999*1.04=1,03998 and he again becomes eligible for
next slab of commision.

T3 followed by T2 followed by T1 will be check all border cases like above.

10) In ……………….. inheritance, the base classes are constructed in the order in 
which they appear in the declaration of the derived class.

A) multipath
B) multiple
C) multilevel
D) hierarchical




Ans- B

11) What will be the output of following code ?

#include <iostream>
using namespace std;

class Animal
{
  public :
  int legs = 4;
};

class Dog : Animal
{
  public:
  int tail = 1;
};

int main()
{
  Dog d;
  cout << d.legs;
  cout << d.tail;
}


A. error 	
B. 44
C. 40
D. 41



Ans- A

12) What will be the output of following code?

#include <iostream>
using namespace std;

class Base
{
  public:
  Base() { cout << "Base"; }
};

class Derived : public Base
{
  public:
  Derived(int i) { cout << i; }
};

int main()
{
  Derived d2(10);
  return 0;
}


A. Base10 	
B. 10
C. 10Base 
D. error




Answer : OPTION A

13) What will be the output of following code?

#include <iostream>
using namespace std;

class A
{
  int x;
};

class B : public A
{
  public:
  void show()
  {
    x=10;
    cout << x;
  }
};

int main()
{
  B b;
  b.show();
  return 0;
}

A. 10 	
B. 0
C. error 
D. garbage value



Answer : C

14) Given the proper import statement(s), and

13. PriorityQueue<String> pq = new PriorityQueue<String>();
14. pq.add("2");
15. pq.add("4");
16. System.out.print(pq.peek() + " ");
17. pq.offer("1");
18. pq.add("3");
19. pq.remove("1");
20. System.out.print(pq.poll() + " ");
21. if(pq.remove("2")) System.out.print(pq.poll() + " ");
22. System.out.println(pq.poll() + " " + pq.peek());

What is the result?
A. 2 2 3 3
B. 2 2 3 4
C. 4 3 3 4
D. 2 2 3 3 3
E. 4 3 3 3 3
F. 2 2 3 3 4
G. Compilation fails
H. An exception is thrown at runtime




Answer: B is correct. 
For the sake of the exam, add() and offer() both add to (in this case), n
aturally sorted queues. 
The calls to poll() both return and then remove the first item  from the queue,
so the if test fails.

15)
Given:
3. import java.util.*;
4. public class Mixup {
5. public static void main(String[] args) {
6. Object o = new Object();
7. // insert code here
8. s.add("o");
9. s.add(o);
10. }
11. }

And these three fragments:

I. Set s = new HashSet();
II. TreeSet s = new TreeSet();
III. LinkedHashSet s = new LinkedHashSet();

When fragments I, II, or III are inserted, independently, at line 7, which are true?
(Choose all that apply.)
A. Fragment I compiles
B. Fragment II compiles
C. Fragment III compiles
D. Fragment I executes without exception
E. Fragment II executes without exception
F. Fragment III executes without exception




Answer:
 A, B, C, D, and F are all correct.
Only E is incorrect. Elements of a TreeSet must in some way implement Comparable.

16) Given:

public abstract class AbstractTest {
public int getNum() {
return 45;
}
public abstract class Bar {
public int getNum() {
return 38;
}
}
public static void main(String[] args) {
AbstractTest t = new AbstractTest() {
public int getNum() {
return 22;
}
};
AbstractTest.Bar f = t.new Bar() {
public int getNum() {
return 57;
}
};
System.out.println(f.getNum() + " " + t.getNum());
} }
What is the result?
A. 57 22
B. 45 38
C. 45 57
D. An exception occurs at runtime
E. Compilation fails



Answer: A. 

Explanation 

You can define an inner class as abstract, which means you can instantiate only
concrete subclasses of the abstract inner class. 
The object referenced by the variable t is an instance of an anonymous subclass
of AbstractTest, and the anonymous class overrides the getNum() method to return 22. 
The variable referenced by f is an instance of an anonymous subclass of Bar, and
the anonymous Bar subclass also overrides the getNum() method (to return 57). 
Remember that to create a Bar instance, we need an instance of the enclosing 
AbstractTest class to tie to the new Bar inner class instance.
AbstractTest can't be instantiated because it's abstract, 
so we created an anonymous subclass (non-abstract) and then used the instance of
that anonymous subclass to tie to the new Bar subclass instance.

B, C, D, and E are incorrect based on the program logic described above.

17) Given:

3. public class Tour {
4. public static void main(String[] args) {
5. Cathedral c = new Cathedral();
6. // insert code here
7. s.go();
8. }
9. }
10. class Cathedral {
11. class Sanctum {
12. void go() { System.out.println("spooky"); }
13. }
14. }

Which, inserted independently at line 6, compile and produce the output "spooky"? (Choose all that apply.)

A. Sanctum s = c.new Sanctum();
B. c.Sanctum s = c.new Sanctum();
C. c.Sanctum s = Cathedral.new Sanctum();
D. Cathedral.Sanctum s = c.new Sanctum();
E. Cathedral.Sanctum s = Cathedral.new Sanctum();




Answer:
D is correct. It is the only code that uses the correct inner class instantiation syntax.

18)Given:
1. public class WaitTest {
2. public static void main(String [] args) {
3. System.out.print("1 ");
4. synchronized(args){
5. System.out.print("2 ");
6. try {
7. args.wait();
8. }
9. catch(InterruptedException e){}
10. }
11. System.out.print("3 ");
12. } }

What is the result of trying to compile and run this program?

A. It fails to compile because the IllegalMonitorStateException of wait() is not dealt
with in line 7
B. 1 2 3
C. 1 3
D. 1 2
E. At runtime, it throws an IllegalMonitorStateException when trying to wait
F. It will fail to compile because it has to be synchronized on the this object

Answer:

D is correct. 
1 and 2 will be printed, but there will be no return from the wait call because 
no other thread will notify the main thread, so 3 will never be printed. It's frozen at line 7.

A is incorrect; IllegalMonitorStateException is an unchecked exception. 
B and C are incorrect; 3 will never be printed, since this program will wait forever. 
E is incorrect because IllegalMonitorStateException will never be thrown because the 
wait() is done on args within a block of code synchronized on args. 
F is incorrect because any object can be used to synchronize on and this and static don't mix. 

19) Assume the following method is properly synchronized and called from a 
thread A on an object B:

wait(2000);

After calling this method, when will the thread A become a candidate to get another turn at the CPU?

A. After object B is notified, or after two seconds
B. After the lock on B is released, or after two seconds
C. Two seconds after object B is notified
D. Two seconds after lock B is released

Answer:
A is correct. Either of the two events will make the thread a candidate for running again.

B is incorrect because a waiting thread will not return to runnable when the lock is 
released, unless a notification occurs. 
C is incorrect because the thread will become a candidate immediately after notification. 
D is also incorrect because a thread will not come out of a waiting pool just because a
lock has been released. (Objective 4.4)

20) Which are true? (Choose all that apply.)

A. The notifyAll() method must be called from a synchronized context
B. To call wait(), an object must own the lock on the thread
C. The notify() method is defined in class java.lang.Thread
D. When a thread is waiting as a result of wait(), it releases its lock
E. The notify() method causes a thread to immediately release its lock
F. The difference between notify() and notifyAll() is that notifyAll() notifies 
all waiting threads, regardless of the object they're waiting on

Answer:

A is correct because notifyAll() (and wait() and notify()) must be called from 
within a synchronized context. D is a correct statement.
B is incorrect because to call wait(), the thread must own the lock on the object 
that wait() is being invoked on, not the other way around. 
C is wrong because notify() is defined in java.lang.Object. 
E is wrong because notify() will not cause a thread to release its locks.  
The thread can only release its locks by exiting the synchronized code. 
F is wrong because notifyAll() notifies all the threads waiting on a particular 
locked object, not all threads waiting on any object. 

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/6th%2BJuly%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/6th+July+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
