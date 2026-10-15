---
kind: "study-reference"
title: "MCQ DAY 45"
collection: "Course Quizzes"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 45 Solutions/MCQ DAY 45.java"]
tags: ["career/library"]
source_status: "source-reference"
---

# MCQ DAY 45

[[The Climb/Career Library/Career Library]]

```java
1. Which of the following statement is correct about program given below?

abstract class Super
{
	abstract void CallMe( );
	void Super( )
	{
		System.out.print ("Super Abstract");
	}
}
class Sub extends Super
{
	void CallMe()
	{
		System.out.print ("Sub Class");
	}
}
class Main
{
	public static void main (String args[])
	{
		Sub S = new Sub();
		S.CallMe();
	}
}

A. Above program will print the output: Super Abstract.
B. Above program will print the output: Sub Class.
C. Above program will print the output: Super Abstract Sub Class.
D. Above program will report compilation error.

ANSWER: B



2. Which of the following statement is correct about program given below?

class Good
{
	Good()
	{
		System.out.println ("Good");
	}
}
class Better extends Good
{
	Better()
	{
		System.out.println ("Better");
	}
}
class Best extends Better
{
	Best()
	{
		System.out.println ("Best");
	}
}
class Main
{
	public static void main (String Args[])
	{
		Good Obj = new Best();
	}
}

A. Above program will report compilation error.
B. Above program will print the output:
	Good
	Best
C. Above program will print the output:
	Best
    Good
D. Above program will print the output:
	Good
	Better
	Best
	
ANSWER: D



3. Which of the following statement is correct about program given below?

class XYZ
{
	int A;
	XYZ()
	{
		ABC AB = new ABC();
		A += 1;
	}
}
class ABC extends XYZ
{
	ABC()
	{
		System.out.println (A);
	}
}
class Main
{
	public static void main (String args[])
	{
		ABC AB = new ABC();
	}
}

A. Above program will print the output: 2.
B. Above program will print the output: 1.
C. Above program will report compilation error.
D. Above program will report run-time error.

ANSWER: D


4. Which of the following statement is correct about program given below?

class abc
{
	void Show ( ) { };
}
class xyz extends abc
{
	void Show ( )
	{
		System.out.println ("Hello");
	}
}
class TestDemo
{
	public static void main (String Argc[])
	{
		abc A = new abc();
		A.Show();
	}
}

A. Above program will print "Hello".
B. Above program will not print anything in console.
C. Above program will report compilation error.
D. Above program will report run-time error.

ANSWER: B


5. Which of the following statement is correct about program given below?

class A
{
	final void meth()
	{
		System.out.print ("Legal");
	}
}
class B extends A
{
	void meth ()
	{
		System.out.print ("illegal!");
	}
}
class Main
{
	public static void main ( String args[])
	{
		B obj = new B();
	}
}

A. Above program will print the output: Legal.
B. Above program will print the output: illegal!
C. Above program will print the output: Legal illegal!
D. Above program will report compilation error.

ANSWER: D



6. What will be the output of the program given below?

class A1
{
	int i = 5;
	public void fun()
	{
		System.out.print ("i" + ++i);
	}
}
class B1 extends A1
{
	int i = 7;
	public void fun()
	{
		System.out.print ("i" + ++i);
	}
}
class Test
{
	static void fun()
	{
		A1 C = new B1();
		C.fun();
	}
	public static void main (String args[])
	{
		fun();
	}
}


A. i 5
B. i 6
C. i 7
D. i 8

ANSWER: D


7. What will be the output of the program given below?

class Test
{
	class InTest
	{
		int In;
		InTest()
		{
			System.out.print ("Object of InTest");
		}
	}
	Test()
	{
		InTest I = new InTest();
		System.out.print ("Object of Test");
	}
}
class Test2 extends Test
{
	Test2()
	{
		Test T = new Test();
		System.out.print ("Object of Test2");
	}
}
class WithMain
{
	public static void main (String args[])
	{
		Test2 T2 = new Test2();
	}
}

A. Object of Test2 Object of InTest Object of Test1 Object of InTest.
B. Object of InTest Object of Test1 Object of Test2.
C. Object of InTest Object of Test Object of InTest Object of Test Object of Test2.
D. Object of Test Object of InTest Object of Test Object of InTest Object of Test2.

ANSWER: C


8. Which of the folowing statement is correct about the program given below?

class Test
{
	int In;
	class InTest
	{
		int In;
		InTest()
		{
			super.In = In;
	    }
    }
	Test()
    {
		In ++;
    }
}

class Test2 extends Test
{
	Test2()
    {
		super.In ++;
		System.out.print(super.In);
	}
}

class WithMain
{
	public static void main (String args[])
	{
		Test2 T2 = new Test2();
    }
}

A. The above program will print output 0.
B. The above program will print output 1.
C. The above program will print output 2.
D. The program will report compile time error.


ANSWER: D


9. What will be the output of the program given below?

class Test
{
	int In;
	class InTest
	{
		int In;
		InTest()
		{
			In ++;
	    }
    }
	Test()
    {
		InTest t = new InTest();
		In = t.In;
    }
}

class Test2 extends Test
{
	int In;
	Test2()
    {
		super.In ++;
		System.out.print(In);
	}
}

class WithMain
{
	public static void main (String args[])
	{
		Test2 T2 = new Test2();
    }
}


A. 0
B. 1
C. 2
D. 3

ANSWER: A


10. Which of the folowing statement is correct about program given below?

class Min
{
	public       int z;
	Min()
	{
		z = 1;
	}
	void showdata()
	{
		System.out.print(z + "");
	}
}

class Max extends Min
{
	public int z1;
	Max()
	{
		z1 = 2;
	}
	void showdata()
	{
		System.out.print(z1 + "");
	}
}

class More extends Max
{
	public More()
	{
		System.out.print (z1 +"");
	}
}

class MinMaxMore
{
	public static void main (String args[])
	{
		More M = new More();
    }
}

A. The above program will print the output 2.
B. The above program will print the output 1 2.
C. The above program will print two non-negative numbers.
D. The above program will report compilation error.

ANSWER: A
```

## Source provenance

- [Original JAVA](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2045%20Solutions/MCQ%20DAY%2045.java) · CODING RESOURCES/ELITE FS COMPLETE/Day 45 Solutions/MCQ DAY 45.java

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
