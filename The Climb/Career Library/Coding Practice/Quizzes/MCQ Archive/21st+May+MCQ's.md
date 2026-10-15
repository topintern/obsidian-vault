---
kind: "study-reference"
title: "21st+May+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/21st+May+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 21st+May+MCQ's

[[The Climb/Career Library/Career Library]]

1)

What is the output of following function for start pointing to first node of following linked list?

1->2->3->4->5->6

void fun(struct node* start) 
{ 
  if(start == NULL) 
    return; 
  printf("%d  ", start->data);  
   
  if(start->next != NULL ) 
    fun(start->next->next); 
  printf("%d  ", start->data); 
} 

(A) 1 4 6 6 4 1
(B) 1 3 5 1 3 5
(C) 1 2 3 5
(D) 1 3 5 5 3 1














Answer: (D)

Explanation: fun() prints alternate nodes of the given Linked List, first from head to end, and then from end to head. 
If Linked List has even number of nodes, then skips the last node. 


2)
Which of the following is true about linked list implementation of stack?
(A) In push operation, if new nodes are inserted at the beginning of linked list, then in pop operation, nodes must be removed from end.
(B) In push operation, if new nodes are inserted at the end, then in pop operation, nodes must be removed from the beginning.
(C) Depends on the Application
(D) None of these














Answer: (D)


3)
What is the worst case time complexity for search, insert and delete operations in a general Binary Search Tree?
(A) O(n) for all
(B) O(Logn) for all
(C) O(Logn) for search and insert, and O(n) for delete
(D) O(Logn) for search, and O(n) for insert and delete





















Answer: (A)

Explanation: In skewed Binary Search Tree (BST), all three operations can take O(n). See the following example BST and operations.

          10
        /
       20
      /
     30
    / 
   40

Search 40. 
Delete 40
Insert 50.



4)

Which of the following piece of code has the functionality of counting the number of elements in the list?


a)
public int length(Node head)
{
	int size = 0;
	Node cur = head;
	while(cur!=null)
	{
	    size++;
	    cur = cur.getNext();
	}
	return size;
}

b)
public int length(Node head)
{
        int size = 0;
	Node cur = head;
	while(cur!=null)
	{
	    cur.getNext();
	    size++;
	}
	return size;
}

c)

public int length(Node head)
{
	int size = 0;
	Node cur = head;
	while(cur!=null)
	{
	    size++;
	    cur = head.getNext();
	}
}

d)

public int length(Node head)
{
	int size = 0;
	Node cur = head;
	while(cur!=null)
	{
	    size++;
	    cur = cur.getNext().getNext();
	}
	return size;
}









Answer: a
Explanation: ‘cur’ pointer traverses through list and increments the size variable until the end of list is reached.





5)Given a hash table T with 25 slots that stores 2000 elements, the load factor a for T is ______

(A) 80
(B) 0.0125
(C) 8000
(D) 1.25

















Answer: (A)

Explanation: load factor = (no. of elements) / (no. of table slots) = 2000/25 = 80



6)
#include<stdio.h> 
#define f(g,g2) g##g2 
int main() 
{ 
int var12 = 100; 
printf("%d", f(var,12)); 
return 0; 
} 

A) 100
(B) Compiler Error
(C) 0
(D) 1










Answer: (A)

Explanation: The operator ## is called “Token-Pasting” or “Merge” Operator. 
It merges two tokens into one token. So, after preprocessing, the main function becomes as follows, and prints 100. 


7)
#include <stdio.h> 
#include <stdlib.h> 
int main(void) 
{ 
	int i;
    char x = 'A'; 
    char* y = (char*)malloc(sizeof(char)); 
    y = &x; 
    for (i = 0; i < 26; i++) { 
        printf("%c", x); 
        y[0] += 1; 
    } 
} 

A. SDKJNSDNSKDJNSKDVNSKJD
B. SLKFVMSLFKVSFLALKDJF
C. ABCDEFGHIJKLMNOPQRSTUVWXYZ
D. NONEOFTHEABOVE

















Answer:

C. ABCDEFGHIJKLMNOPQRSTUVWXYZ

Explanation:
The space allotted for a character is just 1 byte or 8 bits. y is being allocated during run time. It contains the address of x
. Now, we can index the memory location of x. And, any change to y reflects in x also. 
When y[0]+=1 is executed, in each loop, the last bit in that 1 byte of data is being incremented by 1 like:








8)
#include <stdio.h> 
  
int main() 
{ 
   int x=1,y=0,z=5;
   int a = x && y || z++;
   printf(" %d ",z);
    return 0; 
} 


A) 0
B) Varies
C) 6
D) 5










Ans - C


9)

#include <stdio.h> 
  
int main() 
{ 
    int i = 1024; 
    for (; i; i >>= 1) 
        printf("hello"); 
    return 0; 
} 

How many times will hello be printed in the above program?
(A) 10
(B) 11
(C) Infinite
(D) The program will show compile-time error







Answer: (B)

