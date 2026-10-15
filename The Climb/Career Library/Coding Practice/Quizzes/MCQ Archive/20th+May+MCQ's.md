---
kind: "study-reference"
title: "20th+May+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/20th+May+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 20th+May+MCQ's

[[The Climb/Career Library/Career Library]]

1) For a given graph G having v vertices and e edges which is connected and has no cycles, which of the following statements is true?

a) v=e
b) v = e+1
c) v + 1 = e
d) v = e-1




























Answer: b


2)  What is the number of edges present in a complete graph having n vertices?
a) (n*(n+1))/2
b) (n*(n-1))/2
c) n
d) Information given is insufficient















Answer: b

Explanation: Number of ways in which every vertex can be connected to each other is nC2.



3)
Suppose the numbers 7, 5, 1, 8, 3, 6, 0, 9, 4, 2 are inserted in that order into an initially empty binary search tree. 

The binary search tree uses the usual ordering on natural numbers. What is the in-order traversal sequence of the resultant tree?
(A) 7 5 1 0 3 2 4 6 8 9
(B) 0 2 4 3 1 6 5 9 8 7
(C) 0 1 2 3 4 5 6 7 8 9
(D) 9 8 6 4 2 3 0 1 5 7














Answer: (C)


4)Following is C like pseudo code of a function that takes a Queue as an argument, and uses a stack S to do processing.

void fun(Queue *Q) 
{ 
	Stack S; // Say it creates an empty stack S 

	// Run while Q is not empty 
	while (!isEmpty(Q)) 
	{ 
		// deQueue an item from Q and push the dequeued item to S 
		push(&S, deQueue(Q)); 
	} 

	// Run while Stack S is not empty 
	while (!isEmpty(&S)) 
	{ 
	// Pop an item from S and enqueue the poppped item to Q 
	enQueue(Q, pop(&S)); 
	} 
} 


What does the above function do in general?
(A) Removes the last from Q
(B) Keeps the Q same as it was before the call
(C) Makes Q empty
(D) Reverses the Q





Answer: (D)

Explanation: The function takes a queue Q as an argument. It dequeues all items of Q and pushes them to a stack S. 
Then pops all items of S and enqueues the items back to Q. 
Since stack is LIFO order, all items of queue are reversed.


5)

Given pointer to a node X in a singly linked list. Only one pointer is given, pointer to head node is not given, can we delete the node X from given linked list?
(A) Possible if X is not last node. Use following two steps (a) Copy the data of next of X to X. (b) Delete next of X.
(B) Possible if size of linked list is even.
(C) Possible if size of linked list is odd
(D) Possible if X is not first node. Use following two steps (a) Copy the data of next of X to X. (b) Delete next of X.








Answer: (A)



6)


int main() 
{ 
    unsigned int i=65000; 
    while ( i++ != 0 ); 
    printf("%d",i); 
    return 0; 
} 


A) 1
B) 0
C) compilation fails
D) None of these







Ans - A



7)
#include<stdio.h>
void main() {
char b[]="12345\0";
int x = strlen(b);
printf("here in 3 %d\n ", ++x);
}


a)here in 3 3
b)here in 3 6
c)here in 3 9
d)here in 3 5








Ans- b 



8) Consider the following C function:

int  f(int n)   
{
static int r = 0; 
if(n<=0) 
	return 1;   
if(n>3)
{ 
r=n;
return f(n-2)+2;
} 
return (f(n-1)+r);
} 

What is the value of f(5)?
(A) 3 
(B) 7
(C) 9
(D) 18






Ans - [D] 

f(5) will return f(3)+2 
f(3) will return  f(2)+5 
f(2) will return f(1)+5 
f(1) will return f(0)+5 
f(0) will return 1 
f(1) will return 6 
f(2) will return 11 
f(3) will return 16 
f(5) will return 18


9)

#include <stdio.h> 
int main() 
{ 
    int arr[] = {1, 2, 3, 4, 5}; 
    int *p = arr; 
    ++*p; 
    p += 2; 
    printf("%d", *p); 
    return 0; 
} 

(A) 2
(B) 3
(C) 4
(D) Compiler Error





Answer: (B)

Explanation: The expression ++*p is evaluated as "++(*p)" . 

So it increments the value of first element of array (doesn’t change the pointer p).

When p += 2 is done, p is changed to point to third element of array.




10)

#include<stdio.h> 
int main() 
{ 
    int a, b = 10; 
    a = -b--; 
    printf("a = %d, b = %d", a, b); 
    return 0; 
} 


A) a = -10, b = 9
B) a = -9 , b =-10
C) a = 10, b = 9
D) a = -10, b = -9




Ans- A



11)
import java.util.*; 
  
