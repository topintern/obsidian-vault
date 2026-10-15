---
kind: "study-reference"
title: "22nd+May+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/22nd+May+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 22nd+May+MCQ's

[[The Climb/Career Library/Career Library]]

1)

The preorder traversal sequence of a binary search tree is 30, 20, 10, 15, 25, 23, 39, 35, 42. 

Which one of the following is the postorder traversal sequence of the same tree?
(A) 10, 20, 15, 23, 25, 35, 42, 39, 30
(B) 15, 10, 25, 23, 20, 42, 35, 39, 30
(C) 15, 20, 10, 23, 25, 42, 35, 39, 30
(D) 15, 10, 23, 25, 20, 35, 42, 39, 30


Answer: (D)

Explanation: The following is the constructed tree

            30
         /      \
        20       39 
       /  \     /  \
     10    25  35  42  
      \   /
      15 23


2)struct node { 
    int data; 
    struct node *left, *right; 
}; 
  
int count = 0; 
  
void print(struct node *root, int k) 
{ 
    if (root != NULL && count <= k) 
    { 
        print(root->right, k); 
        count++; 
        if (count == k) 
          printf("%d ", root->data); 
       print(root->left, k); 
    } 
} 

What is the output of print(root, 3) where root represent root of the following BST.

                   15
                /     \
              10      20
             / \     /  \
            8  12   16  25   

(A) 10
(B) 16
(C) 20
(D) 20 10


Answer: (B)


3)
Which one of the following array represents a binary max-heap?
(A) [26, 13, 17, 14, 11, 9, 15]
(B) [26, 15, 14, 17, 11, 9, 13]
(C) [26, 15, 17, 14, 11, 9, 13]
(D) [26, 15, 13, 14, 11, 9, 17]


Answer: (C)

Explanation: For max heap we will compare parent node(i) with its left-child(2 * i) and right-child(2 * i + 1):



4)
Which one of the following is an application of Queue Data Structure?
(A) When a resource is shared among multiple consumers.
(B) When data is transferred asynchronously (data not necessarily received at same rate as sent) between two processes
(C) Load Balancing
(D) All of these


Answer: (D)


5)
Which traversal of tree resembles the breadth first search of the graph?
(A) Preorder
(B) Inorder
(C) Postorder
(D) Level order


Answer: (D)




6)
Given i = 0, j = 1, k = –1
x = 0.5, y = 0.0
What is the output of the following expression in C language ?
x * y < i + j || k

(A) -1
(B) 0
(C) 1
(D) 2


Answer: (C)

Explanation:

  = x * y < i + j || k
  = 0.5 * 0.0 < 0 + 1 || -1
  = 0.0 <  0 + 1 || -1 
  = 0.0 < 1 || -1
  = 1 || -1
  = 1

So, option (C) is correct.


7)What will be the output of the program ?

#include<stdio.h>

int main()
{
    int i=3, *j, k;
    j = &i;
    printf("%d\n", i**j*i+*j);
    return 0;
}

A. 	30
B. 	27
C. 	9
D. 	3

Answer: Option A



8)
#include<stdio.h>

int main()
{
    int ***r, **q, *p, i=8;
    p = &i;
    q = &p;
    r = &q;
    printf("%d, %d, %d\n", *p, **q, ***r);
    return 0;
}

A. 	8, 8, 8
B. 	4000, 4002, 4004
C. 	4000, 4004, 4008
D. 	4000, 4008, 4016

Answer: Option A


9)

#include<stdio.h>

int main()
{
    int arr[1]={10};
    printf("%d\n", 0[arr]);
    return 0;
}

A. 	1
B. 	10
C. 	0
D. 	6

Answer: Option B


10) 	



#include<stdio.h>
#define INFINITE while(1)

void main()
{
    INFINITE
    printf("hello");
}

A. 	None of these
B. 	prints hello only one time
C.	Compilation fails
D.	prints hello infinite times

Answer: Option D



11)
#include<iostream> 
using namespace std; 
class Test { 
    Test() { cout << "Constructor called"; } 
}; 
  
int main() 
{ 
   Test t1; 
   return 0; 
} 

(A) Compiler Error
(B) Runtime Error
(C) Constructor called
(D) None of these

Answer: (A)



12)
#include<iostream> 
using namespace std; 
class Base 
{ 
public: 
    virtual void show() = 0; 
}; 
  
class Derived : public Base { }; 
  
int main(void) 
{ 
    Derived q; 
    return 0; 
} 