Explanation: In for loop, mentioning expression is optional. >>= is a composite operator. 
It shifts the binary representation of the value by 1 to the right and assigns the resulting value to the same variable.
The for loop is executed until value of variable i doesn’t drop to 0.


10)

#include <stdio.h> 
int main() 
{ 
    int check = 20, arr[] = {10, 20, 30}; 
    switch (check) 
    { 
        case arr[0]: printf("amazon "); 
        case arr[1]: printf("wow "); 
        case arr[2]: printf("India Amazon"); 
    } 
    return 0; 
} 

(A) amazon
(B) amazon wow
(C) India Amazon
(D) Compile-time error
















Answer: (D)

Explanation: The case labels must be constant inside switch block.



11)What is the use of this pointer?
(A) When local variable’s name is same as member’s name, we can access member using this pointer.
(B) To return reference to the calling object
(C) Can be used for chained function calls on an object
(D) All of the above














Answer: (D)


12)

Which operator can not be overloaded?

(A) +
(B) -
(C) *
(D) ::

















Ans-D



13)
#include <iostream> 
using namespace std; 
  
template <typename T> 
T max(T x, T y) 
{ 
    return (x > y)? x : y; 
} 
int main() 
{ 
    cout << max(3, 7) << std::endl; 
    cout << max(3.0, 7.0) << std::endl; 
    cout << max(3, 7.0) << std::endl; 
    return 0; 
} 














(A)
7
7.0
7.0
(B) Compiler Error in all cout statements as data type is not specified.
(C) Compiler Error in last cout statement as call to max is ambiguous.
(D) None of the above


Answer: (C)









14)
#include<iostream> 
using namespace std; 
  
int fun(int x = 0, int y = 0, int z) 
{  return (x + y + z); } 
  
int main() 
{ 
   cout << fun(10); 
   return 0; 
} 

(A) 10
(B) 0
(C) 20
(D) Compiler Error














Answer: (D)

Explanation: All default arguments must be the rightmost arguments.


15)
#include<iostream> 
using namespace std; 
   
#include<iostream.h>  
class X
{
public: X()
        { cout<<"X"; }
        ~X()
        { cout<<"~X"; }
};

class Y : public X
{
public: Y()
        { cout<<"Y"; }
        ~Y()
        { cout<<"~Y"; }
};

int main()
{
    Y obj;
    return 0;
}

(A) XY~X~Y
(B) XY~Y~X
(C) X~XY~Y
(D) X~X~YY









Ans-B



16)
class Test { 
  int i; 
}  
class Main { 
   public static void main(String args[]) {  
     Test t;  
     System.out.println(t.i);  
}   
}

(A) 0
(B) garbage value
(C) compiler error
(D) runtime error
















Answer: (C)



17)

final class Complex { 
  
    private final double re; 
    private final double im; 
  
    public Complex(double re, double im) { 
        this.re = re; 
        this.im = im; 
    } 
  
    public String toString() { 
        return "(" + re + " + " + im + "i)"; 
    } 
} 
  
class Main { 
  public static void main(String args[]) 
  { 
       Complex c = new Complex(10, 15); 
       System.out.println("Complex number is " + c); 
  }          
} 

(A)Complex number is (10.0 + 15.0i)
(B) Compiler Error
(C) Complex number is SOME_GARBAGE
(D) Complex number is Complex@8e2fb5
     Here 8e2fb5 is hash code of c












Answer: (A)



18)Given:
12. TreeSet map = new TreeSet();
13. map.add("one");
14. map.add("two");
15. map.add("three");
16. map.add("four");
17. map.add("one");
18. Iterator it = map.iterator();
19. while (it.hasNext() ) {
20. System.out.print( it.next() + " " );
21. }
What is the result?
A. Compilation fails.
B. one two three four
C. four three two one
D. four one three two
E. one two three four one
F. one four three two one
G. An exception is thrown at runtime.
H. The print order is not guaranteed.









Answer:
-> D is correct. TreeSet assures no duplicate entries; also, when it is accessed it
will return elements in natural order, which for Strings means alphabetical.



19) Given:
class TestOne implements Runnable {
 public static void main (String[] args) throws Exception {
 Thread t = new Thread(new TestOne());
 System.out.print("Started ");
 t.start();
 t.join();
 System.out.print("Complete");
 }
 public void run() {
 for (int i = 0; i < 4; i++) {
 System.out.print(i+" ");
 }
 }
}


What can be a result?
A. Compilation fails.
B. An exception is thrown at runtime.
C. The code executes and prints "Started Complete".
D. The code executes and prints "Started Complete 0 1 2 3".
E. The code executes and prints "Started 0 1 2 3 Complete".








Answer: E

20)
Given:
class Hexy {
public static void main(String[] args) {
Integer i = 42;
String s = (i<40)?"life":(i>50)?"universe":"everything";
System.out.println(s);
} }
What is the result?
A. null
B. life
C. universe
D. everything
E. Compilation fails.
F. An exception is thrown at runtime.
















Answer:
-> D is correct. This is a ternary nested in a ternary with a little unboxing thrown in.
Both of the ternary expressions are false.

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/21st%2BMay%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/21st+May+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
