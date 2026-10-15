---
kind: "study-reference"
title: "16th+July+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/16th+July+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 16th+July+MCQ's

[[The Climb/Career Library/Career Library]]

1)#include<stdio.h>

int main() {
char i=0;
for(i=5 && i >=-1;++i;i>0)
  printf(" %d\n ", i);
  printf(" \n");
  return 0;

}

A) 1 2 3 4 .... 126 127 -128 -127 ..... -2  -1
B) Compilation fails
C) compiles fine but prints nothing
D) 0 1 2 3 4 5
E) 1 2 3 4 .... 125 126 -127 -126....-1
F) None of these 















ANS- F

Explanation :- 

Prints 
 2  3  4  5  6  7  8  9  10  11  12  13  14  15  16  17  18  19  20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35  36    
37  38  39  40  41  42  43  44  45  46  47  48  49  50  51  52  53  54  55  56  57  58  59  60  61  62  63  64  65  66  67  68  69  7  
0  71  72  73  74  75  76  77  78  79  80  81  82  83  84  85  86  87  88  89  90  91  92  93  94  95  96  97  98  99  100  101  102   
 103  104  105  106  107  108  109  110  111  112  113  114  115  116  117  118  119  120  121  122  123  124  125  126  127  -128  -  
127  -126  -125  -124  -123  -122  -121  -120  -119  -118  -117  -116  -115  -114  -113  -112  -111  -110  -109  -108  -107  -106  -1  
05  -104  -103  -102  -101  -100  -99  -98  -97  -96  -95  -94  -93  -92  -91  -90  -89  -88  -87  -86  -85  -84  -83  -82  -81  -80   
 -79  -78  -77  -76  -75  -74  -73  -72  -71  -70  -69  -68  -67  -66  -65  -64  -63  -62  -61  -60  -59  -58  -57  -56  -55  -54  -5  
3  -52  -51  -50  -49  -48  -47  -46  -45  -44  -43  -42  -41  -40  -39  -38  -37  -36  -35  -34  -33  -32  -31  -30  -29  -28  -27    
-26  -25  -24  -23  -22  -21  -20  -19  -18  -17  -16  -15  -14  -13  -12  -11  -10  -9  -8  -7  -6  -5  -4  -3  -2  -1  


2) #include<stdio.h>
int main()
{
    char ch;
    if((ch=printf("")))
	    printf("if block");
    else;
      printf("else block");
}
A) if block
B) else block
C) if block else block
D) Prints Nothing
E) Compilation fails





Ans- B

3) #include<stdio.h>
int main()
{
     int i=1;
     switch(i)
     {
         printf("one");
         case 1 : printf("zero"); break;
         case 2 : printf("two"); break;
     }
}

A) zero
B) one zero
C) one
D) Compilation fails
E) None of these




Ans- A

4) 
#include<stdio.h>
#define PAT(a,b) ((a)>(b))?(a):(b);

int main()
{
  int a=10,b=5;
  int k=0;
  k=PAT(++a,b++); 
  printf(" %d %d %d ", a,b,k);
  return 0;
}




A) 12 6 12
B) 11 5 11
C) 11 5 Garbage Value
D) 12 6 Garbage Value
E) Compilation fails


Ans - A

5)If you think the following CPP code works fine and if the rno entered is 15 and marks entered is 95 what will be the output ?

#include <iostream> 
using namespace std; 
  
class Student
{ 
private: 
    int rno,marks;
public: 
    Student(int r = 0, int i =0) 
    {  
        rno = r;   marks = i; 
    } 
    friend ostream & operator << (ostream &MyCout, const Student &c); 
    friend istream & operator >> (istream &MyCin,  Student &c); 
}; 
  
ostream & operator << (ostream &MyCout, const Student &c) 
{ 
    MyCout << c.rno; 
    MyCout << " " << c.marks << endl; 
    return MyCout; 
} 
  
istream & operator >> (istream &MyCin,  Student &c) 
{     
    MyCin >> c.rno; 
    MyCin >> c.marks; 
    return MyCin; 
} 
  
int main() 
{ 
   Student s1; 
   cin >> s1; 
   cout << s1; 
   return 0; 
}

A) Compilation fails
B) Segmentation fault
C) Compiles fine but prints Nothing
D) None of these
E) 15 95



Ans- E

6)#include<iostream>
using namespace std; 
  
class Sample
{ 
private: 
    int x,y;
public: 
     void sample();
     void display();
}; 

void Sample::sample()
{
    cin>>x>>y;
}

void Sample::display()
{
    cout<<x<<" "<<y;
}  

int main() 
{ 
   Sample s1; 
   s1.sample();
   s1.display();
   return 0; 
}

A) Compilation fails
B) Reads two numbers and prints two numbers
C) Compiles but prints nothing
D) Segmentation fault


Ans- B

7) #include<iostream>
using namespace std; 
  
class Sample
{ 
private: 
    int x,y;
public: 
     void read();
     void display();
}; 

