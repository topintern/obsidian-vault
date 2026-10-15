---
kind: "study-reference"
title: "21st+July+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/21st+July+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 21st+July+MCQ's

[[The Climb/Career Library/Career Library]]

1) what is the output of the following C Code

#include <stdio.h>

int main()
{
    int i=5;
    const int j = 3;
    switch(i)
    {
        case 1 : printf("one "); break;
        case j+2 : printf("Three ");
        case 5: printf(" five "); break;
    }  
    return 0;
}

A) Three five
B) five
C) Compilation fails
D) Segmentation fault









Ans - C

2)

#include <stdio.h>

int main()
{
    char ch='A';
    printf(" %c ", ch>='A' && ch<='Z' ? ch+'a'-'A':ch);
    printf(" %c ", ch >='A' && ch <='Z' ?ch: ch +'a'-'A');   
    return 0;
}

A) Compilation fails
B) Segmentation fault
C) a A
D) A a
E) A A
F) a a





Ans- C

3) Output of the following C Code

#include <stdio.h>
int m2(int x)
{
    return x*x;
}

int  m1(int a, int b)
{
   return (m2(11));
}

int main()
{
    printf(" %d ", m1(10,20));
    return 0;
}

A) Compilation fails
B) Segmentation fault
C) 11
D) 121




Ans: D

4)
#include <stdio.h>
int fun(int,int);
typedef int (*pf) (int,int);
int proc(pf,int,int);

int main()
{
    printf(" %d ", proc(fun,6,6));
    return 0;
}

int fun(int a,int b)
{
    return (a==b);
}

int proc(pf p, int a, int b)
{
    return ((*p)(a,b));
}

A) 6
B) 1
C) 0
D) -1





Ans: B

5) Output of the following C Code 

#include <stdio.h>
int main()
{
    printf(" %c ", "zyxwvutsrqpo"[4]);
    return 0;
}

A) 118
B) v
C) Compilation fails
D) w
E) s




Ans- B

6)
#include<iostream>
using namespace std;

template<class T,class S,class Z> void fun(T a,S b,Z c)
{
 cout<<a<<" "<<b<<" "<<c;
}

class Sample
{
    int i;
    public:
    Sample() {i=100;}
    
    friend  ostream & operator << (ostream &MyCout, const Sample &c){
          MyCout<<c.i<<" ";
      }
    
};

int main()
{
    int i=10;
    char c='T';
    Sample S;
    fun(i,c,S);
}

A) Compilation fails
B) Segmentation fault
C) 10 T Garbage Value
D) 10  T 100
E) None of these




Ans- D

7) Output of the below CPP Code 

#include<string.h>
#include<iostream>
using namespace std;

class Sample
{
    int i;
    public:
    class ErrClass
    {    public:
         char str[50];
         ErrClass(const char *s)
          {
              strcpy(str,s);
          }
        
    };
    void fun(int a,int b)
    {
        int c;
        if(b==0)
          throw ErrClass("This is a Divison Error ");
        else
        {
            c=a/b;
            cout<<c<<" ";
        }
    }
};

int main()
{
    try {
      Sample S;
      S.fun(20,5);
      S.fun(2,0);
    }
    catch(Sample::ErrClass e)
    {
        cout<<e.str<<endl;
    }
    catch(char *st)
    {
        cout<<st<<" exception caught ";
    }
    return 0;
}

A) Compilation fails
B) Segmentation fault
C) 4 followed by Segmentation fault
D) 4 This is a Divison Error 
E) 4 This is a Divison Error exception caught 





Ans - D

8) Output of the below cpp code 

Assume the size of int as 4 bytes 

#include<string.h>
#include<iostream>
using namespace std;

class Sample
{
    public :
      int i : 10;
      int j : 5;
      Sample()
      {
        i=3;
        j=4;
      }    
};

int main()
{
  Sample s;    
  cout<<sizeof(s);
  return 0;
}

A) 4 bytes
B) 15 bits
C) 8 bytes
D) None of these





Ans- A

9) Output of the below java called 

interface A {
    void m1();
}

class Main
{
  A a;
  void m2()
  {
    a=new A()
    {
      public void m1(){
          System.out.println("m1 called");
      }  
    };
  }
  public static void main(String [] args)
  {
      Main m = new Main();
      m.a.m1();
  }    
}

A) Compilation fails
B) m1 called
C) NoSuchMethodException at runtime
D) NullPointer exception at runtime 





Ans- D

10)
IF start is called again on a dead thread, which exception is thrown 

A) IllegalThreadStateException
B) InterruptedException
C) IllegalMonitorStateException
D) None of these







Ans- A

11)
class C1
{
    static class C2
    {
        static int i;
    }
    public static void main(String args[])
    {
        System.out.println(C1.C2.i);
    }
}


A) Compilation fails
B) Runtime Exception
C) 0
D) Garbage Value





Ans- C

12) what does the below mysql trigger do 

create trigger t1  before  UPDATE on sailors
for each row
begin
   if new.age>60 then
      set new.age=old.age;
   else
      set new.age=new.age;
   end if;
end;
$

A) updates the sailor table age column to the value 60 for all rows 
B) it only checks if the sailor table has age column or not
C) the way of creating the trigger is not correct here 
D) None of these




Ans- D

13)
Given the following table Managers with (Id,Name,Salary) as the columns what
will be the rows of the Managers table after the below query has been executed 

Query:

DELETE M1 
From managers M1, managers M2 
Where M2.Name = M1.Name AND M1.Id>M2.Id; 

Managers –
Id 	Name 		    Salary
1 	Harpreet 		20000
2 	Ravi 			  30000
3 	Vinay 		  10000
4 	Ravi 			  30000
5 	Harpreet 		20000
6 	Vinay 		  10000
7 	Rajeev 		  40000
8 	Vinay 		  10000
9 	Ravi 			  30000
10 	Sanjay 		  50000

A) 
Managers –
Id 	Name 	Salary
1 	Harpreet 	20000
2 	Ravi 		30000
3 	Vinay 	10000
7 	Rajeev 	40000
10 	Sanjay 	50000

B) 
Managers –
Id 	Name 		Salary
5 	Harpreet 		20000
6 	Vinay 		10000
7 	Rajeev 		40000
9 	Ravi 			30000
10 	Sanjay 		50000

C) Managers –
Id 	Name 		Salary
1 	Harpreet 		20000
2 	Ravi 			30000
3 	Vinay 		10000
4 	Ravi 			30000
5 	Harpreet 		20000
6 	Vinay 		10000
7 	Rajeev 		40000
8 	Vinay 		10000
9 	Ravi 			30000
10 	Sanjay 		50000

D) None of these




Ans- A

14)

Unit testing is done by:

a) Users
b) Developers
c) Customers
d) None of the mentioned





Ans- b) Developers

Explanation: 
Unit testing is a method by which individual units of source code, sets of one
or more computer program modules together with associated control data,
operating procedures and usage procedures are tested to identify if they are 
fit for use or not.

15)

System testing is a

a) Black box testing
b) Grey box testing
c) White box testing
d) Both a and b





Answer:a) Black box testing

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/21st%2BJuly%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/21st+July+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
