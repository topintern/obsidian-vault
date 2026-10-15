---
kind: "study-reference"
title: "22nd+June+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/22nd+June+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 22nd+June+MCQ's

[[The Climb/Career Library/Career Library]]

1)

what is the output of the below C code 

#include<stdio.h>
#include<string.h>

int main() 
{ 
    char p[] = "helloworld"; 
    char t; 
    int i, j; 
    for(i=0,j=strlen(p)-1; i<j; i++) 
    { 
        t = p[i]; 
        p[i] = p[j-i]; 
        p[j-i] = t; 
    } 
    printf("%s", p); 
    return 0; 
} 

(A) dlrowolleh
(B) Nothing is printed on the screen
(C) helloworld
(D) Segmentation fault
(E) delloworlh








Answer: (E)

2)
Output of the following C Code

#include<stdio.h> 
int main() 
{ 
    float x = 0.1; 
    if ( x == 0.1 ) 
        printf("IF"); 
    else if (x == 0.1f) 
        printf("ELSE IF"); 
    else
        printf("ELSE"); 
} 

(A) ELSE IF
(B) IF
(C) ELSE
(D) Compilation fails






Answer: (A)
Explanation:

in if(x==0.1) 0.1 is taken as double and 0.1f is considered as float since f is specified. 
hence it gives ELSEIF as output


3) Output of the following C Code
#include<stdio.h> 
  
void dynamic(int s, ...) 
{ 
    printf("%d ", s); 
} 
  
int main() 
{ 
    dynamic(2, 4, 6, 8); 
    dynamic(3, 6, 9); 
    return 0; 
} 

(A) 2 3
(B) Compiler Error
(C) 4 3
(D) 3 2




Answer: (A)

Explanation: 

In c three continuous dots is known as ellipsis which is variable number of arguments of function. 
The values to parameters are assigned one by one.


4) Output of the following C Code

#include<stdio.h> 
int main() 
{ 
  typedef int *i; 
  int j = 10; 
  i *a = &j; 
  printf("%d", **a); 
  return 0; 
} 

(A) Compiler Error
(B) Garbage Value
(C) 10
(D) 0







Answer: (A)

Explanation: 

Compiler Error -> Initialization with incompatible pointer type.
The line typedef int *i makes i as type int *. 
So, the declaration of a means a is pointer to a pointer.


5)

In _______, the bodies of the two loops are merged together to form a single
loop provided that they do not make any references to each other.

(A) Loop unrolling
(B) Strength reduction
(C) Loop concatenation
(D) Loop jamming






Answer: (D)

Explanation:

In loop jamming, the bodies of the two loops are merged together to form a
single loop provided that they do not make any references to each other.

In loop concatenation, the bodies of the two loops are concatenated together to
form a series of loop, loop concatenation, some times help to reduce complexity.

In loop unrolling, we try to optimize a program’s execution speed. It is also
known as space–time tradeoff.

In strength reduction compiler optimize expensive operations with equivalent but
less expensive operations.

So, option (D) is correct.

6)
Output of the following C Code

# include <stdio.h> 
int main() 
{ 
   int i = 0; 
   for (i=0; i<20; i++) 
   { 
     switch(i) 
     { 
       case 0: 
         i += 5; 
       case 1: 
         i += 2; 
       case 5: 
         i += 5; 
       default: 
         i += 4; 
         break; 
     } 
     printf("%d  ", i); 
   } 
   return 0; 
} 

(A) 5 10 15 20
(B) 7 12 17 22
(C) 16 21
(D) Compiler Error





Answer: (C)

Explanation:

Initially i = 0. 
Since case 0 is true i becomes 5, and since there is no break statement till last statement of switch block, i becomes 16.
Now in next iteration no case is true, so execution goes to default and i becomes 21.

7)Consider the C function given below.


int f(int j) 
{ 
  static int i = 50; 
  int k; 
  if (i == j) 
  { 
    printf(“something”); 
    k = f(i); 
    return 0; 
  } 
  else return 0; 
} 

Which one of the following is TRUE?

(A) The function returns 0 for all values of j.
(B) The function prints the string something for all values of j.
(C) The function returns 0 when j = 50.
(D) The function will exhaust the runtime stack or run into an infinite loop when j = 50




Answer: (D)

Explanation: 

When j is 50, the function would call itself again and again as neither i nor j is changed inside the recursion.


8) What is the output of the following C Code

#include<stdio.h> 
void crazy(int n,int a,int b) 
{ 
    if (n <= 0)  return; 
    crazy(n-1, a, b+n); 
    printf("%d %d %d\n",n,a,b); 
    crazy(n-1, b, a+n); 
} 
  
int main() 
{ 
    crazy(3,4,5); 
    return 0; 
} 

(A)

1 4 10
2 4 8
1 8 6
3 4 5
1 5 9
2 5 7
1 7 7

(B)

3 4 5
1 4 10
2 4 8
1 8 6
1 5 9
2 5 7
1 7 7

(C)

1 4 10
2 4 8
1 8 6
3 4 5

(D)

3 4 5
1 5 9
2 5 7
1 7 7




Answer: (A)

9) Output of the following CPP Code

