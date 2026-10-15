---
kind: "study-reference"
title: "14th+July+MCQs"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/14th+July+MCQs.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 14th+July+MCQs

[[The Climb/Career Library/Career Library]]

1)which of the following statements are correct about an if-else statement in a C Program ?

A) Every if-else statement can be replaced by an equivalent statement using ?: operators
B) Nested if-else statements are allowed.
C) if we use an if it is compulsory to use an else
D) Multiple statements in an if block are allowed
E) Multiple statements in an else block are allowed 























Ans- B,D,E

https://www.indiabix.com/c-programming/control-instructions/discussion-54

2) output of the following code

#include<stdio.h>
int main() {
int x=10,y=20;
if(!(!x) && x)
	printf("x=%d\n",x);
else
	printf("y=%d\n",y);
return 0;
}

A) y=20
B) x=0
C) x=10
D) x=1
E) x=-10





Ans-C

3) output of the following C code 

Assume the sizes are given as below 

int- 4 bytes
float - 4 bytes
double - 8 bytes
char - 1 bytes
long double - 16 bytes

#include<stdio.h>
int main()
{
   printf(" %lu %lu %lu ", sizeof(3.14f),sizeof(3.14),sizeof(3.14l));
}

A) 4 4 4 
B) 4 8 16
C) 4 8 8
D) 4 8 12




Ans- B

4)
The binary equivalent of 5.375 is 

A) 101.101110111
B) 101.011
C) 101011
D) None of these




Ans- B

we can write 5 in binary format as 101 

for the number 0.375 in binary format we have to multiple by 2 

0.375 * 2 = 0.750
0.75 * 2 = 1.500
0.5 * 2 = 1.000

Consider,only the decimal part from top to bottom ( 0 1 1)
so 0.375 in decimal is equivalent to .011 in binary.

Adding up we get 

101 + 0.011 = 101.011 

5)
#include<stdio.h>
int main()
{
int i = 1;
if(!i)
	 printf("\n Recursion ends here ");
else
{
	i=0;
	printf("\n Recursion continues here ");
	main();
}
return 0;
}

A) Recursion ends here
     Recursion continues here
  
B)  Recursion continues here
     Recursion ends here

C) Recursion ends here

D)  Recursion continues here

E) The Code prints Recursion continues here 
     Recursion continues here (till the stack over flows )




Ans- E

6) Output of the following CPP Code

Assume the size of int as 4 bytes 

#include<iostream>
using namespace std;
class parent
{
    int i;
};

class child : public parent
{
    int j;
};

int main()
{
  cout<<sizeof(parent)<<" "<<sizeof(child)<<" ";
  parent p;
  child c;
  cout<<sizeof(p)<<" "<<sizeof(c);
  return 0;
}

A) 4 4 4 4 
B) 1 1 1 1
C) 4 8 4 8
D) 8 8 8 8




Ans- C

7)#include<iostream>
#include<string.h>

using namespace std;
class parent
{
    public:
    int i=10;
    char s[10]="sachin";
    parent()
    {
      i=20;
      strcpy(s,"scott");
      
    }
    parent(int i,char s[10])
    {
        this->i=i;
        strcpy(this->s,s);
    }
};

int main()
{
parent p(30,"shyam");
cout<<p.i<<" "<<p.s;
return 0;
}

A) 10 saching
B) 20 scott
C) 30 shyam
D) Compilation fails




Ans- C

8)#include<iostream>
using namespace std;

int i=3;

class parent
{
    protected: 
    int i;
    public:
    parent() {
        i=2;
        cout<<" "<<i;
    }
};

class child:public parent
{
    int i;
    public:
    
    child():parent() {
        i=1;
        cout<<" "<<i;
        cout<<" "<<parent::i;
        cout<<" "<<::i;
    }
};

int main()
{

child c;
return 0;
}

A) 1 1 2 3
B) 2 2 2 3
C) 2 1 2 3
D) Compilation fails




Ans- C

9)#include<iostream>
using namespace std;

class parent
{
     public:
      virtual void display()=0;
};

class child:public parent
{
     private:
     virtual void display() =0;  // Line A
};

class child2 : child       // Line B
{
    public:
    void display()
    {
        cout<<"display called";
    }
};

int main()
{
child2 c;
c.display();
return 0;
}

