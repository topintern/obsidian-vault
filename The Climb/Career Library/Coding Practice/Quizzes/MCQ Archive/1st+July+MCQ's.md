---
kind: "study-reference"
title: "1st+July+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/1st+July+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 1st+July+MCQ's

[[The Climb/Career Library/Career Library]]

1) Choose the correct option to fill the ?1 and ?2 so that the program prints an 
input string in reverse order. 
Assume that the input string is terminated by a new line character.

#include <stdio.h>
void wrt_it (void);
int main (void)
{
    printf("Enter Text"); 
    printf ("\n");
    wrt_ it();
    printf ("\n");
    return 0;
}
void wrt_it (void)
{
    int c;
    if (?1)
        wrt_it();
    ?2
}

(A)	?1 is  getchar() ! = ‘\n’
	?2 is  getchar(c);

(B)	?1 is  (c = getchar()); ! = ‘\n’
	?2 is  getchar(c);

(C)	?1 is  c! = ‘\n’
	?2 is  putchar(c);

(D)	?1 is (c = getchar()) ! = ‘\n’
	?2 is putchar(c);





Answer: (D)

Explanation:
getchar() : This function is used to read a character from the standard input stream.

2) Pick the best statement for the following program snippet:
#include <stdio.h> 
  
int main() 
{ 
 int var;  /*Suppose address of var is 2000 */
  
 void *ptr = &var; 
 *ptr = 5; 
 printf("var=%d and *ptr=%d",var,*ptr); 
               
 return 0; 
} 

(A) It will print “var=5 and *ptr=2000”
(B) It will print “var=5 and *ptr=5”
(C) It will print “var=5 and *ptr=XYZ” where XYZ is some random address
(D) Compile error


Answer: (D)

Explanation: 

Key point in the above snippet is dereferencing of void pointer. 
It should be noted that dereferencing of void pointer isn’t allowed because void is an incomplete data type. 
The correct way to assign value of 5 would be first to typecast void pointer and then use it. 
So instead of *ptr, one should use *(int *)ptr. 
Correct answer is d.

3)Pick the best statement for the below program:

#include<stdio.h>
  
int size = 4; 
int arr[size]; 
  
int main() 
{ 
 if(arr[0]) 
  printf("Initialized to ZERO"); 
 else
  printf("Not initialized to ZERO"); 
  
 return 0; 
} 

(A) No compile error and it’ll print “Initialized to ZERO”.
(B) No compile error and it’ll print “Not initialized to ZERO”.
(C) Compile error because size of arr has been defined using variable outside any function.
(D) No compile error and it’ll print either “Initialized to ZERO” or “Not initialized to ZERO” depending on what value is present at arr[0] at a particular run of the program.

Answer: (C)

Explanation: 

An array whose size is specified as variable can’t be defined out any function. 
It can be defined only inside a function. 
So putting arr[size] outside main() would result in compile error. 
Answer is C.

4)Pick the best statement for the below program:

#include<stdio.h>
   
void fun(int n) 
{ 
   int idx; 
   int arr1[n] = {0}; 
   int arr2[n]; 
   
   for (idx=0; idx<n; idx++) 
       arr2[idx] = 0;     
} 
   
int main() 
{ 
   fun(4); 
   return 0; 
} 

(A) Definition of both arr1 and arr2 is incorrect because variable is used to
specify the size of array. That’s why compile error.
(B) Apart from definition of arr1 arr2, initialization of arr1 is also
incorrect. arr1 can’t be initialized due to its size being specified as
variable. That’s why compile error.
(C) Initialization of arr1 is incorrect. arr1 can’t be initialized due to its
size being specified as variable. That’s why compile error.
(D) No compile error. The program would define and initializes both arrays to
ZERO.




Answer: (C)

Explanation: 

There’s no issue with definition of arr1 and arr2.
In definition of these arrays, the mention of array size using variable is ok as per C standard but these types of arrays can’t be initialized at the time of definition. 
That’s why initialization of arr1 is incorrect. 
But initialization of arr2 is done correctly. Right answer is C.

5) Output of following program under the assumption that numbers are stored in 2’s complement form.

#include<stdio.h> 
int main() 
{ 
   printf("%c\n", ~('C' * -1)); 
   return 0; 
} 

(A) B
(B) A
(C) Compiler Error
(D) C


Answer: (A)

Explanation: executed without any error or warning messages and the output for the above code is
‘B’
The above program processes as below
Step 1:
First (‘C’ *-1) is processed
ASCII value of ‘C’ is 67 and it is multiplied with -1 as
67 * (-1) = -67
Step 2:
The binary representation of -67 is 10111101
The bitwise negation of 10111101 becomes (01000010 ) 2 = (66) 10
Step 3:
66 is the ASCII value of ‘B’
So ~(‘C’*-1) = 66 and so the output of the above the program is B

6) The seven elements A, B, C, D, E, F and G are pushed onto a stack in reverse order, i.e., starting from G. 
The stack is popped five times and each element is inserted into a queue.
Two elements are deleted from the queue and pushed back onto the stack. Now, one element is popped from the stack. 
The popped item is ________.

