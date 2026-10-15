---
kind: "study-reference"
title: "30th+June+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/30th+June+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 30th+June+MCQ's

[[The Climb/Career Library/Career Library]]


1)  Output of the following in C Language

Suppose a, b, c and d are int variables. For ternary operator in C ( ? : ), pick the best statement.

(A) a>b ? : ; is valid statement i.e. 2nd and 3rd operands can be empty and they
are implicitly replaced with non-zero value at run-time.

(B) a>b ? c=10 : d=10; is valid statement. Based on the value of a and b, 
either c or d gets assigned the value of 10.

(C) a>b ? (c=10,d=20) : (c=20,d=10); is valid statement. Based on the value of 
a and b, either c=10,d=20 gets executed or c=20,d=10 gets executed.

(D) All of these are valid statements for ternary operator.























Answer: (C)

Explanation: 

For ternary operator, both 2nd and 3rd operands are necessary. 
So A) isn’t correct. 
As per operator precedence, ternary operator has higher precedence over assignment operator.
So B) isn’t correct. 




2) Output of the following C Code


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
Here, even though life of static variables span across function calls but their scope is respective to their function body only. 
That’s why staticVar of each function has separate copies whose life span across function calls. 
And d is correct.




3) Which of the following is correct with respect to "Jump Statements" in C?

(A) goto
(B) continue
(C) break
(D) return
(E) All of these










Answer: (E)


Explanation: 

As per C standard, "A jump statement causes an unconditional jump to another place". 
So if we see carefully, all "goto", "continue", "break" and "return" makes the program control jump unconditionally from one place to another. 
That’s why correct answer is E. 




4)
What’s going to happen when we compile and run the following C program?

#include<stdio.h>
  
int main() 
{ 
  int i = 1, j; 
  for ( ; ; ) 
  {  
    if (i) 
        j = --i; 
    if (j < 10) 
       printf("helloWorld", j++); 
    else
       break; 
  } 
  return 0; 
} 

(A) Compile Error.
(B) it will run into infinite loop printing helloWorld.
(C) it’ll print helloWorld 10 times.
(D) it’ll print helloWorld 9 times.










Answer: (C)



5)  Suppose that in a C program snippet, followings statements are used.

i) sizeof(int); 
ii) sizeof(int*); 
iii) sizeof(int**); 

Assuming size of pointer is 4 bytes and size of int is also 4 bytes, pick the most correct answer from the given options.

(A) Only i) would compile successfully and it would return size as 4.
(B) i), ii) and iii) would compile successfully and size of each would be same i.e. 4
(C) i), ii) and iii) would compile successfully but the size of each would be different and would be decided at run time.
(D) ii) and iii) would result in compile error but i) would compile and result in size as 4.







Answer: (B)




6)

Consider the following C function:

int f(int n) 
{ 
   static int i = 1; 
   if (n >= 5) 
      return n; 
   n = n+i; 
   i++; 
   return f(n); 
} 

The value returned by f(1) is

(A) 5
(B) 6
(C) 7
(D) 8


Answer: (C)

7) A process executes the following code

for (i = 0; i < n; i++) 
     fork();

The total number of child processes created is
(A) n
(B) 2n - 1
(C) 2n
(D) 2(n+1) - 1









Answer: (B)

Explanation:

         F0       // There will be 1 child process created by first fork
      /     \
    F1      F1    // There will be 2 child processes created by second fork
   /  \    /  \
 F2   F2  F2   F2  // There will be 4 child processes created by third fork
/ \   / \ / \  / \
 ...............   // and so on

If we sum all levels of above tree for i = 0 to n-1, we get 2n - 1. 
So there will be 2n – 1 child processes. 
On the other hand, the total number of process created are (number of child processes)+1.

8) Virtual memory is

(A) Large secondary memory
(B) Large main memory
(C) Illusion of large main memory
(D) None of the above








Answer: (C)

Explanation: Virtual memory is illusion of large main memory.

9) #include<iostream>
using namespace std;

int main()
{
 cout<<(int i=5) << (int j=6);
}


A) Prints 5 6
B) Compilation fails
C) Segmentation fault
D) None of these




Ans: B

10) What will be the output of the following C++ code?

#include <iostream>
using namespace std;

class sample
{
    public:
    virtual void example() = 0; 
};

class Ex1:public sample
{
    public:
    void example()
    {
	cout << "hello ";
    }
};

class Ex2:public sample
{
    public:
    void example()
    {
	cout << "world";
    }
};

int main()
{
    sample* arra[2];
    Ex1 e1;
    Ex2 e2;
    arra[0]=&e1;
    arra[1]=&e2;
    arra[0]->example();
    arra[1]->example();
}

a) hello
b) world
c) hello world
d) Compilation fails






Answer: c

Explanation: 

In this program, We are combining the two statements from two classes and
printing it by using abstract class.

11) What will be the order of execution of base class constructors in the following method of inheritance?

class A: public B, virtual public C {….};

A) B(); C(); A();
B) C(); B(); A();
C) A(); B(); C();
D) B(); A(); C();





Ans-  B) 




