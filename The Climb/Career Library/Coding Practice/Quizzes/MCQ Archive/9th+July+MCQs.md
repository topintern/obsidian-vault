---
kind: "study-reference"
title: "9th+July+MCQs"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/9th+July+MCQs.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 9th+July+MCQs

[[The Climb/Career Library/Career Library]]

1) Output of the following C Code

#include<stdio.h>

struct emp
{
  char name[20];
  int age;
};

void f(struct emp);

int main(){
struct emp e ={34,"Scott"};
f(e);
return 0;
}

void f(struct emp e)
{
   printf(" %s %d ", e.name,e.age);
}

A) Scott 34
B) 34 Scott
C) Garbage Value followed by 34
D) Garbage value followed by garbage value 




Ans- D 

2) Which of the following set of statements is correct ?

A) typedef long a;
     extern int a c;

B) typedef long a;
    extern a int c;
 
C) typedef long a;
    extern a c;

D) All of these 



Ans - D

3)  #include<stdio.h>
    int main() {
   enum status {pass,fail,atkt};
   enum status stud1,stud2,stud3;
   stud1=pass;
   stud2=atkt;
   stud3=fail;
   printf(" %d %d %d ", stud1, stud2,stud3);
   return 0;
   }

   A) 0 1 2
   B) 1 2 3
   C) 0 2 1
   D) 1 3 2
   E) pass atkt fail



   Ans- C

4)Consider the following code snippet :

   struct data1
   {
    int i;
    float f;
   };

   struct data2
   {
    char name[10];
    double d;
   };

   what is the correct way of declaring a union info which would share space 
   amongst structure data1 and data2 ?


   A) union info 
	{
	 struct data1 x;
	 struct data2 y;
	};

 B) 
    union info 
	{
	 struct data1 x;
	};


C)  union info 
	{
	 struct data2 y;
	};

D) None of these



Ans- A

5)
Which of the following is not a user-defined data type ?


A) struct book 
	{
	   char name [10];
	}

B) long int i = 100;

C) enum day {Sun,Mon,Tue};

D) union stud
     {
      int age;
      char name [20];
     }

 
 Ans- B

 6) #include<iostream>
 using namespace std;

 struct emp{
     char name [20];
     int age;
 };

 union uemp{
     char name [20];
     int age;
 };

int main()
{
    struct emp e = {"Pinky",25};
    union uemp ue;
    ue=e;
    cout<<ue.name<<ue.age;
}


A) Pinky 25
B) Garbage Value followed by Garbage value
C) Segmentation fault/run time error
D) Compilation fails



Ans - D

7)
#include<iostream>
using namespace std;

const int i = 57;

int main() 
{
   const int i = 89;
   cout<<i<<" "<<::i<<endl;
   cout<<&i<<" "<<&::i;
   return 0;
}

A) 89 57 
    address followed by address 

B) GarbageValue GarbageValue
    GarbageValue GarbageValue
    
C) 89 57 
    GarbageValue GarbageValue

D) Compilation fails 



Ans - A

8)
#include<iostream>
using namespace std;

union test 
{
    test()
    {
        cout<<"Test called ";
    }
    ~test() {
        cout<<"Test Des called ";
    }
}t[2];

int main()
{
    
}


A) Compilation fails
B) Segmentation fault
C) Test called Test called Test Des called Test Des called
D) Test called Test Des called Test called Test Des called 
E) Compiles but prints nothing


Ans - C

9)#include<iostream>
using namespace std;

int i = 5;

int main()
{
  int i = 10;
  {
    int i = 20;
    cout<< i <<" "<< ::i << " "<<::(::i);
  }
}

A) 20 10 5
B) 20 10 10
C) 20 5 5 
D) Compilation fails
E) 20 10 followed by run time error 



Ans - D

10)
3. import java.util.*;
4. public class Magellan {
5. public static void main(String[] args) {
6. TreeMap<String, String> myMap = new TreeMap<String, String>();
7. myMap.put("a", "apple"); myMap.put("d", "date");
8. myMap.put("f", "fig"); myMap.put("p", "pear");
9. System.out.println("1st after mango: " + // sop 1
10. myMap.higherKey("f"));
11. System.out.println("1st after mango: " + // sop 2
12. myMap.ceilingKey("f"));
13. System.out.println("1st after mango: " + // sop 3
14. myMap.floorKey("f"));
15. SortedMap<String, String> sub = new TreeMap<String, String>();
16. sub = myMap.tailMap("f");
17. System.out.println("1st after mango: " + // sop 4
18. sub.firstKey());
19. }
20. }
Which of the System.out.println statements will produce the output 1st after mango: p?
(Choose all that apply.)
A. sop 1
B. sop 2
C. sop 3
D. sop 4
E. None; compilation fails
F. None; an exception is thrown at runtime

Answer:
A is correct. 
The ceilingKey() method's argument is inclusive. 
The floorKey() method would be used to find keys before the specified key. 
The firstKey() method's argument is also inclusive.


11)

Given:
3. import java.util.*;
4. class Business { }
5. class Hotel extends Business { }
6. class Inn extends Hotel { }
7. public class Travel {
8. ArrayList<Hotel> go() {
9. // insert code here
10. }
11. }

Which, inserted independently at line 9, will compile? (Choose all that apply.)
A. return new ArrayList<Inn>();
B. return new ArrayList<Hotel>();
C. return new ArrayList<Object>();
D. return new ArrayList<Business>();

