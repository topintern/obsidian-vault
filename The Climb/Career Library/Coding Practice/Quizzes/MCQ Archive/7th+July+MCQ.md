---
kind: "study-reference"
title: "7th+July+MCQ"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/7th+July+MCQ.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 7th+July+MCQ

[[The Climb/Career Library/Career Library]]

1) How long will the for loop get executed ?

#include<stdio.h>
int main() {
	int i;
	for(;scanf("%d",&i);printf("%d\n",i));

}

A) The for loop would not get executed at all.
B) The for loop would get executed only once.
C) The for loop would get executed 5 times
D) The for loop would get executed infinite times 

















Ans - D

2)Which of the following is the correct output for the C program given below ?

#include<stdio.h>
int main() 
{
   extern int i;
   i=20;
   printf(" %lu ", sizeof(i));
   return 0;
}

A) 2
B) 4
C) Would vary from compiler to compiler
D) Compilation fails 





Ans- D

3) Output of the following c code 

#include<stdio.h>
int main() {
  char *cptr, c;
  void *vptr,v;
  c=10,v=0;
  cptr=&c;
  vptr=&v;
  printf(" %d %d ", *cptr,*vptr);
  return 0;
}


A) 10 0
B) Compilation fails
C) Segementation fault
D) GarbageValue GarbageValue




Ans- B

4)If size of an integer is 4 bytes what will be the output of the following program ?

#include<stdio.h>
int main() {
	int arr[]={11,12,13,14,15};
	printf(" %d %d %d ", sizeof(arr),sizeof(*arr),sizeof(arr[0]));
	return 0;
}

A) 4 4 4 
B) 20 20 4
C) 20 4 4 
D) 4 4 20




Ans- C

5) what would be the equivalent pointer expression for referrring the array element a[i][j][k][l];

A) *(*(*(*(a+i)+j)+k)+l)
B) ***a
C) *a[i][j][k][l]
D)  *(*(*(a+i)+j)+k)+l)




Ans- A

6) Which of the following is the correct output for the program given below ?

#include<stdio.h>
int main() {
int arr[3] = {2,3,4};
char *p;
p=(char *)arr;
printf(" %d ",*p);
p=p+1;
printf(" %d ", *p);
return 0;
}

A) 2 3
B) 2 0
C) 1 0
D) Garbage Values




Ans - B

7) output of the Below CPP Code 

#include<iostream>
using namespace std;

int main() {

char *str1 = "My Cat Pat ";
char *str2= str1;
cout<<endl<<str1<<endl<<str2;

*str1='B';
cout<<endl<<str1<<endl<<str2;

*str2='P';
cout<<endl<<str1<<endl<<str2;
return 0;
}

A)  My Cat Pat 
     My Cat Pat
     By Cat Pat
     My Cat Pat
     By Cat Pat
     Py Cat Pat

B)   My Cat Pat 
     My Cat Pat
     My Cat Pat
     My Cat Pat
     My Cat Pat
     My Cat Pat

C)   My Cat Pat 
     My Cat Pat
     By Cat Pat
     By Cat Pat
     Py Cat Pat
     Py Cat Pat

D) Compilation fails

E) Segementaion fault 




Ans- E

Here we are attempting to change the constant string first through str1 and
second through str2 both result in a run time error, 
as we are trying to change a string which is constant 

8)  output of the Below CPP Code 

#include<iostream>
using namespace std;

int main() {

int str1(43);
cout<<endl<<str1;
return 0;
}

A) 43
B) Compilation fails
C) Segmentation fault
D) None of these





Ans - A



9) output of the Below CPP Code 

#include<iostream>
using namespace std;

int main() {
       bool b = 32;
       int i = false;
       cout<<endl<<b<<endl<<i;

       int j = b+b;
       bool k = b+b;
       cout<<endl<<j<<endl<<k<<endl;
       return 0;
}

A) 32 
      0
      64
      1
 
 B) 1
    0
    1
    0


C) 1
     0
     2
     1

D) Compilation Fails 
  




Ans- C

10)  output of the Below CPP Code 

#include<iostream>
using namespace std;

int main()
{
char *p="what a day";
char *q=p;
cout<<p<<endl<<q;
q="its a good day";
cout<<p<<endl<<q;
return 0;
}