12) What will be the output of the following C++ code?

        #include <iostream>
        using namespace std;

        class stu
        {
            protected:
            int rno;
            public:
            void get_no(int a)
            {
                rno = a;
            }
            void put_no(void)
            {
            }
        };

        class test:public stu
        {
            protected:
            float part1,part2;
            public:
            void get_mark(float x, float y)
            {
                part1 = x;
                part2 = y;
            }
            void put_marks()
            {
            }
        };

        class sports
        {
            protected:
            float score;
            public:
            void getscore(float s)
            {
                score = s;
            }
            void putscore(void)
            {
            }
        };

        class result: public test, public sports
        {
            float total;
            public:
            void display(void);
        };
        void result::display(void)
        {
            total = part1 + part2 + score;
            put_no();
            put_marks();
            putscore();
            cout << "Total Score=" << total << "\n";
        }

        int main()
        {
            result stu;
            stu.get_no(123);
            stu.get_mark(27.5, 33.0);
            stu.getscore(6.0);
            stu.display();
            return 0;
        }


a) 66.5
b) 64.5
c) 62.5
d) 60.5







Answer: a

13) What will be the output of the following C++ code?

#include <iostream>
using namespace std;

class Base
{
   public:
    virtual void print() const = 0;
};

class DerivedOne : virtual public Base
{
    public:
    void print() const
    {
	cout << "1";
    }
};

class DerivedTwo : virtual public Base
{
    public:
    void print() const
    {
	cout << "2";
    }
};

class Multiple : public DerivedOne, DerivedTwo
{
    public:
    void print() const
    {
	DerivedTwo::print();
    }
};

int main()
{
    Multiple both;
    DerivedOne one;
    DerivedTwo two;
    Base *array[ 3 ];
    array[ 0 ] = &both;
    array[ 1 ] = &one;
    array[ 2 ] = &two;
    for ( int i = 0; i < 3; i++ )
    array[ i ] -> print();
    return 0;
}


a) 121
b) 212
c) 12
d) 215





Answer: b




14) output of the following CPP Code

#include<iostream>
using namespace std;
class signal1
{
    public:
      int a:20;
      int b:10;
};
int main()
{
    signal1 s = {5,7};
    cout<<s.a<<" "<<s.b;
}

A) compilation fails
B) Segmentation fault
C) prints 5 7
D) prints 5 followed by garbage value
E) prints 5 followed by 5




Ans- C


15)Given:

import java.util.*;
class MapEQ {
public static void main(String[] args) {
Map<ToDos, String> m = new HashMap<ToDos, String>();
ToDos t1 = new ToDos("Monday");
ToDos t2 = new ToDos("Monday");
ToDos t3 = new ToDos("Tuesday");
m.put(t1, "doLaundry");
m.put(t2, "payBills");
m.put(t3, "cleanAttic");
System.out.println(m.size());
} }
class ToDos{
String day;
ToDos(String d) { day = d; }
public boolean equals(Object o) {
return ((ToDos)o).day == this.day;
}
// public int hashCode() { return 9; }
}

Which is correct? (Choose all that apply.)

A. As the code stands it will not compile
B. As the code stands the output will be 2
C. As the code stands the output will be 3
D. If the hashCode() method is uncommented the output will be 2
E. If the hashCode() method is uncommented the output will be 3
F. If the hashCode() method is uncommented the code will not compile

Answer:

C and D are correct. 

If hashCode() is not overridden then every entry will go into its own bucket, and the overridden equals() method will have no effect on determining equivalency.
If hashCode() is overridden, then the overridden equals() method will view t1 and t2 as duplicates.

16) Given:

12. public class AccountManager {
13. private Map accountTotals = new HashMap();
14. private int retirementFund;
15.
16. public int getBalance(String accountName) {
17. Integer total = (Integer) accountTotals.get(accountName);
18. if (total == null)
19. total = Integer.valueOf(0);
20. return total.intValue();
21. }
23. public void setBalance(String accountName, int amount) {
24. accountTotals.put(accountName, Integer.valueOf(amount));
25. } }

This class is to be updated to make use of appropriate generic types, with no changes in behavior (for better or worse). 

Which of these steps could be performed? (Choose three.)

A. Replace line 13 with
	private Map<String, int> accountTotals = new HashMap<String, int>();

B. Replace line 13 with
	private Map<String, Integer> accountTotals = new HashMap<String, Integer>();

C. Replace line 13 with
	private Map<String<Integer>> accountTotals = new HashMap<String<Integer>>();

D. Replace lines 17–20 with
	int total = accountTotals.get(accountName);
	if (total == null) total = 0;
	return total;

E. Replace lines 17–20 with
	Integer total = accountTotals.get(accountName);
	if (total == null) total = 0;
	return total;

F. Replace lines 17–20 with
	return accountTotals.get(accountName);

G. Replace line 24 with
	accountTotals.put(accountName, amount);

H. Replace line 24 with
	accountTotals.put(accountName, amount.intValue());

Answer:

B, E, and G are correct.

