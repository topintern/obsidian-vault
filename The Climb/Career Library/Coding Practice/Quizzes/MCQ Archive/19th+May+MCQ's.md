---
kind: "study-reference"
title: "19th+May+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/19th+May+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 19th+May+MCQ's

[[The Climb/Career Library/Career Library]]

1) You have to sort a list L, consisting of a sorted list followed by a few ‘random’ elements.
Which of the following sorting method would be most suitable for such a task?

(A) Bubble sort
(B) Selection sort
(C) Quick sort
(D) Insertion sort




























Answer: (D)

Explanation: For a sorted list with few random numbers:
Bubble sort will take O(n2) time in best case.
Selection sort will take O(n2) time in best case.
Quick sort will take O(n2) time in this case because it is the worst case for quick sort.
Insertion sort will take O(n)

So, option (D) is correct.


2) Which of the following algorithms can be used to most efficiently determine
the presence of a cycle in a given graph ?
(A) Depth First Search
(B) Breadth First Search
(C) Prim’s Minimum Spanning Tree Algorithm
(D) Kruskal’ Minimum Spanning Tree Algorithm























Answer: (A)

3) Traversal of a graph is different from tree because
(A) There can be a loop in graph so we must maintain a visited flag for every vertex
(B) DFS of a graph uses stack, but inorrder traversal of a tree is recursive
(C) BFS of a graph uses queue, but a time efficient BFS of a tree is recursive.
(D) All of these


















Answer: (A) 



4)
Following function is supposed to calculate the maximum depth or height of a Binary tree — 
the number of nodes along the longest path from the root node down to the farthest leaf node.

int maxDepth(struct node* node)
{
   if (node==NULL)
       return 0;
   else
   {
       /* compute the depth of each subtree */
       int lDepth = maxDepth(node->left);
       int rDepth = maxDepth(node->right);
  
       /* use the larger one */
       if (lDepth > rDepth)
           return X;
       else return Y;
   }
}

What should be the values of X and Y so that the function works correctly?
(A) X = lDepth, Y = rDepth
(B) X = lDepth + 1, Y = rDepth + 1
(C) X = lDepth – 1, Y = rDepth -1
(D) None of the above




Answer: (B) 

Explanation: If a tree is not empty, height of tree is
MAX(Height of Left Subtree, Height of Right Subtree) + 1


5)
Consider a situation where swap operation is very costly. 
Which of the following sorting algorithms should be preferred so that the number
of swap operations are minimized in general?

(A) Heap Sort
(B) Selection Sort
(C) Insertion Sort
(D) Merge Sort



















Answer: (B)

Explanation:

Selection sort makes O(n) swaps which is minimum among all sorting algorithms mentioned above.


6)

A CPP Program contains the following declaration, what would be the value of the
expression abs(i-2*j) ?

int i=8,j=5;
abs(i-2*j);

A)2
B)6
C)-2
D) compilation error










Ans- A



7)
Assuming, x,y and z are floating point variables and they have been assigned the values 
x=8.8, y=3.5 and  z= -5.2

what will be the value of the arithmetic expression 2*x/(3*y) in CPP ?

A)2
B)1.6
C)1.67619
D)0.67619






Ans - C) 1.67619


8) How many number of arguments can a destructor of a class receives?

A)0
B)1
C)2
D)None of the above.


Answer : A



9)
        #include <iostream>
        using namespace std;
        int main()
        {
            int x = -1;
            try 
            {
                if (x < 0)
                {
                    throw x;
                }
                else
                {
                    cout<<x;
                }
            }
            catch (int x )
            {
                cout << "Exception occurred: Thrown value is " << x << endl;
            }
            return 0;
        }

a) -1
b) 0
c) Exception occurred: Thrown value is -1
d) Error

Answer: c