A)
what a day 
what a day
its a good day
its a good day

B)
what a day
what a day
what a day
its a good day

C)
compilation fails

D)
segementation fault





Ans- B

11) output of the below CPP Code 

#include<iostream>
using namespace std;

int i =20;
int main() {
int i = 5;
cout<<i<<endl<<::i<<endl;
{
int i=10;
cout<<i<<endl<<::i;
}
return 0;
}

A) 5 
     20
     10
     20

B) 5
    20
    10
    5

C) compilation error

D) 5 
     10
     10
     20

Ans-A

12) output of the below cpp code 

#include<iostream>
using namespace std;

const int i =10;

int main() {
const int i =20;
cout<<i<<" "<<::i<<" ";

cout<<&i<<" "<<&::i<<" ";
cout<<"end of main";
return 0;
}


A) 20 10 20 10 end of main
B) Compilation fails
C) Segmentation fault
D) None of these
E) 20 10 followed by junk values followed by  end of main


Ans- E

13) Given:

3. import java.util.*;
4. class Turtle {
5. int size;
6. public Turtle(int s) { size = s; }
7. public boolean equals(Object o) { return (this.size == ((Turtle)o).size); }
8. // insert code here
9. }
10. public class TurtleTest {
11. public static void main(String[] args) {
12. LinkedHashSet<Turtle> t = new LinkedHashSet<Turtle>();
13. t.add(new Turtle(1)); t.add(new Turtle(2)); t.add(new Turtle(1));
14. System.out.println(t.size());
15. }
16. }


And these two fragments:
I. public int hashCode() { return size/5; }
II. // no hashCode method declared

If fragment I or II is inserted, independently, at line 8, which are true? (Choose all that apply.)

A. If fragment I is inserted, the output is 2
B. If fragment I is inserted, the output is 3
C. If fragment II is inserted, the output is 2
D. If fragment II is inserted, the output is 3
E. If fragment I is inserted, compilation fails
F. If fragment II is inserted, compilation fails

Answer:

A and D are correct. 
While fragment II wouldn’t fulfill the hashCode() contract (as you can see by
the results), it is legal Java. 
For the purpose of the exam, if you don’t override hashCode(), every object
will have a unique hashcode.

14) Given the proper import statement(s), and:

13. TreeSet<String> s = new TreeSet<String>();
14. TreeSet<String> subs = new TreeSet<String>();
15. s.add("a"); s.add("b"); s.add("c"); s.add("d"); s.add("e");
16.
17. subs = (TreeSet)s.subSet("b", true, "d", true);
18. s.add("g");
19. s.pollFirst();
20. s.pollFirst();
21. s.add("c2");
22. System.out.println(s.size() +" "+ subs.size());

Which are true? (Choose all that apply.)

A. The size of s is 4
B. The size of s is 5
C. The size of s is 7
D. The size of subs is 1
E. The size of subs is 2
F. The size of subs is 3
G. The size of subs is 4
H. An exception is thrown at runtime

Answer:
B and F are correct. 

After "g" is added, TreeSet s contains six elements and TreeSet subs contains 
three (b, c, d), because "g" is out of the range of subs. 
The first pollFirst() finds and removes only the "a".
The second pollFirst() finds and removes the "b" from both TreeSets (remember they are backed).
The final add() is in range of both TreeSets.
The final contents are [c,c2,d,e,g] and [c,c2,d].
 
15) Given:

5. class A { void m() { System.out.println("outer"); } }
6.
7. public class TestInners {
8. public static void main(String[] args) {
9. new TestInners().go();
10. }
11. void go() {
12. new A().m();
13. class A { void m() { System.out.println("inner"); } }
14. }
15. class A { void m() { System.out.println("middle"); } }
16. }
What is the result?
A. inner
B. outer
C. middle
D. Compilation fails
E. An exception is thrown at runtime


Answer:
C is correct. 
The "inner" version of class A isn't used because its declaration comes after 
the instance of class A is created in the go() method.

16) Given:
3. public class Car {
4. class Engine {
5. // insert code here
6. }
7. public static void main(String[] args) {
8. new Car().go();
9. }
10. void go() {
11. new Engine();
12. }
13. void drive() { System.out.println("hi"); }
14. }

