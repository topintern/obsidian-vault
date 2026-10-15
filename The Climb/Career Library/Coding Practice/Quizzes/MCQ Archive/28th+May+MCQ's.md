---
kind: "study-reference"
title: "28th+May+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/28th+May+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 28th+May+MCQ's

[[The Climb/Career Library/Career Library]]

1)

Output of the following in C Language
#include <stdio.h> 
int main() 
{ 
    int i = 5, j = 10, k = 15; 
    printf("%d ", sizeof(k /= i + j)); 
    printf("%d", k); 
    return 0; 
} 

Assume size of an integer as 4 bytes. What is the output of above program?
(A) 4 1
(B) 4 15
(C) 2 1
(D) Compile-time error














Answer: (B)


Explanation: 
The main theme of the program lies here: sizeof(k /= i + j). 
An expression doesn’t get evaluated inside sizeof operator.
sizeof operator returns sizeof(int) because the result of expression will be an integer. 
As the expression is not evaluated, value of k will not be changed



2)

Consider the following two C lines

int var1; 
extern int var2; 

Which of the following statements is correct

(A) Both statements only declare variables, don’t define them.
(B) First statement declares and defines var1, but second statement only declares var2
(C) Both statements declare define variables var1 and var2
(D) None of these

















Answer: (B)



3)In C Language , When fopen() is not able to open a file, it returns

(A) EOF
(B) NULL
(C) Runtime Error
(D) Compiler Dependent
























Answer: (B)



4)
Output of the following in  C 
#include<stdio.h>
  
int main() 
{ 
 struct {int a[2];} arr[] = {{1},{2}}; 
  
 printf("%d %d %d %d",arr[0].a[0],arr[0].a[1],arr[1].a[0],arr[1].a[1]); 
  
 return 0; 
} 

(A) Compile error because arr has been defined using struct type incorrectly. First struct type should be defined using tag and then arr should be defined using that tag.
(B) Compile error because apart from definition of arr, another issue is in the initialization of array of struct i.e. arr[].
(C) Compile error because of initialization of array of struct i.e. arr[].
(D) No compile error and it’ll print 1 2 0 0
(E) No compile error and it’ll print 1 0 2 0











Answer: (E)



5)

#include<iostream> 
using namespace std; 
class A 
{ 
    int i; 
public: 
    A(int ii = 0) : i(ii) {} 
    void show() {  cout << i << endl;  } 
}; 
  
class B 
{ 
    int x; 
public: 
    B(int xx) : x(xx) {} 
    operator A() const {  return A(x); } 
}; 
  
void g(A a) 
{ 
    a.show(); 
} 
  
int main() 
{ 
    B b(10); 
    g(b); 
    g(20); 
    return 0; 
}

(A) Compiler Error

(B)
10
20

(C)
20
20

(D)
10
10









Answer: (B)




6)
#include<iostream> 
using namespace std; 
  
class Test 
{ 
private: 
  int x; 
  int y; 
public: 
  Test(int x = 0, int y = 0) { this->x = x; this->y = y; } 
  static void fun1() { cout << "Inside fun1()"; } 
  static void fun2() { cout << "Inside fun2()"; this->fun1(); } 
}; 
  
int main() 
{ 
  Test obj; 
  obj.fun2(); 
  return 0; 
} 

(A) Inside fun2() Inside fun1()
(B) Inside fun2()
(C) Inside fun1() Inside fun2()
(D) Compiler Error







Answer: (D)




7)Which of the following is FALSE about references in C++

(A) References cannot be NULL
(B) A reference must be initialized when declared
(C) Once a reference is created, it cannot be later made to reference another object; it cannot be reset.
(D) References cannot refer to constant value













Answer: (D)



8)

Assume the size of int is 4 bytes and 
int * is also 4 bytes 

#include<iostream> 
using namespace std; 
  
class Test 
{ 
    static int x; 
    int *ptr; 
    int y; 
}; 
  
int main() 
{ 
    Test t; 
    cout << sizeof(t) << " "; 
    cout << sizeof(Test *); 
} 

(A) 12 4
(B) 12 12
(C) 8 4
(D) 8 8

















Answer: (C)



9)What is the best time complexity of bubble sort?

(A) N^2
(B) NlogN
(C) N
(D) N(logN)^2




Answer: (C)

Explanation: The bubble sort is at its best if the input data is sorted. i.e. 
If the input data is sorted in the same order as expected output. 
This can be achieved by using one boolean variable. 
The boolean variable is used to check whether the values are swapped at least once in the inner loop.