#include<iostream> 
using namespace std; 
  
class Base { 
private: 
     int i, j; 
public: 
    Base(int _i = 0, int _j = 0): i(_i), j(_j) { } 
}; 
class Derived: public Base { 
public: 
     void show(){ 
        cout<<" i = "<<i<<"  j = "<<j; 
     } 
}; 
int main(void) { 
  Derived d; 
  d.show(); 
  return 0; 
} 

(A) i = 0 j = 0
(B) Compiler Error: i and j are private in Base
(C) Compiler Error: Could not call constructor of Base
(D) None of these




Answer: (B)

10) #include <iostream> 
using namespace std; 
  
int main() 
{ 
    try  { 
       throw "10"; 
    } 
    catch (char *excp)  { 
        cout << "Caught " << excp; 
    } 
    catch (...)  { 
        cout << "Default Exception\n"; 
    } 
    return 0; 
}


A) Caught 10
B) Default Exception
C) Compilation fails
D) Segmentation fault




Ans - B


11)Consider the below C++ program.

#include<iostream> 
using namespace std; 

class A 
{ 
public: 
     A(){ cout <<"1";} 
     A(const A &obj){ cout <<"2";} 
};   
class B: virtual A 
{ 
public: 
    B(){cout <<"3";} 
    B(const B & obj){cout<<"4";} 
};   
class C: virtual A 
{ 
public: 
   C(){cout<<"5";} 
   C(const C & obj){cout <<"6";} 
}; 
  
class D:B,C 
{ 
public: 
    D(){cout<<"7";} 
    D(const D & obj){cout <<"8";} 
}; 
  
int main() 
{ 
   D d1; 
   D d(d1); 
}

Which of the below is not printed?


(A) 2
(B) 4
(C) 6
(D) All of these are not printed




Answer: (D)

Explanation: 

Output will be 13571358 as 1357 (for D d1) and 

as 1358 (for D d(d1))……reason is that ……during inheritance we need to explicitly call copy constructor of base class otherwise only default constructor of base class is called. 

One more thing, as we are using virtual before base class, there will be only one copy of base class in multiple inheritance. 

And without virtual output will be……13157….&…13158 as (1315713158) respectively for each derived class object.

12) #include<iostream> 
using namespace std; 
  
class Base1 
{ 
public: 
    char c; 
}; 
  
class Base2 
{ 
public: 
    int c; 
}; 
  
class Derived: public Base1, public Base2 
{ 
public: 
    void show()  { cout << c; } 
}; 
  
int main(void) 
{ 
    Derived d; 
    d.show(); 
    return 0; 
} 

(A) Compiler Error in “cout << c;"
(B) Garbage Value
(C) Compiler Error in “class Derived: public Base1, public Base2”
(D) None of these




Answer: (A)

Explanation: 

The variable ‘c’ is present in both super classes of Derived. 
So the access to ‘c’ is ambiguous. 
The ambiguity can be removed by using scope resolution operator. 




13) Given:
import java.io.*;
class Player {
Player() { System.out.print("p"); }
}
class CardPlayer extends Player implements Serializable {
CardPlayer() { System.out.print("c"); }
public static void main(String[] args) {
CardPlayer c1 = new CardPlayer();
try {
FileOutputStream fos = new FileOutputStream("play.txt");
ObjectOutputStream os = new ObjectOutputStream(fos);
os.writeObject(c1);
os.close();
FileInputStream fis = new FileInputStream("play.txt");
ObjectInputStream is = new ObjectInputStream(fis);
CardPlayer c2 = (CardPlayer) is.readObject();
is.close();
} catch (Exception x ) { }
}
}

What is the result?
A. pc
B. pcc
C. pcp
D. pcpc
E. Compilation fails
F. An exception is thrown at runtime

Answer:

C is correct. 

It's okay for a class to implement Serializable even if its superclass doesn't.
However, when you deserialize such an object, the non-serializable superclass must run its constructor. 
Remember, constructors don't run on deserialized classes that implement Serializable.


14) Given:
class TKO {
public static void main(String[] args) {
String s = "-";
Integer x = 343;
long L343 = 343L;
if(x.equals(L343)) s += ".e1 ";
if(x.equals(343)) s += ".e2 ";
Short s1 = (short)((new Short((short)343)) / (new Short((short)49)));
if(s1 == 7) s += "=s ";
if(s1 < new Integer(7+1)) s += "fly ";
System.out.println(s);
} }

Which of the following will be included in the output String s? (Choose all that apply.)

A.	.e1
B.	.e2
C.	=s
D.	fly
E.	None of the above
F.	Compilation fails
G.	An exception is thrown at runtime



Answer:
B, C, and D are correct. 

Remember, that the equals() method for the integer wrappers will only return true if the two primitive types and the two values are equal. 
With C, it's okay to unbox and use ==. 
For D, it's okay to create a wrapper object with an expression, and unbox it for comparison with a primitive.




15) Given:

