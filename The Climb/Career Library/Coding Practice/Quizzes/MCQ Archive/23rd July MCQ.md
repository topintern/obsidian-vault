---
kind: "study-reference"
title: "23rd July MCQ"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/23rd July MCQ.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 23rd July MCQ

[[The Climb/Career Library/Career Library]]

1) 

What should be the empty line in the following code should be filled to make the code work and print 20 

#include<stdio.h>

int check(int,int);

int main()
{
	int c;
	c=check(10,20);
	printf(" %d ",c);
}

int check(int i,int j)
{
	int *q,*p;
	p=&i;
	q=&j;
//	_________
}


A) i >= 45 ? return(*p):return(*q);
B) return i >= 45 ? *p:*q;
C) return i >= 45 ? *q:*p;
D) i >= 45 ? return(*q):return(*p);
E) None of these


Ans- B





2)
If an int is 4 bytes wide then which of the following is the correct output for the program given below ?

#include<stdio.h>
void fun(char **);
int main()
{
    char *argv[]={"hello","doing","good","everyone"};
    fun(argv);
}

void fun(char **p)
{
     char *t;
     t=(p+sizeof(int))[-1];
     printf(" %s ", t);
}


A) hello
B) doing
C) good
D) everyone
E) Compilation fails
G) Segmentation fault


Ans- D



3)
what will be the output of the program(Test.c) if it is executed from the command line as shown below

Test 1 2 3

#include<stdio.h>
#include<stdlib.h>
int main(int argc,char *argv[])
{
	int i,j=0;
	for(i=0;i<argc;i++)
	  j=j+atoi(argv[i]);
	printf(" %d ", j);
	return 0;
}

A) 1 2 3
B)  6
C) Compilation error
D) "123"


Ans- B




4) output of the followint C code 

#include<stdio.h>

int main()
{
    int i=32,j=0x20,k,l,m;
    k=i|j;
    l=i&j;
    m=k^i;
    printf(" %d %d %d %d %d ", i, j, k, l,m);
    return 1;
}



A) 0 0 0 0 0 
B) 32 32 32 32 0
C) 0 32 32 32 32
D) 32 32 32 32 32

Ans - B




5)
What will be the output of the following c code 

#include<stdio.h>

int main()
{
    typedef int LONG;
    LONG a = 4;
    LONG b = 68;
    float c = 0;
    c=b;
    b+=a;
    printf(" %d %f ", b, c);
    
    return 1;
}

A) 72.000000 68
B) 68.000000 72.000000
C)  Compilation fails
D) 72 68.000000 


Ans- D



6) 
output of the below cpp code 

#include<iostream>
using namespace std;

class sample
{
    private:
    int i;
    public :
    virtual void display() { }
};

class example
{
int i;
public :
void display() {   }
};

class demo
{
   public: void display() { }
};

int main()
{
    cout<<sizeof(sample)<<" ";
    cout<<sizeof(demo)<<" ";
    cout<<sizeof(example);
    return 1;
 }

 A) 8 8 8
 B) 8 4 1
 C) 8 1 4
 D) 8 4 4


 Ans- C



 7)
output of the below cpp code 


#include<iostream>
using namespace std;

class sample
{
    public :
    sample() { cout<<"sample called " ; }
};

class demo:public sample
{
public :
void display() { ::sample(); cout<<" display called ";  }
};

int main()
{
    demo d;
    d.display();
    return 1;
 }

 A) sample called display called
 B) Compilation fails
 C) Segmention fault
 D) sample called sample called display called


 Ans - D



 8)
output of the below cpp code 

#include<string.h>
#include<iostream>
using namespace std;

class sample
{
    int rno=55;
    int marks = 100;
    char name[25]="Shiva";
    public :
    sample() { 
        rno= 95;
        marks = 85;
        strcpy(name,"Arjun");
        
        
    }
    void display()
    {
        cout<<rno<<" "<<name<<" "<<marks;
    }
};


int main()
{
    sample s;
    s.display();
    return 1;
 }

 A) Compilation fails
 B) Segmentation fault
 C) 95 Arjun 85   
 D) 55 Shiva 100


 Ans- C



9)
what is the output of the java code 

class A extends Thread
{
    public void run(){
        System.out.print("A ");
    }
}

class Main{
    public static void main(String [] args)
    {
        A a = new A();
        a.run();
        a.start();
    }
}


A) A A
B) Compilation fails
C) Results in "IllegalThreadStateException"
D) None of these
E) A


Ans - A



10)
what is the output of the java code 

class Main{
    public void m1(Object o1)
    {
        System.out.println("Object");
    }
    public void m1(String str)
    {
        System.out.println("String");
    }
    public void m1(StringBuffer sb)
    {
        System.out.println("String Buffer");
    }
    
    public static void main(String [] args)
    {
        new Main().m1("Hello");
    }
}


A) Object
B) String
C) String Buffer
D) Compilation Fails


Ans- B



11)
what is the output of the java code 


class Main{
    private String get(String str)
    {
        try {
        throw new Exception();
        
        }
        catch(Exception e)
        {
            return null;
        }
    }
    public static void main(String [] args)
    {
        try {
            System.out.println(new Main().get("Hello"));
            
        }catch(Exception e)
        {
        System.out.println("Exception ");
            
        }
        }
    
}


A) Results in NullPointerException
B) Compilation fails
C) Compiles fine and prints null
D) None of these
E) Compiles fine but prints nothing


Ans - C




12) 
what is the output of the java code 

class Main extends Exception implements Runnable{
    
    public void run() { }
    
    public static void main(String [] args)
    {
        Main m = new Main();
        Thread t = new Thread(m);
        t.start();
        t.setPriority(-1);
    }
    
}


A) Compialtion fails
B) Results in IllegalArgumentException
C) Compiles fine and prints nothing
D) None of these 



Ans- B


13)

Consider the following schema:

Emp (Empcode, Name, Sex, Salary, Deptt)

A simple SQL query is executed as follows:

SELECT Deptt FROM Emp
WHERE sex = 'M'
GROUP by Dept
Having avg (Salary) > {select avg (Salary) from Emp}

The output will be
(A) Average salary of male employee is the average salary of the organization
(B) Average salary of male employee is less than the average salary of the organization
(C) Average salary of male employee is equal to the average salary of the organization
(D) Average salary of male employee is more than the average salary of the organization


Answer: (D)




14) Project Risk Factor is considered in ?

A) Spiral Model
B) Waterfall Model
C) Prototyping Model
D) Iterative enhancement model

Ans-A


15) In the Spiral model, ‘risk analysis’ is perfomed

a) In the first loop
b) In the first and second loop
c) In every loop
d) Before using spiral model



Ans- C


## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/23rd%20July%20MCQ.txt) · CODING RESOURCES/Quiz Mcqs/23rd July MCQ.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