A) Compilation fails at Line A
B) Compilation fails at Line B
C) Compilation fails at Both Line A and Line B
D) Compiles fine and prints display called




Ans- D

10) #include<iostream>
using namespace std;

class sample
{
  static int count ;
  public:
  sample() {
     count++;
  }
  static void showcount() {
     cout<<" "<<count;
  }     
};

int sample::count=0;

int main()
{
  sample s;
  sample::showcount();
  sample s2;
  sample::showcount();
  sample s3;
  sample::showcount();

  return 0;
}

A) 3 3 3
B) 1 2 3
C) 0 1 2
D) Compilation fails
E) 2 2 2





Ans- B

11) Given the default classpath:
/foo

And this directory structure:

foo
   |
 test
     |
     xcom
           |--A.class
           |--B.java

And these two files:

package xcom;
public class A { }

package xcom;
public class B extends A { }

Which allows B.java to compile? (Choose all that apply.)

A. Set the current directory to xcom then invoke
    javac B.java

B. Set the current directory to xcom then invoke
    javac -classpath . B.java

C. Set the current directory to test then invoke
    javac -classpath . xcom/B.java

D. Set the current directory to test then invoke
     javac -classpath xcom B.java

E. Set the current directory to test then invoke
    javac -classpath xcom:. B.java

Answer:

C is correct. 

In order for B.java to compile, the compiler first needs to be able to find  B.java. 
Once it's found B.java it needs to find A.class. 
Because A.class is in the xcom package the compiler won't find A.class if it's 
invoked from the xcom directory.

Remember that the -classpath isn't looking for B.java, it's looking for whatever
classes B.java needs (in this case A.class)

12)
Given two files:

1. package pkgA;
2. public class Foo {
3. int a = 5;
4. protected int b = 6;
5. }

1. package pkgB;
2. import pkgA.*;
3. public class Fiz extends Foo {
4. public static void main(String[] args) {
5. Foo f = new Foo();
6. System.out.print(" " + f.a);
7. System.out.print(" " + f.b);
8. System.out.print(" " + new Fiz().a);
9. System.out.println(" " + new Fiz().b);
10. }
11. }
What is the result? (Choose all that apply.)

A. 5 6 5 6
B. 5 6 followed by an exception
C. Compilation fails with an error on line 6
D. Compilation fails with an error on line 7
E. Compilation fails with an error on line 8
F. Compilation fails with an error on line 9





Answer: C, D, and E are correct. 

Variable a (default access) cannot be accessed from outside the package. 
Since variable b is protected, it can be accessed only through inheritance.

13) Given:
3. import java.util.*;
4. public class Antique {
5. public static void main(String[] args) {
6. List<String> myList = new ArrayList<String>();
7. assert (args.length > 0);
8. System.out.println("still static");
9. }
10. }

Which sets of commands (javac followed by java) will compile and run without 
exception or error? (Choose all that apply.)

A. javac Antique.java
java Antique

B. javac Antique.java
java -ea Antique

C. javac -source 6 Antique.java
java Antique

D. javac -source 1.4 Antique.java
java Antique

E. javac -source 1.6 Antique.java
java -ea Antique

Answer:
A and C are correct. If assertions (which were first available in Java 1.4) 
are enabled, an AssertionError will be thrown at line 7.
D is incorrect because the code uses generics, and generics weren't introduced 
until Java 5.


14)Output of the following java code 

public class Main {
public static void main (String[] args) {
        double d = 10.0/-0;
        if(d==Double.POSITIVE_INFINITY)
            System.out.println("Positive Infinity");
        else
            System.out.println("Negative Infinity");
    }
}

A) Runtime exception
B) Compilation fails
C) Positive Infinity 
D) Negative Infinity



Ans- C

15)public class Main {
    
public static void main (String[] args) {
        int [] a ={1};
        Main m = new Main();
        m.increment(a);
        System.out.println(a[a.length-1]);
        
    }
    void increment(int [] j){
        j[j.length-1]++;
    }
}

A) An ArrayIndexOutOfBounds Exception at runtime
B) Compiles and runs printing out 2
C) Compiles and runs printing out 1
D) Compile error





Ans- B



## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/14th%2BJuly%2BMCQs.txt) · CODING RESOURCES/Quiz Mcqs/14th+July+MCQs.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