import java.io.*;
class Keyboard { }
public class Computer implements Serializable {
private Keyboard k = new Keyboard();
public static void main(String[] args) {
Computer c = new Computer();
c.storeIt(c);
}
void storeIt(Computer c) {
try {
ObjectOutputStream os = new ObjectOutputStream(
new FileOutputStream("myFile"));
os.writeObject(c);
os.close();
System.out.println("done");
} catch (Exception x) {System.out.println("exc"); }
}
}

What is the result? (Choose all that apply.)

A. exc
B. done
C. Compilation fails
D. Exactly one object is serialized
E. Exactly two objects are serialized



Answer:
A is correct.
An instance of type Computer Has-a Keyboard. Because Keyboard doesn't implement Serializable, 
any attempt to serialize an instance of Computer will cause an exception to be thrown.

16) Given:

import java.io.*;
public class TestSer {
public static void main(String[] args) {
SpecialSerial s = new SpecialSerial();
try {
ObjectOutputStream os = new ObjectOutputStream(
new FileOutputStream("myFile"));
os.writeObject(s); os.close();
System.out.print(++s.z + " ");
ObjectInputStream is = new ObjectInputStream(
new FileInputStream("myFile"));
SpecialSerial s2 = (SpecialSerial)is.readObject();
is.close();
System.out.println(s2.y + " " + s2.z);
} catch (Exception x) {System.out.println("exc"); }
}
}

class SpecialSerial implements Serializable {
transient int y = 7;
static int z = 9;
}
Which are true? (Choose all that apply.)

A. Compilation fails
B. The output is 10 0 9
C. The output is 10 0 10
D. The output is 10 7 9
E. The output is 10 7 10
F. In order to alter the standard deserialization process you would implement the
readObject() method in SpecialSerial
G. In order to alter the standard deserialization process you would implement the
defaultReadObject() method in SpecialSerial







Answer:
C and F are correct. 

C is correct because static and transient variables are not serialized when an object is serialized. 
F is a valid statement.



17) Given:
3. public class Theory {
4. public static void main(String[] args) {
5. String s1 = "abc";
6. String s2 = s1;
7. s1 += "d";
8. System.out.println(s1 + " " + s2 + " " + (s1==s2));
9.
10. StringBuffer sb1 = new StringBuffer("abc");
11. StringBuffer sb2 = sb1;
12. sb1.append("d");
13. System.out.println(sb1 + " " + sb2 + " " + (sb1==sb2));
14. }
15. }

Which are true? (Choose all that apply.)
A. Compilation fails
B. The first line of output is abc abc true
C. The first line of output is abc abc false
D. The first line of output is abcd abc false
E. The second line of output is abcd abc false
F. The second line of output is abcd abcd true
G. The second line of output is abcd abcd false




Answer:
D and F are correct. 

While String objects are immutable, references to Strings are mutable.
The code s1 += "d"; creates a new String object. 
StringBuffer objects are mutable, so the append() is changing the single StringBuffer object to which both StringBuffer references refer.

18) Given:
3. import java.io.*;
4. public class ReadingFor {
5. public static void main(String[] args) {
6. String s;
7. try {
8. FileReader fr = new FileReader("myfile.txt");
9. BufferedReader br = new BufferedReader(fr);
10. while((s = br.readLine()) != null)
11. System.out.println(s);
12. br.flush();
13. } catch (IOException e) { System.out.println("io error"); }
16. }
17. }

And given that myfile.txt contains the following two lines of data:
ab
cd

What is the result?

A. ab

B. abcd

C. ab
cd

D. a
b
c
d

E. Compilation fails




Answer:
E is correct. 
You need to call flush() only when you're writing data. 
Readers don't have flush() methods. 
If not for the call to flush(), answer C would be correct.


19)The following table has two attributes A and C where A is the primary key and C is the foreign key referencing A with on-delete cascade.

A   C
-----
2   4
3   4
4   3
5   2
7   2
9   5
6   4

The set of all tuples that must be additionally deleted to preserve referential integrity when the tuple (2,4) is deleted is:
(a) (3,4) and (6,4)
(b) (5,2) and (7,2)
(c) (5,2), (7,2) and (9,5)
(d) (3,4), (4,3) and (6,4)




Answer (C)
When (2,4) is deleted. 
Since C is a foreign key referring A with delete on cascade, all entries with value 2 in C must be deleted. 
So (5, 2) and (7, 2) are deleted. 
As a result of this 5 and 7 are deleted from A which causes (9, 5) to be deleted.

20) The relation book (title, price) contains the titles and prices of different
books. 
Assuming that no two books have the same price, what does the following SQL
query list?

  select title
  from book as B
  where (select count(*)
     from book as T
     where T.price > B.price) < 5

(a) Titles of the four most expensive books
(b) Title of the fifth most inexpensive book
(c) Title of the fifth most expensive book
(d) Titles of the five most expensive books




Answer (d)

When a subquery uses values from outer query, the subquery is called correlated subquery. 
The correlated subquery is evaluated once for each row processed by the outer query.
The outer query selects all titles from book table. 
For every selected book, the subquery returns count of those books which are more expensive than the selected book.
The where clause of outer query will be true for 5 most expensive book. 
For example count (*) will be 0 for the most expensive book and count(*) will be 1 for second most expensive book.

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/22nd%2BJune%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/22nd+June+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