class Demo { 
    public static void main(String[] args) 
    { 
        ArrayList<Integer> arr = new ArrayList<Integer>(); 
        arr.add(11); 
        arr.add(2); 
        arr.add(3); 
        arr.add(5); 
        arr.add(7); 
        arr.remove(new Integer(7)); 
        arr.remove(2); 
        for (int i = 0; i < arr.size(); i++) 
            System.out.print(arr.get(i) + " "); 
    } 
} 

A. Compilation error.
B. 11 3 5
C. 11 2 5
D. Run time exception




Answer: C.


12)
import java.util.*; 
  
class Demo { 
    public static void main(String[] args) 
    { 
        Deque<Integer> dq = new LinkedList<Integer>(); 
        dq.offerFirst(1); 
        dq.offerFirst(2); 
        dq.offerFirst(3); 
        dq.offerLast(4); 
        Queue<Integer> q = new LinkedList<Integer>(); 
        Iterator it = dq.descendingIterator(); 
        while (it.hasNext()) { 
            System.out.print(it.next() + " "); 
        } 
    } 
} 

A. 1 2 3 4
B. 4 1 2 3
C. 4 3 2 1
D. Compilation fails
E. Run time exception




Answer: B.


13) 	

What will be the output of the program?

class MyThread extends Thread 
{
    MyThread() 
    {
        System.out.print(" MyThread");
    }
    public void run() 
    {
        System.out.print(" bar");
    }
    public void run(String s) 
    {
        System.out.println(" baz");
    }
}
public class TestThreads 
{
    public static void main (String [] args) 
    {
        Thread t = new MyThread() 
        {
            public void run() 
            {
                System.out.println(" foo");
            }
        };
        t.start();
    }
}

A. 	foo
B. 	MyThread foo
C. 	MyThread bar
D. 	foo bar

Answer: Option B

Explanation:

Option B is correct because in the first line of main we're constructing an instance of an anonymous inner class extending from MyThread. 
So the MyThread constructor runs and prints "MyThread". 
The next statement in main invokes start() on the new thread instance, which causes the overridden run() method 
(the run() method defined in the anonymous inner class) to be invoked, which prints "foo"




14) 	

What is the numerical range of a char?
A. 	-128 to 127
B. 	-(215) to (215) - 1
C. 	0 to 32767
D. 	0 to 65535




Answer: Option D

Explanation:
A char is really a 16-bit integer behind the scenes, so it supports 2^16 (from 0 to 65535) values.



15) 	

Which class does not override the equals() and hashCode() methods, inheriting them directly from class Object?
A. 	java.lang.String
B. 	java.lang.Double
C. 	java.lang.StringBuffer
D. 	java.lang.Character

Answer: Option C

Explanation:

java.lang.StringBuffer is the only class in the list that uses the default methods provided by class Object.



16) What happens if the following code is compiled on both C and C++?

#include<stdio.h>
struct STRUCT
{
private:
	int a;
};
int main()
{
	printf("%d\n", (int)sizeof(struct STRUCT));
	return 0;
}

a) The program runs fine and both prints output “HELLO THIS IS STRUCTURE”
b) The program gives an error in case of C but runs perfectly in case of C++
c) The program gives an error in case of C++ but runs perfectly in case of C
d) The program gives an error in case of both C and C++





Answer: b



17)
#include<iostream> 
using namespace std; 
  
int x = 10; 
void fun() 
{ 
    int x = 2; 
    { 
        int x = 1; 
        cout << ::x << endl;  
    } 
} 
  
int main() 
{ 
    fun(); 
    return 0; 
}


A) Compilation fails
B) 10
C) 1
D) 2
E) None of these 





Ans - B



18)

Assume class TEST. 

Which of the following statements is/are responsible to invoke copy constructor?(Choose all that apply)

a. TEST T2(T1)
b. TEST T4 = T1
c. T2 = T1
d. None of these
e. All of these





ANSWER: both a and b




19)

#include <iostream>
using namespace std;
class A
{
protected:
    int x;
public:
    A() {x = 0;}
    friend void show();
};
 
class B: public A
{
public:
    B() : y (0) {}
private:
    int y;
};
 
void show()
{
    A a;
    B b;
    cout << "The default value of A::x = " << a.x << " ";
    cout << "The default value of B::y = " << b.y;
}

A)Compiler Error in show() because x is protected in class A
B)Compiler Error in show() because y is private in class b
C)The default value of A::x = 0 The default value of B::y = 0
D)Compiler Dependent





Answer: (B)


20)
#include <iostream> 
using namespace std; 
  
class A 
{ 
    int id; 
public: 
    A (int i) { id = i; } 
    void print () { cout << id << endl; } 
}; 
  
int main() 
{ 
    A a[2]; 
    a[0].print(); 
    a[1].print(); 
    return 0; 
} 
A) Compilation error
B) 0
    0
 C) Garbage value
     Garbage Value
 D) 0
      1




  Ans - A


## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/20th%2BMay%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/20th+May+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