void Sample::read()
{
    cin>>x>>y;
}

void Sample::display()
{
    cout<<x<<" "<<y;
}  

int main() 
{ 
   Sample *s1;
   s1 =(Sample *)malloc(sizeof(Sample)); // Line A
   s1->read();
   s1->display();
   return 0; 
}

A) reads two numbers and prints two numbers
B) the code will work if and only if  replaced Line A to 
     s1=new Sample;
C) the code will work if and only if replaced Line A to 
     s1 = (Sample)new Sample;
D) What ever changes you make the code will not compile at all


Ans- A

8) #include<iostream>
using namespace std; 
  
class Sample
{ 
  private: 
    int x,y;
  public: 
    void read();
    void show(Sample s);
}; 

void Sample::read()
{
    cin>>x>>y;
}

void show(Sample s)
{
    cout<<s.x<<" "<<s.y;
}

int main() 
{ 
   Sample s2;
   s2.read();
   show(s2);
   return 0; 
}

In order to make the code compile we should mark the show(Sample s) in the class Sample as 

A) static
B) inline
C) friend
D) const



Ans- C

9)
public class Test
{
  public static void main(String [] args ) 
  {
     Integer x = new Integer(256);
     System.out.println(x.byteValue());
  }
}

A) Prints 127
B) Prints 256
C) Runtime error
D) Compilation fails
E) Prints 0




Ans - E

Explanation 
Method byteValue() returns the value of Integer as a byte

10)
public class Main
{
  String pearl(String s)
  {
    return s.substring(0,1);      //Line A
  }
  public static void main(String [] args ) 
  {
    Main m = new Main();
    char c = 4 * 4;        //Line B
    String str="Bead";

    str=m.pearl(str);
    System.out.println(Byte.parseByte(str,c)); // Line C
  }
}

A) Compilation fails at Line A only
B) Compilation fails at Line B only
C) Compilation fails at Line C only
D) Runtime exception
E) Compilation fails at all the three lines (Line A, Line B and Line C)
F) Compiles fine and prints some number 



Ans - F


Prints 11 
The Hexadecimal value of letter B 

11)
public class Test
{
  public static void main(String [] args ) 
  {
    byte a = 10;
    Byte b = new Byte(a);
    Byte c = new Byte(11);
    System.out.println(b.compareTo(c));
	}
}

A) Runs and prints false
B) Runtime error
C) Compiletime error
D) Runs and prints 1
E) Runs and prints 0
F) Runs and prints -1




Ans- C

12)
public class Main
{
  public static void main(String [] args ) 
  {
    StringBuffer a="Hello";
    StringBuffer b = a.append(" World");
    System.out.println(b);
	}
}

A) Hello World
B) Hello
C) World
D) Compilation fails
E) Run time exception




Ans- D

13)
In SQL, __________ is an Aggregate function.
(A) SELECT
(B) CREATE
(C) AVG
(D) MODIFY



Answer: (C)

14)
Consider the following tables 

employee 

empid	empname	    managerid		  deptid		salary		    dob
11		  Ram          0			      1			  40000	      01-01-1991
12		  Murali       0			      2       35000       21-02-1987
13      Tarang       1            1       30000       25-08-1989
15      Lisa         2            2       42000       31-05-1992
27      Fatima       2            1       39000       17-04-1990

Department

Deptid             DeptName
1                   IT
2                   Admin

What is the outut of below SQL Query?

SELECT * FROM EMPLOYEE E
WHERE 2 = (SELECT COUNT(DISTINCT E1.SALARY)
FROM EMPLOYEE E1
WHERE E1.SALARY > E.SALARY)

A) Second Highest salary
B) Two distinct salary of employees
C) Third highest salary
D) Employee with second highest salary





Ans- Answer: (C)

Explanation: Query will give the 3rd highest salary. N-1 = 3-1 = 2
Can be used to find for any value of n.

15)
Consider the schema
Sailors(sid, sname, rating, age) with the following data

sid 	sname 	rating 	age
22 	Dustin 	  7 		45
29 	Borg 		  1 		33
31 	Pathy 	  8 		55
32 	Robert 	  8 		25
58 	Raghu 	  10 		17
64 	Herald 	  7 		35
71 	Vishnu 	  10 		16
74 	King 		  9 		35
85 	Archer 	  3 		26
84 	Bob 		  3 		64
96 	Flinch 	  3 		17

For the query

SELECT S.rating, AVG(S.age) AS avgage FROM Sailors S
Where S.age >= 18
GROUP BY S.rating
HAVING 1 < (SELECT COUNT(*) FROM Sailors S2 where S.rating = S2.rating)

The number of rows returned is
(A) 6
(B) 5
(C) 4
(D) 3




Answer: (D)

Explanation: The qiven query would run like:
First of all where statement would be executed and all the tuples with age less than 18 would be eliminated.
Now with Group By the remaining tuples will be grouped according to rating: 


## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/16th%2BJuly%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/16th+July+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
