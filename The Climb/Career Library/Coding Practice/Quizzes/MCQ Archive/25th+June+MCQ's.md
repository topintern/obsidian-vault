---
kind: "study-reference"
title: "25th+June+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/25th+June+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 25th+June+MCQ's

[[The Climb/Career Library/Career Library]]


1) output of the following C Code

#include <stdio.h> 
int var = 20; 
int main() 
{ 
    int var = var; 
    printf("%d ", var); 
    return 0; 
} 

(A) Garbage Value/0
(B) 20
(C) Compiler Error
(D) Segmentation fault
(E) None of these
















Answer: (A)

Explanation:
First var is declared, then value is assigned to it. 
As soon as var is declared as a local variable, it hides the global variable var.






2)
Output of the following C Code

#include <stdio.h> 
  
int main() 
{ 
    float arr[5] = {12.5, 10.0, 13.5, 90.5, 0.5}; 
    float *ptr1 = &arr[0]; 
    float *ptr2 = ptr1 + 3; 
  
    printf("%f ", *ptr2); 
    printf("%d", ptr2 - ptr1); 
  
   return 0; 
} 

(A) 
90.500000
3

(B) 
90.500000
12

(C)
10.000000
12

(D)
0.500000
3





Answer: (A)


Explanation: 

When we add a value x to a pointer p, the value of the resultant expression is 
p + x*sizeof(*p) where sizeof(*p) means size of data type pointed by p. 
That is why ptr2 is incremented to point to arr[3] in the above code. 
Same rule applies for subtraction. Note that only integral values can be added 
or subtracted from a pointer. 
We can also subtract or compare two pointers of same type.

3)
Output of the following C Code

#include <stdio.h> 
char str1[100]; 
  
char *fun(char str[]) 
{ 
    static int i = 0; 
    if (*str) 
    { 
        fun(str+1); 
        str1[i] = *str; 
        i++; 
    } 
    return str1; 
} 
  
int main() 
{ 
    char str[] = "C was Developed by Dennis"; 
    printf("%s", fun(str)); 
    return 0; 
}

(A) C was Developed by Dennis
(B) sinneD yb depoleveD saw C
(C) Nothing is printed on screen
(D) Segmentation Fault




Answer: (B)

Explanation: The function basically reverses the given string.

4)
Output of the following C Code

#include <stdio.h>

int main()
{
    printf(6+"Hello World");
    return 0;
}


(A) Hello World
(B) 6 Hello World
(C) Hello World 6
(D) World
(E) Hello
(F) Compilation fails






Ans - D




5)
Output of the following C Code

#include <stdio.h>

int i=3;
void  main(int k)
{
   if(i==0)
   {
   k=0;
   return;
   }
   else
   {
   k=i;
   k--;
   main(--i);
   }
   printf(" %d ", k);
}


(A) 2 1 
(B) 2 1 0
(C) 0 1 2
(D) 0
(E) Compilation fails





Ans - C





6)
Output of the following C Code
Assume the size of integer is 4 bytes 

#include <stdio.h>
struct bits
{
    int i : 10;
    int j : 20;
}b;

int  main()
{
   printf(" %ld ", sizeof(b));
    return 1;    
}


(A) 8
(B) 30
(C) 120
(D) 4




Ans - D

7) Assume a class D that is privately derived from class B. 

Which of the following can an object of class D located in main() access ?

A) Public Members of D
B) Protected Members of D
C) Private Members of D
D) public Members of B
E) Protected Members of B
F) private members of B




 Answer -A

Only the public members of the class D are accessible through an object of 
class D from main().

8)
what is the output of the following cpp code
#include <iostream>
using namespace std;

int top =3; 
class base 
{
protected: 
  int top; 
public: 
   base() 
   {  
    top=2;
    cout<<top<<" "; 
    }
};

class derived :public base
{
   private :
      int top;
    public :
        derived():base()
         {
	top=1;
	cout<<top<<" ";
	cout<<base::top<<" ";
	cout<<::top<<" ";
          }
};
int main()
{
 derived d1;
return 1;
    
}


A) 2 1 2 3
B) 1 2 3 2
C) 2 2 1 2
D) None of these