10)
        #include <iostream>
        using namespace std; 
        int main()
        {
            int x = -1;
            char *ptr;
            ptr = new char[256];
            try 
            {
                if (x < 0)
                {
                    throw x;
                }
                if (ptr == NULL)
                {
                    throw " ptr is NULL ";
                }
            }
            catch (...) 
            {
                cout << "Exception occurred: exiting "<< endl;
            }
            return 0;
        }


a) -1
b) ptr is NULL
c) exception occured: exiting
d) 1


Answer: c


11)
#include<stdio.h>
int main() {
printf("\n %d %d %d ", sizeof('1'),sizeof("1"),sizeof(1));
return 0;
}


a)1 1 1
b)4 2 4
c)4 4 4
d)1 4 1


ans- b

12)
#include<stdio.h>
void main()
{
  int i=-1, j=-1, k=-1, l=2, m;
  m = i++ || l++ ;
  printf(" %d ", m);
}

a)0
b)1
c)2
d)-2


ans- b


13)
#include<stdio.h>
#define defMethod(i) (i*i)

void main()
{
int a,b=5;
a=defMethod(b+5);
printf("\n%d",a);
}

a)100
b)25
c)35
d)45


ans- c


14)

#include<stdio.h>

void show();
int main() {
show();
show();
}

void show() {
	auto int i =0;
	register int j=0;
	static int k;
	i++;
	j++;
	k++;
	printf("\n %d %d %d ", i,j,k);
	}

a)
1 1 1
1 1 2

b)
1 1 1
1 1 1

c)
1 1 2
1 1 2

d)
1 2 2
1 2 2


ans-a 
1 1 1
1 1 2


15)
#include<stdio.h>
int main() {
	int i = 3;
	switch(i) {
	default : printf("zero");
	case 1 : printf("one"); break;
	case 2 : printf("two"); break;
	case 3 : printf("three") ; break;
}
return 0;
}

a)compile time error
b)runtime error
c)three
d)zero



ans- c



16)

A JavaBeans component has the following field:

 private boolean enabled;

Which two pairs of method declarations follow the JavaBeans standard for accessing this field? (Choose two.)

A. public void setEnabled( boolean enabled )
     public boolean getEnabled()

B. public void setEnabled( boolean enabled )
    public void isEnabled()

C. public void setEnabled( boolean enabled )
    public boolean isEnabled()

D. public boolean setEnabled( boolean enabled )
    public boolean getEnabled()                          
 

Answer: A, C




17)

Given:

1. import java.util.*;
2. public class Old {
3. public static Object get0(List list) {
4. return list.get(0);
5. }
6. }

Which three will compile successfully? (Choose three.)

A. Object o = Old.get0(new LinkedList());
B. Object o = Old.get0(new LinkedList<?>());
C. String s = Old.get0(new LinkedList<String>());
D. Object o = Old.get0(new LinkedList<Object>());
E. String s = (String)Old.get0(new LinkedList<String>());

Answer: A, D, E




18)

1. public class Threads3 implements Runnable {
2. public void run() {
3. System.out.print("running");
4. }
5. public static void main(String[] args) {
6. Thread t = new Thread(new Threads3());
7. t.run();
8. t.run();
9. t.start();
10. }
11. }

What is the result?
A. Compilation fails.
B. An exception is thrown at runtime.
C. The code executes and prints "running".
D. The code executes and prints "runningrunning".
E. The code executes and prints "runningrunningrunning".

Answer: E




19)


10. public class Bar {
11. static void foo( int... x ) {
12. // insert code here
13. }
14. }

Which two code fragments, inserted independently at line 12, will allow the class to compile? (Choose two.)

A. foreach( x ) System.out.println(z);
B. for( int z : x ) System.out.println(z);
C. while( x.hasNext() ) System.out.println( x.next() );
D. for( int i=0; i< x.length; i++ ) System.out.println(x[i]);

Answer: B, D



20)
Given:

25. int x = 12;
26. while (x < 10) {
27. x--;
28. }
29. System.out.print(x);

What is the result?
A. 0
B. 10
C. 12
D. Line 29 will never be reached.
Answer: C

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/19th%2BMay%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/19th+May+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