(A) Segmentation fault
(B) Compiler Error
(C) No compiler Error
(D) None of these


Answer: (B)




13)

#include <iostream> 
using namespace std; 
  
template <class T> 
class Test 
{ 
private: 
    T val; 
public: 
    static int count; 
    Test()  {   count++;   } 
}; 
  
template<class T> 
int Test<T>::count = 0; 
  
int main() 
{ 
    Test<int> a; 
    Test<int> b; 
    Test<double> c; 
    cout << Test<int>::count   << endl; 
    cout << Test<double>::count << endl; 
    return 0; 
} 

(A)
0
0

(B)
1
1

(C)
2
1

(D)
1
0


Answer: (C)



14)
#include<iostream> 
using namespace std; 
  
class Base {}; 
class Derived: public Base {}; 
int main() 
{ 
   Derived d; 
   try { 
       throw d; 
   } 
   catch(Base b) { 
        cout<<"Caught Base Exception"; 
   } 
   catch(Derived d) { 
        cout<<"Caught Derived Exception"; 
   } 
   return 0; 
} 

(A) Caught Derived Exception
(B) Caught Base Exception
(C) Compiler Error
(D) Segementation fault


Answer: (B)



15)

#include <iostream> 
using namespace std; 
  
class Test 
{ 
    static int x; 
public: 
    Test() { x++; } 
    static int getX() {return x;} 
}; 
  
int Test::x = 0; 
  
int main() 
{ 
    cout << Test::getX() << " "; 
    Test t[5]; 
    cout << Test::getX(); 
}

(A) 0 0
(B) 5 5
(C) 0 5
(D) Compiler Error


Answer: (C)





16)
public class A { 
    public static void main(String[] args) 
    { 
        System.out.println('j' + 'a' + 'v' + 'a'); 
    } 
} 


A) java
B) Compilation fails
C) 'j''a''v''a'
D) None of these

“java” would be printed if String literals (in double quotes) are used, 
but in the question since character literals has been used, these won’t be concatenated. 
Therefore After execution of the program, an addition of each equivalent ASCII(Unicode) value of the character will be obtained.
Hence the output is 106 + 97 + 118 + 97 = 418


17)
class Test 
{ 
    static int a; 
      
    static
    { 
        a = 4; 
        System.out.println ("inside static block\n"); 
        System.out.println ("a = " + a); 
    } 
      
    Test() 
    { 
        System.out.println ("\ninside constructor\n"); 
        a = 10; 
    } 
      
    public static void func() 
    { 
        a = a + 1; 
        System.out.println ("a = " + a); 
    } 
      
    public static void main(String[] args) 
    { 
  
        Test obj = new Test(); 
        obj.func(); 
  
    } 
} 
  

(A)

inside static block
a = 4
inside constructor
a = 11

(B) Compiler Error
(C) Run Time Error
(D)

inside static block
a = 4
inside constructor
a = 5

(E)


inside static block
a = 10
inside constructor
a = 11


Answer: (A)



18)
Which three are methods of the Object class?

   1) notify();
   2)notifyAll();
   3) isInterrupted();
   4) synchronized();
   5) interrupt();
   6) wait(long msecs);
   7) sleep(long msecs);
   8) yield();

A. 	1, 2, 4
B. 	2, 4, 5
C. 	1, 2, 6
D. 	2, 3, 4

Answer: Option C



19) 	

Which cannot directly cause a thread to stop executing?
A. 	Calling the SetPriority() method on a Thread object.
B. 	Calling the wait() method on an object.
C. 	Calling notify() method on an object.
D. 	Calling read() method on an InputStream object.

Answer: Option C

Explanation:

Option C is correct. notify() - wakes up a single thread that is waiting on this object's monitor.


20)
import java.util.*;
    public class Demo

    {

      public static void main(String[] args)

      {

    		Map<Integer, Object> sampleMap = new TreeMap<Integer, Object>();
    		sampleMap.put(1, null); 
    		sampleMap.put(5, null); 
    		sampleMap.put(3, null); 
    		sampleMap.put(2, null); 
    		sampleMap.put(4, null); 
               System.out.println(sampleMap);

       }

    }

a) {1=null, 2=null, 3=null, 4=null, 5=null}
b) {5=null}
c) Exception is thrown
d) {1=null, 5=null, 3=null, 2=null, 4=null}

Answer: a

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/22nd%2BMay%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/22nd+May+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