Answer–A

When the object d1 is created, the constructor of the class base gets called 
which prints the value of the data member top, which is 2. 
Then the derived class constructor gets executed it prints the value of data 
member top declared in the derived class, which is 1. 
The base::top refers to the data member top of the class base and hence prints 2. 
Finally value of the global variable top gets printed which is 3.

9) 
output of the following cpp code

#include <iostream>
using namespace std;

void fun(int i)
{ 
    cout<<i+10;
}

void fun(int &i)
{
cout<<i+20;
}

int main()
{
  int i=40;
  fun(i);
  return 1;
}


(A) 50
(B) 60
(C) 40
(D) Compilation fails 



Ans- D

10) Are the following two sets of statements same in CPP:

Assume  sample is a class and s1 and s2 are objects 

sample s1;
s1=s2;

and

sample s1=s2;


A) Same
B) Not Same
C) Depends on the Compiler
D) None of these


Ans: B 

In the first set, s1 gets created. 
Then s1 is assigned a value of s2 through an assignment operator.

In the second set, s1 gets created. 
Then s1 is initialized with a value of s2 through the copy constructor.

11)
#include<iostream>
using namespace std;

class A
{
public:
A()
{ 
cout<<"A Constructor "; }
};
class B
{
public:
B()
{
cout<<"B Constructor "; }
};
class C:public B,virtual public A
{
public:
C()
{ 
cout<<"C Constructor "; }
};
int main()
{
C a;
return 1;
}

(A)   Illegal to specify virtual in derivation of class
(B)    A Constructor	B Constructor	C Constructor
(C)	B Constructor	A Constructor C Constructor
(D)   None of these




Ans- B

12)

#include<iostream>
using namespace std;

class Test { 	
int rno; 
public: 
static void setDetails(int rno) 
{ 	
this->rno=rno;
}
void dispDetails() 
{ 
cout<<rno; 
}
}; 
int main() 
{ 
Test t;
Test::setDetails(10);
t.dispDetails(); 
return 1;
}


A) Displays Garbage Value
B) Displays 10
C) Compilation Error
D) None of these




Ans- C



13)
Each time a defect gets detected and fixed, the reliability of a software product

(A)increases. 
(B) decreases.
(C) remains constant.
(D) cannot say anything.




Ans- (B)

14)

Given:
3. import java.io.*;
4. public class Talker {
5. public static void main(String[] args) {
6. Console c = System.console();
7. String u = c.readLine("%s", "username: ");
8. System.out.println("hello " + u);
9. String pw;
10. if(c != null && (pw = c.readPassword("%s", "password: ")) != null)
11. // check for valid password
12. }
13. }

If line 6 creates a valid Console object, and if the user enters fred as a username and 1234 as a
password, what is the result? (Choose all that apply.)

A. username:
password:
B. username: fred
password:
C. username: fred
password: 1234
D. Compilation fails
E. An exception is thrown at runtime



Answer:
D is correct. 

The readPassword() method returns a char[]. 
If a char[] were used, answer B would be correct.




15)
Given:

3. import java.io.*;
4. class Vehicle { }
5. class Wheels { }
6. class Car extends Vehicle implements Serializable { }
7. class Ford extends Car { }
8. class Dodge extends Car {
9. Wheels w = new Wheels();
10. }

Instances of which class(es) can be serialized? (Choose all that apply.)
A. Car
B. Ford
C. Dodge
D. Wheels
E. Vehicle





Answer:
A and B are correct. 

Dodge instances cannot be serialized because they "have" an instance of Wheels,
which is not serializable. 
Vehicle instances cannot be serialized even though the subclass Car can be.

16)
Given:

3. import java.text.*;
4. public class Slice {
5. public static void main(String[] args) {
6. String s = "987.123456";
7. double d = 987.123456d;
8. NumberFormat nf = NumberFormat.getInstance();
9. nf.setMaximumFractionDigits(5);
10. System.out.println(nf.format(d) + " ");
11. try {
12. System.out.println(nf.parse(s));
13. } catch (Exception e) { System.out.println("got exc"); }
14. }
15. }