(A) A
(B) B
(C) F
(D) G


Answer: (B)

7) While inserting the elements 71, 65, 84, 69, 67, 83 in an empty binary search tree (BST) in the sequence shown, the element in the lowest level is

(A) 65
(B) 67
(C) 69
(D) 83


Answer: (B)

8)
#include<iostream>
using namespace std;
 
class base {
  int arr[10];     
};
 
class b1: virtual public base { };
 
class b2: virtual public base { };
 
class derived: public b1, public b2 {};
 
int main(void)
{ 
  cout << sizeof(derived);
  return 0;
} 


(A) 48
(B) 80
(C) 0
(D) 4



Ans- A

virtual base classes are used to save space and avoid ambiguities in such cases. 
the program prints 48. 
8 extra bytes are for bookkeeping information stored by the compiler 

9)
#include<iostream> 
using namespace std; 
  
class base { 
    int arr[10]; 
}; 
  
class b1: public base { }; 
  
class b2: public base { }; 
  
class derived: public b1, public b2 {}; 
  
int main(void) 
{ 
  cout << sizeof(derived); 
  return 0; 
} 

(A) 40
(B) 80
(C) 0
(D) 4



Answer: (B)

Explanation: Since b1 and b2 both inherit from class base, two copies of class base are there in class derived. 
This kind of inheritance without virtual causes wastage of space and ambiguities. 

10)
#include<iostream>
using namespace std;

void Execute(int &x, int y = 200)
{
 int TEMP = x + y;
 x+= TEMP;
 if(y!=200)
     cout<<TEMP<<x<<y<<"--";
}

int main()
{
 int A=50, B=20;
 cout<<A<<B<<"--";
 Execute(A,B);
 cout<<A<<B<<"--";
 return 0;
}

(A) 5020--5020--
(B) 5020--7012020--12020--
(C) 5020--70120200--5020
(D) 5020--7050200--5020--





Ans- B

11) 
class Mycpp
{
    int Mycpp()
    {
       cout<<"Constructor";
       return 0;
     }
};

int main()
{
    Mycpp obj;
    return 0;
}

(A) Constructor
(B) 0
(C) Compilation Error
(D) Runtime Error





Ans- C

12) 
#include <iostream>
using namespace std;
class sample1 
{
    float i, j;
};

class sample2 
{
    int x, y;
   public:
    sample2 (int a, int b) 
    {
      x = a; 
      y = b;
    }
    int result() 
    { 
	    return x + y;
    }
};

int main () 
{
    sample1 d;
    sample2 * padd;
    padd = (sample2*) &d;
    cout<< padd->result();
    return 0;
}

a) 20
b) runtime error
c) random number
d) runtime error or random number




Answer: d

Explanation: 
As it assigns to a reference to an object of another incompatible type using explicit type-casting.

13)
Which collection class(es) allows you to grow or shrink its size and provides
indexed access to its elements, but whose methods are not synchronized? 
(Choose all that apply.)

A. java.util.HashSet
B. java.util.LinkedHashSet
C. java.util.List
D. java.util.ArrayList
E. java.util.Vector
F. java.util.PriorityQueue



Answer:
D is correct. 

All of the collection classes allow you to grow or shrink the size of your collection. 
ArrayList provides an index to its elements. 
The newer collection classes tend not to have synchronized methods. 
Vector is an older implementation of ArrayList functionality and has synchronized methods; it is slower than ArrayList.

14) Given a method declared as

public static <E extends Number> List<E> process(List<E> nums)

A programmer wants to use this method like this
// INSERT DECLARATIONS HERE
output = process(input);

Which pairs of declarations could be placed at // INSERT DECLARATIONS HERE to allow the code to compile? (Choose all that apply.)

A.	ArrayList<Integer> input = null;
	ArrayList<Integer> output = null;

B.	ArrayList<Integer> input = null;
	List<Integer> output = null;

C.	ArrayList<Integer> input = null;
	List<Number> output = null;

D.	List<Number> input = null;
	ArrayList<Integer> output = null;

E.	List<Number> input = null;
	List<Number> output = null;

F.	List<Integer> input = null;
	List<Integer> output = null;

G. None of the above

Answer:
B, E, and F are correct.

The return type of process is definitely declared as a List, not an ArrayList, so A and D are wrong. 
C is wrong because the return type evaluates to List<Integer>, and that can't be assigned to a variable of type List<Number>. 
Of course all these would probably cause a NullPointerException since the variables are still null—
but the question only asked us to get the code to compile. 

15)
Which are true about a method-local inner class? (Choose all that apply.)
A. It must be marked final
B. It can be marked abstract
C. It can be marked public
D. It can be marked static
E. It can access private members of the enclosing class



Answer:
B and E. 

B is correct because a method-local inner class can be abstract, although it
means a subclass of the inner class must be created if the abstract class is to
be used (so an abstract method-local inner class is probably not useful). 

E is correct because a method-local inner class works like any other inner
class—it has a special relationship to an instance of the enclosing class, 
thus it can access all members of the enclosing class.

