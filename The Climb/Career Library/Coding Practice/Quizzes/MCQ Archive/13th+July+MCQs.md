---
kind: "study-reference"
title: "13th+July+MCQs"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/13th+July+MCQs.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 13th+July+MCQs

[[The Climb/Career Library/Career Library]]

1) Which of the following is correct about err used in the declaration given below ?

typedef enum error { warning, test, exception } err;

A) It is a typedef for enum error
B) It is a variable of type enum error
C) The statement is erroneous
D) It is a structure
E) It is one of the elements of enum error























Ans- A

2) which of the following statement should be used to obtain a remainder after 
dividing 3.14 by 2.1 ?

A) rem=3.14%2.1;
B) rem = modf(3.14,2.1);
C) rem = fmod(3.14,2.1);
D) rem = 3.14 mod 2.1 
E) we cannot obtain the remainder in floating point division 












Ans- C

3) 
what will be the output of the following program?

#include<stdio.h>
int main() {
int i = 4;
switch(i) 
{
default :
	printf(" apple ");
case 1 : printf(" orange "); break;
case 2 : printf(" grapes "); break;
case 3 : printf(" mango "); 
}
return 0;
}

A) apple orange
B) apple
C) Compilation fails
D) None of these







Ans- A

4)
#include<stdio.h>
int main() {
int i = 1;
for( ; ;) 
{
     printf(" %d ", i++);
     if(i > 10)  break;
    
}
return 0;
}

A) There should be a condition in the for loop
B) The two semicolons should be removed
C) The for loop should be replaced by a while loop
D) No error




Ans - D

5) What will be the output of the following C Program
the array begins at the location 1008 

#include<stdio.h>
int main() {
int a[2][3][4] = { {19,2,3,4},{5,6,7,8},{9,1,1,2},{2,1,4,7},{6,7,8,9},{9,8,7,6}};

printf(" %d %d %d %d", a,*a,**a,***a);
return 0;
}

A) 1008 1008 1008 1008
B) 19 19 19 19
C) 1008 19 19 19
D) Compilation fails
E) 1008 1008 1008 19 




Ans- E

6) #include<iostream>
using namespace std;

int main(){
int a=5,b=6,c=7,d=8;
int *pa,*pb,*pc,*pd;
pa=&a;
pb=&b;
pc=&c;
pd=&d;
int *arr[]={pa,pb,pc,pd};
for(int i=0;i<4;i++)
  cout<<*arr[i]<<" ";
}

A) Compilation fails
B) Segmentation fault
C) 5 6 7 8
D) 4 Address gets printed 




Ans - C

7) #include<iostream>
using namespace std;

int main(){
  bool x(true);
  std::cout<<x;
}

A) true
B) 1
C) compilation error
D) Segmentation fault




Ans- B

8) #include<iostream>
using namespace std;

class Student
{
    public:
    int age;
    int rno;
    Student(int age,int rno)
    {
        this->age= age;
        this->rno = rno;
    }
    void change()
    {
        age = 40;
        rno = 80;
    }
};

int main(){
  const Student s(10,15);
  s.change();
  std::cout<<s.age<<" "<<s.rno;
}

A) Compilation fails
B) 10 15
C) 40 80
D) Segmentation fault



Ans- A

9) #include<iostream>
using namespace std;

class index
{
    public:
    index() { count = 0; }
    index(int c) { count = c; }
    
    protected :
    int count;
    public:
    void display() {
        std::cout<<count<<" ";
    }
    void operator ++() {
       count++;
    }
};

class index1 : public index{
  public :
    void operator --(){
        count--;
    }    
};

int main(){
    index1 i;
    ++i;
    ++i;
    i.display();
    --i;
    i.display();
    return 0;
}

A) 2 1
B) 2 2 
C) Compilation error
D) Segmentation fault



Ans- A

10) #include<iostream>
using namespace std;

class base
{
    public:
    virtual void disp(){
        cout<<"\nin base :: disp ";
    }
};

class derived1 : virtual public base
{
    public:
    virtual void disp(){
        cout<<"\nin derived1 :: disp ";
    }
};

class derived2 : virtual public base
{
    public:
    virtual void disp(){
        cout<<"\nin derived2 :: disp ";
    }
};

class derived3 : public derived1 ,  public derived2
{
    public:
     void disp(){
        cout<<"\nin derived3 :: disp ";
        derived1::disp();
    }
};

int main(){
    base *b;
    derived1 d1;
     b = &d1;
     b->disp();
     
     derived2 d2;
     b=&d2;
     b->disp();
     
     derived3 d3;
     b=&d3;
     b->disp();
    return 0;
}