Which are true? (Choose all that apply.)
A. The output is 987.12345 987.12345
B. The output is 987.12346 987.12345
C. The output is 987.12345 987.123456
D. The output is 987.12346 987.123456
E. The try/catch block is unnecessary
F. The code compiles and runs without exception
G. The invocation of parse() must be placed within a try/catch block


Answer:
D, F, and G are correct. 

The setMaximumFractionDigits() applies to the formatting but not the parsing. 
The try/catch block is placed appropriately. 

17)

3. import java.util.*;
4. public class Looking {
5. public static void main(String[] args) {
6. String input = "1 2 a 3 45 6";
7. Scanner sc = new Scanner(input);
8. int x = 0;
9. do {
10. x = sc.nextInt();
11. System.out.print(x + " ");
12. } while (x!=0);
13. }
14. }

What is the result?
A. 1 2
B. 1 2 3 45 6
C. 1 2 3 4 5 6
D. 1 2 a 3 45 6
E. Compilation fails
F. 1 2 followed by an exception




Answer:
F is correct. 
The nextXxx() methods are typically invoked after a call to a hasNextXxx(), 
which determines whether the next token is of the correct type.


18) Given:

public static void main(String[] args) {
// INSERT DECLARATION HERE
for (int i = 0; i <= 10; i++) {
List<Integer> row = new ArrayList<Integer>();
for (int j = 0; j <= 10; j++)
row.add(i * j);
table.add(row);
}
for (List<Integer> row : table)
System.out.println(row);
}

Which statements could be inserted at // INSERT DECLARATION HERE to allow this code to compile and run? (Choose all that apply.)

A. List<List<Integer>> table = new List<List<Integer>>();
B. List<List<Integer>> table = new ArrayList<List<Integer>>();
C. List<List<Integer>> table = new ArrayList<ArrayList<Integer>>();
D. List<List, Integer> table = new List<List, Integer>();
E. List<List, Integer> table = new ArrayList<List, Integer>();
F. List<List, Integer> table = new ArrayList<ArrayList, Integer>();
G. None of the above

Answer:
B is correct.

A is incorrect because List is an interface, so you can't say new List() 
regardless of any generic types. 
D, E, and F are incorrect because List only takes one type parameter 
(a Map would take two, not a List). 
C is tempting, but incorrect. 
The type argument <List<Integer>> must be the same for both sides of the assignment, 
even though the constructor new ArrayList() on the right side is a subtype of 
the declared type List on the left.



19)

Which statements are true about comparing two instances of the same class, given that the
equals() and hashCode() methods have been properly overridden? (Choose all that apply.)

A. If the equals() method returns true, the hashCode() comparison == might return false
B. If the equals() method returns false, the hashCode() comparison == might return true
C. If the hashCode() comparison == returns true, the equals() method must return true
D. If the hashCode() comparison == returns true, the equals() method might return true
E. If the hashCode() comparison != returns true, the equals() method might return true


Answer:
B and D. 
B is true because often two dissimilar objects can return the same hashcode value. 
D is true because if the hashCode() comparison returns ==, the two objects might
or might not be equal.

A, C, and E are incorrect. 
C is incorrect because the hashCode() method is very flexible in its return values, 
and often two dissimilar objects can return the same hash code value.
A and E are a negation of the hashCode() and equals() contract. 

20)

Given:
public static void before() {
Set set = new TreeSet();
set.add("2");
set.add(3);
set.add("1");
Iterator it = set.iterator();
while (it.hasNext())
System.out.print(it.next() + " ");
}
Which statements are true?
A. The before() method will print 1 2
B. The before() method will print 1 2 3
C. The before() method will print three numbers, but the order cannot be determined
D. The before() method will not compile
E. The before() method will throw an exception at runtime




Answer:
E is correct. 

You can't put both Strings and ints into the same TreeSet. 
Without generics, the compiler has no way of knowing what type is appropriate 
for this TreeSet, so it allows everything to compile. 
At runtime, the TreeSet will try to sort the elements as they're added, and when
it tries to compare an Integer with a String it will throw a ClassCastException. 
Note that although the before() method does not use generics, it does use autoboxing. 


## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/25th%2BJune%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/25th+June+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