A is incorrect because a method-local inner class does not have to be declared
final (although it is legal to do so). 

C and D are incorrect because a method-local inner class cannot be made public
(remember—local variables can't be public) or static.

16) Given:

1. public class TestObj {
2. public static void main(String[] args) {
3. Object o = new Object() {
4. public boolean equals(Object obj) {
5. return true;
6. }
7. }
8. System.out.println(o.equals("Fred"));
9. }
10. }

What is the result?

A. An exception occurs at runtime
B. true
C. fred
D. Compilation fails because of an error on line 3
E. Compilation fails because of an error on line 4
F. Compilation fails because of an error on line 8
G. Compilation fails because of an error on a line other than 3, 4, or 8


Answer:
G. This code would be legal if line 7 ended with a semicolon. Remember that line 3 is a
statement that doesn't end until line 7, and a statement needs a closing semicolon!

A, B, C, D, E, and F are incorrect based on the program logic described above. 
If the semicolon were added at line 7, then answer B would be correct—
the program would print true, the return from the equals() method overridden by the anonymous subclass of Object.

17) Given:
1. public class HorseTest {
2. public static void main(String[] args) {
3. class Horse {
4. public String name;
5. public Horse(String s) {
6. name = s;
7. }
8. }
9. Object obj = new Horse("Zippo");
10. System.out.println(obj.name);
11. }
12. }


What is the result?

A. An exception occurs at runtime at line 10
B. Zippo
C. Compilation fails because of an error on line 3
D. Compilation fails because of an error on line 9
E. Compilation fails because of an error on line 10




Answer : E

If you use a reference variable of type Object, you can access only those members defined in class Object.

18)

Given:
3. class MyThread extends Thread {
4. public static void main(String [] args) {
5. MyThread t = new MyThread();
6. Thread x = new Thread(t);
7. x.start();
8. }
9. public void run() {
10. for(int i=0;i<3;++i) {
11. System.out.print(i + "..");
12. } } }


What is the result of this code?
A. Compilation fails
B. 1..2..3..
C. 0..1..2..3..
D. 0..1..2..
E. An exception occurs at runtime

Answer:

D is correct. The thread MyThread will start and loop three times (from 0 to 2).

A is incorrect because the Thread class implements the Runnable interface; 
therefore, in line 5, Thread can take an object of type Thread as an argument in the constructor (this is NOT recommended). 
B and C are incorrect because the variable i in the for loop starts with a value of 0 and ends with a value of 2. 
E is incorrect based on the above.

19) Given:
3. class Test {
4. public static void main(String [] args) {
5. printAll(args);
6. }
7. public static void printAll(String[] lines) {
8. for(int i=0;i<lines.length;i++){
9. System.out.println(lines[i]);
10. Thread.currentThread().sleep(1000);
11. } } }

The static method Thread.currentThread() returns a reference to the currently executing Thread object. 

What is the result of this code?


A. Each String in the array lines will print, with exactly a 1-second pause between lines
B. Each String in the array lines will print, with no pause in between because this method is not executed in a Thread
C. Each String in the array lines will print, and there is no guarantee there will be a pause because currentThread() may not retrieve this thread
D.This code will not compile
E. Each String in the lines array will print, with at least a one-second pause between lines

Answer:
D is correct. The sleep() method must be enclosed in a try/catch block, or the method printAll() must declare it throws the InterruptedException.
E is incorrect, but it would be correct if the InterruptedException was dealt with (A is too precise). 
B is incorrect (even if the InterruptedException was dealt with) because all Java code, including the main() method, runs in threads. 
C is incorrect. The sleep() method is static, it always affects the currently executing thread. 



20. Assume you have a class that holds two private variables: a and b. 
Which of the following pairs can prevent concurrent access problems in that class? (Choose all that apply.)

A. public int read(){return a+b;}
public void set(int a, int b){this.a=a;this.b=b;}

B. public synchronized int read(){return a+b;}
public synchronized void set(int a, int b){this.a=a;this.b=b;}

C. public int read(){synchronized(a){return a+b;}}
public void set(int a, int b){synchronized(a){this.a=a;this.b=b;}}

D. public int read(){synchronized(a){return a+b;}}
public void set(int a, int b){synchronized(b){this.a=a;this.b=b;}}

E. public synchronized(this) int read(){return a+b;}
public synchronized(this) void set(int a, int b){this.a=a;this.b=b;}

F. public int read(){synchronized(this){return a+b;}}
public void set(int a, int b){synchronized(this){this.a=a;this.b=b;}}

Answer:
B and F are correct. 

By marking the methods as synchronized, the threads will get the lock of the this object before proceeding. 
Only one thread will be setting or reading at any given moment, thereby assuring that read() always returns the addition of a valid pair.
A is incorrect because it is not synchronized; therefore, there is no guarantee that the values added by the read() method belong to the same pair. 
C and D are incorrect; only objects can be used to synchronize on. 
E fails —it is not possible to select other objects (even this) to synchronize on when declaring a method as synchronized. 


## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/1st%2BJuly%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/1st+July+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