A) 
in derived1 :: disp                                                                                                                  
in derived3 :: disp                                                                                                                  
in derived2 :: disp                                                                                                                  
in derived3 :: disp  

B) 
in derived1 :: disp                                                                                                                  
in derived2 :: disp                                                                                                                  
in derived3 :: disp                                                                                                                  
in derived1 :: disp  

C)  Compilation fails

D) Segmentation fault




Ans- B

11) Given:
3. import java.util.*;
4. class Dog { int size; Dog(int s) { size = s; } }
5. public class FirstGrade {
6. public static void main(String[] args) {
7. TreeSet<Integer> i = new TreeSet<Integer>();
8. TreeSet<Dog> d = new TreeSet<Dog>();
9.
10. d.add(new Dog(1)); d.add(new Dog(2)); d.add(new Dog(1));
11. i.add(1); i.add(2); i.add(1);
12. System.out.println(d.size() + " " + i.size());
13. }
14. }

What is the result?
A. 1 2
B. 2 2
C. 2 3
D. 3 2
E. 3 3
F. Compilation fails
G. An exception is thrown at runtime





Answer:
 G is correct. 
 Class Dog needs to implement Comparable in order for a TreeSet 
 (which keeps its elements sorted) to be able to contain Dog objects.

12) Given:
3. import java.util.*;
4. public class GeoCache {
5. public static void main(String[] args) {
6. String[] s = {"map", "pen", "marble", "key"};
7. Othello o = new Othello();
8. Arrays.sort(s,o);
9. for(String s2: s) System.out.print(s2 + " ");
10. System.out.println(Arrays.binarySearch(s, "map"));
11. }
12. static class Othello implements Comparator<String> {
13. public int compare(String a, String b) { return b.compareTo(a); }
14. }
15. }

Which are true? (Choose all that apply.)
A. Compilation fails
B. The output will contain a 1
C. The output will contain a 2
D. The output will contain a –1
E. An exception is thrown at runtime
F. The output will contain "key map marble pen"
G. The output will contain "pen marble map key"




Answer: D and G are correct. 

First, the compareTo() method will reverse the normal sort.
Second, the sort() is valid. 
Third, the binarySearch() gives –1 because it needs to be invoked using the 
same Comparator (o), as was used to sort the array. 

13) Given:
1. // insert code here
2. class StatTest {
3. public static void main(String[] args) {
4. System.out.println(Integer.MAX_VALUE);
5. }
6. }

Which, inserted independently at line 1, compiles? (Choose all that apply.)

A. import static java.lang;
B. import static java.lang.Integer;
C. import static java.lang.Integer.*;
D. import static java.lang.Integer.*_VALUE;
E. import static java.lang.Integer.MAX_VALUE;
F. None of the above statements are valid import syntax




Answer:
C and E are correct syntax for static imports. 
Line 4 isn't making use of static imports, so the code will also compile with none of the imports.

14) Given:
3. public class Leader implements Runnable {
4. public static void main(String[] args) {
5. Thread t = new Thread(new Leader());
6. t.start();
7. System.out.print("m1 ");
8. t.join();
9. System.out.print("m2 ");
10. }
11. public void run() {
12. System.out.print("r1 ");
13. System.out.print("r2 ");
14. }
15. }

Which are true? (Choose all that apply.)
A. Compilation fails
B. The output could be r1 r2 m1 m2
C. The output could be m1 m2 r1 r2
D. The output could be m1 r1 r2 m2
E. The output could be m1 r1 m2 r2
F. An exception is thrown at runtime



Answer:
A is correct. 

The join() must be placed in a try/catch block. 
If it were, answers B and D would be correct. 
The join() causes the main thread to pause and join the end of the other thread,
meaning "m2" must come last.

15)Given:

import static java.lang.System.*;
class _ {
static public void main(String... __A_V_) {
String $ = "";
for(int x=0; ++x < __A_V_.length; )
$ += __A_V_[x];
out.println($);
}
}

And the command line:
java _ - A .

What is the result?

A. -A
B. A.
C. -A.
D. _A.
E. _-A.
F. Compilation fails
G. An exception is thrown at runtime

Answer:
B is correct. 

This question is using valid (but inappropriate and weird) identifiers, static
imports, var-args in main(), and pre-incrementing logic.

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/13th%2BJuly%2BMCQs.txt) · CODING RESOURCES/Quiz Mcqs/13th+July+MCQs.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