Consider the following code snippet:
int main() 
{    
    int arr[] = {10, 20, 30, 40, 50}, i, j, isSwapped; 
    int n = sizeof(arr) / sizeof(*arr); 
    isSwapped = 1; 
    for(i = 0; i < n - 1 && isSwapped; ++i) 
    { 
        isSwapped = 0; 
        for(j = 0; j < n - i - 1; ++j) 
            if (arr[j] > arr[j + 1]) 
            { 
                swap(&arr[j], &arr[j + 1]); 
                isSwapped = 1; 
            } 
    } 
    for(i = 0; i < n; ++i) 
        printf("%d ", arr[i]); 
    return 0; 
} 

Please observe that in the above code, the outer loop runs only once.



10)
What are the appropriate data structures for following algorithms?

1) Breadth First Search                           
2) Depth First Search                            
3) Prim's Minimum Spanning Tree                 
4) Kruskal' Minimum Spanning Tree                

(A)
1) Stack
2) Queue
3) Priority Queue
4) Union Find

(B)
1) Queue
2) Stack
3) Priority Queue
4) Union Find

(C)
1) Stack
2) Queue
3) Union Find
4) Priority Queue 

(D)
1) Priority Queue
2) Queue
3) Stack
4) Union Find


Answer: (B)



11)What does the following C expression do?

 x = x & (x-1) 

(A) Sets all bits as 1
(B) Makes x equals to 0
(C) Turns of the rightmost set bit
(D) Turns of the leftmost set bit














Answer: (C)

Explanation: The expression simply turns off the rightmost set bit.
For example, if x = 14 (1110), x – 1 = 13 (1101) it returns resultant as (1100) i.e, 12 .




12)
Given:
11. public class Key {
12. private long id1;
13. private long id2;
14.
15. // class Key methods
16. }

A programmer is developing a class Key, that will be used as a key in a standard java.util.HashMap.
Which two methods should be overridden to assure that Key works correctly as a key? (Choose two.)

A. public int hashCode()
B. public boolean equals(Key k)
C. public int compareTo(Object o)
D. public boolean equals(Object o)
E. public boolean compareTo(Key k)











Answer: A, D



13)Given:

42. public class ClassA {
43. public int getValue() {
44.int value=0;
45. boolean setting = true;
46. String title="Hello";
47. if (value || (setting && title == "Hello")) { return 1; }
48. if (value == 1 & title.equals("Hello")) { return 2; }
49. }
50. }
And:
70. ClassA a = new ClassA();
71. a.getValue();
What is the result?
A. 1
B. 2
C. Compilation fails.
D. The code runs with no output.
E. An exception is thrown at runtime.










Answer: C



14)Given:

class CardBoard {
Short story = 5;
CardBoard go(CardBoard cb) {
cb = null;
return cb;
}
public static void main(String[] args) {
CardBoard c1 = new CardBoard();     
CardBoard c2 = new CardBoard();    
CardBoard c3 = c1.go(c2);     
c1 = null;
// do Stuff
} }
When // doStuff is reached, how many objects are eligible for GC?

A. 0
B. 1
C. 2
D. Compilation fails.
E. It is not possible to know.
F. An exception is thrown at runtime.





Answer: C is correct. 

 Only one CardBoard object (c1) is eligible, but it has an associated Short wrapper object that is also eligible.
A, B, D, E, and F are incorrect based on the above. 





15)   The "all-or-none" property is commonly referred to as _________
a) Isolation
b) Durability
c) Atomicity
d) None of the mentioned










Answer: c



16)The deadlock state can be changed back to stable state by using _____________ statement.
a) Commit
b) Rollback
c) Savepoint
d) Deadlock












Answer: (b). Rollback



17) what operator tests column for the absence of data ?

A) Exists Operator
B) NOT Operator
C) IS NULL Operator
D) None of these















Ans - C



18) ________ diagrams are used to illustrate data structures, and the static snapshots instances of the things found in the class diagrams. 

a.use case 
b.Object 
c.Collaboration 
d.Sequence 














Ans-b


19) Forward engineering and reverse engineering can be applicable to ________

a. class diagram 
b. stereotypes 
c. tagged values 
d. adornments 
















Ans- a



20) UML is useful to ________ a system as it is or as we want it to be. 

a. Visualize 
b. Specify 
c. Document 
d. All of these













Ans- d

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/28th%2BMay%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/28th+May+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