Answer:
B is correct.
A is incorrect because polymorphic assignments don't apply to generic type parameters. 
C and D are incorrect because they don't follow basic polymorphism rules. 

12)
3. import java.util.*;
4. public class Pockets {
5. public static void main(String[] args) {
6. String[] sa = {"nickel", "button", "key", "lint"};
7. Sorter s = new Sorter();
8. for(String s2: sa) System.out.print(s2 + " ");
9. Arrays.sort(sa,s);
10. System.out.println();
11. for(String s2: sa) System.out.print(s2 + " ");
12. }
13. class Sorter implements Comparator<String> {
14. public int compare(String a, String b) {
15. return b.compareTo(a);
16. }
17. }
18. }
What is the result?

A. Compilation fails
B. button key lint nickel
    nickel lint key button
C. nickel button key lint
     button key lint nickel
D. nickel button key lint
    nickel button key lint
E. nickel button key lint
    nickel lint key button
F. An exception is thrown at runtime

Answer:
A is correct, the inner class Sorter must be declared static to be called from the static method main(). 
If Sorter had been static, answer E would be correct.

13)
Given:
class MyThread extends Thread {
MyThread() {
System.out.print(" MyThread");
}
public void run() { System.out.print(" bar"); }
public void run(String s) { System.out.print(" baz"); }
}
public class TestThreads {
public static void main (String [] args) {
Thread t = new MyThread() {
public void run() { System.out.print(" foo"); }
};
t.start();
} }
What is the result?
A. foo
B. MyThread foo
C. MyThread bar
D. foo bar
E. foo bar baz
F. bar foo
G. Compilation fails
H. An exception is thrown at runtime

Answer:

B is correct. 
The first line of main we're constructing an instance of an anonymous inner 
class extending from MyThread. 
So the MyThread constructor runs and prints MyThread.
Next, main() invokes start() on the new thread instance, which causes the overridden
run() method (the run() method in the anonymous inner class) to be invoked.

14)Given:
public class ThreadDemo {
synchronized void a() { actBusy(); }
static synchronized void b() { actBusy(); }
static void actBusy() {
try { Thread.sleep(1000); }
catch (InterruptedException e) {}
}
public static void main(String[] args) {
final ThreadDemo x = new ThreadDemo();
final ThreadDemo y = new ThreadDemo();
Runnable runnable = new Runnable() {
public void run() {
int option = (int) (Math.random() * 4);
switch (option) {
case 0: x.a(); break;
case 1: x.b(); break;
case 2: y.a(); break;
case 3: y.b(); break;
} }
};
Thread thread1 = new Thread(runnable);
Thread thread2 = new Thread(runnable);
thread1.start();
thread2.start();
} }
Which of the following pairs of method invocations could NEVER be executing at the same time?
(Choose all that apply.)
A. x.a() in thread1, and x.a() in thread2
B. x.a() in thread1, and x.b() in thread2
C. x.a() in thread1, and y.a() in thread2
D. x.a() in thread1, and y.b() in thread2
E. x.b() in thread1, and x.a() in thread2
F. x.b() in thread1, and x.b() in thread2
G. x.b() in thread1, and y.a() in thread2
H. x.b() in thread1, and y.b() in thread2

Answer:
A, F, and H. 
A is a right answer because when synchronized instance methods are called on the
same instance, they block each other.
F and H can't happen because synchronized static methods in the same class block
each other, regardless of which instance was used to call the methods.
(An instance is not required to call static methods; only the class.)
C could happen because synchronized instance methods called on different 
instances do not block each other. 
B, D, E, and G could all happen because instance methods and static methods 
lock on different objects, and do not block each other.


15)Given:
public class TwoThreads {
static Thread laurel, hardy;
public static void main(String[] args) {
laurel = new Thread() {
public void run() {
System.out.println("A");
try {
hardy.sleep(1000);
} catch (Exception e) {
System.out.println("B");
}
System.out.println("C");
}
};
hardy = new Thread() {
public void run() {
System.out.println("D");
try {
laurel.wait();
} catch (Exception e) {
System.out.println("E");
}
System.out.println("F");
}
};
laurel.start();
hardy.start();
}
}
Which letters will eventually appear somewhere in the output? (Choose all that apply.)
A. A
B. B
C. C
D. D
E. E
F. F
G. The answer cannot be reliably determined
H. The code does not compile

Answer:
A, C, D, E, and F are correct. 

This may look like laurel and hardy are battling to cause the other to sleep() 
or wait()—but that's not the case. 

Since sleep() is a static method, it affects the current thread, which is laurel
(even though the method is invoked using a reference to hardy). 
That's misleading but perfectly legal, and the Thread laurel is able to sleep
with no exception, printing A and C (after at least a 1-second delay). 
Meanwhile hardy tries to call laurel.wait()—but hardy has not synchronized on laurel,
so calling laurel.wait() immediately causes an IllegalMonitorStateException, 
and so hardy prints D, E, and F. 

Although the order of the output is somewhat indeterminate (we have no way of 
knowing whether A is printed before D, for example)
it is guaranteed that A, C, D, E, and F will all be printed in some order, 
eventually—so G is incorrect.


## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/9th%2BJuly%2BMCQs.txt) · CODING RESOURCES/Quiz Mcqs/9th+July+MCQs.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