Which, inserted independently at line 5, produce the output "hi"? (Choose all that apply.)
A. { Car.drive(); }
B. { this.drive(); }
C. { Car.this.drive(); }
D. { this.Car.this.drive(); }
E. Engine() { Car.drive(); }
F. Engine() { this.drive(); }
G. Engine() { Car.this.drive(); }

Answer:
C and G are correct. 

C is the correct syntax to access an inner class’s outer instance method
from an initialization block, and G is the correct syntax to access it from a constructor.

17) Given:
3. public class City {
4. class Manhattan {
5. void doStuff() throws Exception { System.out.print("x "); }
6. }
7. class TimesSquare extends Manhattan {
8. void doStuff() throws Exception { }
9. }
10. public static void main(String[] args) throws Exception {
11. new City().go();
12. }
13. void go() throws Exception { new TimesSquare().doStuff(); }
14. }

What is the result?
A. x
B. x x
C. No output is produced
D. Compilation fails due to multiple errors
E. Compilation fails due only to an error on line 4
F. Compilation fails due only to an error on line 7
G. Compilation fails due only to an error on line 10
H. Compilation fails due only to an error on line 13



Answer:
C is correct. 

The inner classes are valid, and all the methods (including main()), 
correctly throw an Exception, given that doStuff() throws an Exception. 
The doStuff() in class TimesSquare overrides class Manhattan's doStuff() 
and produces no output.

18) Given:

3. public class Navel {
4. private int size = 7;
5. private static int length = 3;
6. public static void main(String[] args) {
7. new Navel().go();
8. }
9. void go() {
10. int size = 5;
11. System.out.println(new Gazer().adder());
12. }
13. class Gazer {
14. int adder() { return size * length; }
15. }
16. }

What is the result?
A. 15
B. 21
C. An exception is thrown at runtime
D. Compilation fails due to multiple errors
E. Compilation fails due only to an error on line 4
F. Compilation fails due only to an error on line 5



Answer:
B is correct. 

The inner class Gazer has access to Navel's private static and private instance variables.

19) Given the scenario: This class is intended to allow users to write a series
of messages, so that each message is identified with a timestamp and the name 
of the thread that wrote the message:

public class Logger {
private StringBuilder contents = new StringBuilder();
public void log(String message) {
contents.append(System.currentTimeMillis());
contents.append(": ");
contents.append(Thread.currentThread().getName());
contents.append(message);
contents.append("\n");
}
public String getContents() { return contents.toString(); }
}

How can we ensure that instances of this class can be safely used by multiple threads?
A. This class is already thread-safe
B. Replacing StringBuilder with StringBuffer will make this class thread-safe
C. Synchronize the log() method only
D. Synchronize the getContents() method only
E. Synchronize both log() and getContents()
F. This class cannot be made thread-safe

Answer:
E is correct. Synchronizing the public methods is sufficient to make this safe,
so F is false.
This class is not thread-safe unless some sort of synchronization protects the
changing data.

B is not correct because although a StringBuffer is synchonized internally, 
we call append() multiple times, and nothing would prevent two simultaneous 
log() calls from mixing up their messages. 
C and D are not correct because if one method remains unsynchronized,
it can run while the other is executing, which could result in reading the 
contents while one of the messages is incomplete, or worse. 
(You don't want to call getString() on the StringBuffer as it's resizing its
internal character array.)

20) Given:

public static synchronized void main(String[] args) throws
InterruptedException {
Thread t = new Thread();
t.start();
System.out.print("X");
t.wait(10000);
System.out.print("Y");
}
What is the result of this code?
A. It prints X and exits
B. It prints X and never exits
C. It prints XY and exits almost immeditately
D. It prints XY with a 10-second delay between X and Y
E. It prints XY with a 10000-second delay between X and Y
F. The code does not compile
G. An exception is thrown at runtime

Answer:
G is correct. 

The code does not acquire a lock on t before calling t.wait(), so it throws
an IllegalMonitorStateException.
The method is synchronized, but it's not synchronized on t so the exception will be thrown.
If the wait were placed inside a synchronized(t) block, then the answer would have been D.

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/7th%2BJuly%2BMCQ.txt) · CODING RESOURCES/Quiz Mcqs/7th+July+MCQ.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