A is wrong because you can't use a primitive type as a type parameter. 
C is wrong because a Map takes two type parameters separated by a comma. 
D is wrong because an int can't autobox to a null, and 
F is wrong because a null can't unbox to 0. 
H is wrong because you can't autobox a primitive just by trying to invoke a method with it. 

17) Given:

interface Hungry<E> { void munch(E x); }
interface Carnivore<E extends Animal> extends Hungry<E> {}
interface Herbivore<E extends Plant> extends Hungry<E> {}
abstract class Plant {}
class Grass extends Plant {}
abstract class Animal {}
class Sheep extends Animal implements Herbivore<Sheep> {
public void munch(Sheep x) {}
}
class Wolf extends Animal implements Carnivore<Sheep> {
public void munch(Sheep x) {}
}

Which of the following changes (taken separately) would allow this code to compile?
(Choose all that apply.)

A. Change the Carnivore interface to
	interface Carnivore<E extends Plant> extends Hungry<E> {}

B. Change the Herbivore interface to
	interface Herbivore<E extends Animal> extends Hungry<E> {}

C. Change the Sheep class to
	class Sheep extends Animal implements Herbivore<Plant> {
	public void munch(Grass x) {}
	}

D. Change the Sheep class to
	class Sheep extends Plant implements Carnivore<Wolf> {
	public void munch(Wolf x) {}
	}

E. Change the Wolf class to
	class Wolf extends Animal implements Herbivore<Grass> {
	public void munch(Grass x) {}
	}

F. No changes are necessary

Answer:

B is correct. 
The problem with the original code is that Sheep tries to implement Herbivore<Sheep> and 
Herbivore declares that its type parameter E can be any type that extends Plant. 
Since a Sheep is not a Plant, Herbivore<Sheep> makes no sense—
the type Sheep is outside the allowed range of Herbivore's parameter E. 
Only solutions that either alter the definition of a Sheep or alter the definition of Herbivore will be able to fix this. 
So A, E, and F are eliminated. 
B works, changing the definition of an Herbivore to allow it to eat Sheep solves the problem. 
C doesn't work because an Herbivore<Plant> must have a munch(Plant) method, not munch(Grass). 
And D doesn't work, because in D we made Sheep extend Plant, now the Wolf class breaks because its munch(Sheep) method no longer fulfills the contract of Carnivore. 

18)Which are true about a static nested class? (Choose all that apply.)

A. You must have a reference to an instance of the enclosing class in order to instantiate it
B. It does not have access to non-static members of the enclosing class
C. Its variables and methods must be static
D. If the outer class is named MyOuter, and the nested class is named MyInner, it can be instantiated using new MyOuter.MyInner();
E. It must extend the enclosing class


Answer:

B and D. 

B is correct because a static nested class is not tied to an instance of the  enclosing class, and thus can't access the non-static members of the class 
(just as a static method can't access non-static members of a class). 
D uses the correct syntax for instantiating a static nested class.
A is incorrect because static nested classes do not need (and can't use) a reference to an instance of the enclosing class. 
C is incorrect because static nested classes can declare and define non-static members. 
E is wrong because…it just is. 
There's no rule that says an inner or nested class has to extend anything.

19)Given:
class Boo {
  Boo(String s) { }
  Boo() { }
}

class Bar extends Boo {
  Bar() { }
  Bar(String s) {super(s);}
  void zoo() {
  // insert code here
  }
}

Which create an anonymous inner class from within class Bar? (Choose all that apply.)
A. Boo f = new Boo(24) { };
B. Boo f = new Bar() { };
C. Boo f = new Boo() {String s; };
D. Bar f = new Boo(String s) { };
E. Boo f = new Boo.Bar(String s) { };

Answer:
B and C. 

B is correct because anonymous inner classes are no different from any other class when it comes to polymorphism. 
That means you are always allowed to declare a reference variable of the superclass type and have that reference variable refer to an
instance of a subclass type, which in this case is an anonymous subclass of Bar. 
Since Bar is a subclass of Boo, it all works. 
C uses correct syntax for creating an instance of Boo.
A is incorrect because it passes an int to the Boo constructor, and there is no matching constructor in the Boo class. 
D is incorrect because it violates the rules of polymorphism;
you cannot refer to a superclass type using a reference variable declared as the subclass type. 
The superclass doesn't have everything the subclass has. 
E uses incorrect syntax.



20)
The following block of code creates a Thread using a Runnable target:

Runnable target = new MyRunnable();
Thread myThread = new Thread(target);

Which of the following classes can be used to create the target, so that the preceding code compiles correctly?

A. public class MyRunnable extends Runnable{public void run(){}}
B. public class MyRunnable extends Object{public void run(){}}
C. public class MyRunnable implements Runnable{public void run(){}}
D. public class MyRunnable implements Runnable{void run(){}}
E. public class MyRunnable implements Runnable{public void start(){}}

Answer:

C is correct. The class implements the Runnable interface with a legal run() method.

A is incorrect because interfaces are implemented, not extended. 
B is incorrect because even though the class has a valid public void run() method, it does not implement the Runnable interface. 
D is incorrect because the run() method must be public. 
E is incorrect because the method to implement is run(), not start(). 

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/30th%2BJune%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/30th+June+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
