---
kind: "study-reference"
title: "31st+Jan+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/31st+Jan+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 31st+Jan+MCQ's

[[The Climb/Career Library/Career Library]]

1. What will be the output of the following code?
class Is_operator {
public static void main(String [] args)
{
   byte x = 64;
   int i;
   byte y;
   i = x << 2;
   y = (byte) (x<<2);
   System.out.println(i + "   "+ y);
   }
}
A. 0 64
B. 64 256
C. 256 256
D. 256 0
ANSWER: D

2. What will be the output of the following code?
class jump_statments {
public static void main(String [] args) {
     int x=2;
     int y=0;
     for(; y < 10; ++y)
          if( y % x== 0) 
	     continue;
	  else if( y==8) 
	      break;
	   else
             System.out.print(y+" ");	     
}
}
A. 1 3 5 7
B. 2 4 6 8
C. 1 3 5 7 9
D. 1 2 3 4 5 6 7 8 9
ANSWER: C

3. What will be the output of the code snippet given below?

public class Main
{
	public static void main(String[] args) 
	{
		String str = "A chink in your armour, A voice in your mailbox";
		System.out.println (str.replace (str.subSequence (str.indexOf('c'),str.indexOf ('i')), 
						str.subSequence (str.indexOf('v'),str.indexOf('b'))));
	}
}

A. A voice in your mailink in your armour, A voice in your mailbox
B. ch
C. voice in your mail
D. A voice in your mailbox A chink in your armour,
ANSWER: A

4. Which of the following statement is correct about the code snippet given below?

class A
{
	int i;
	private int j;
	void setij (int x, int y)
    {
		i = x;
		j = y;
	}
}
class B extends A
{
	int total;
	void sum( )
    {
		total = i+j;
    }
}
public class Program
{
	public static void main (String[ ] args)
    {
		B subOb = new B( );
		subOb.setij (10,12);
		subOb.sum( );
		System.out.println (subOb.total);
	}
}

A. The code reports an error.
B. The code causes java.lang.ArthimeticException.
C. The code gives an output as 22.
D. The code gives an output as 10.
ANSWER: A


5. Which of the following are the correct ways to construct instances of the 'Program' class given below?

public class Program 
{
    public Program ( int j )
    {
    }
    public Program ( int j, int k )
    {
		this( k ) ;
    }
}

I.   Program p1 = new Program( ) ;
II.  Program p2 = new Program(1) ; 
III. Program p3 = new Program(1,2) ;

A. Only I and II
B. Only I and III
C. Only II and III
D. I,II and III
ANSWER: C

6. What will be the output of the code snippet given below?
import java.io.*;
class Base
{
	 public void method (int i)
     {
		 System.out.print ("Value is" +i);
     }		  
}
public class Program extends Base
{
      public void method (int j)
      {
		  System.out.print ("This value is"+j);
      }
	  public void method (String s)
      {
		  System.out.print ("I was passed"+s);
      }
	  public static void main(String args[])
      {
		  Base b1= new Base();
		  Base b2= new Program();
		  b1.method (5);
		  b2.method (6);
      }
}

A. This value is 5This value is 6
B. This value is 5Value is 6
C. Value is 5This value is 6
D. I Was passed 5I was passed 6
ANSWER: C

7. What will be the output of the code snippet given below?
class Outer
{
	String s = "Outer" ;
	public static void main ( String[] args )
	{
		new Outer().new Inner() ;
	}
	class Inner
	{
		String s = "Inner" ;
		Inner()
	    {
			System.out.print( this.s+" " ) ;
			System.out.print( Outer.this.s ) ;
		}
	}
}

(a) Outer
	Inner
(b) Outer
	Outer
(c) Inner
	Inner
(d) Inner
	Outer

ANSWER: D


8. What will be the output of the following snippet given below?
class S1
{
      public static void main (String[ ] args)
      {
		  new S2();
      }
      S1()
      {
		System.out.print ("S1");
      }
}
class S2 extends S1
{
	S2()
	{
		System.out.print ("S2");
        } 
}

A. S1
B. S2
C. S1S2
D. S2S1
ANSWER: C

9. How many objects of class Test can be created in the following program using the CreateObj()?

class Test
{
   static Test T;
   public Test()
   {
   }
   public static Test CreateObj()
   {
	if ( T== null)
	   T = new Test();
	return T;
    }
}

A. Only I
B. Only 5
C. Only 10
D. As much as user wants
ANSWER: A

10. Which of the following statement is correct about the program given below?

class Sample
{
	String str;
	Sample()
    {
		str="hello";
    }
	Sample Fun()
    {   
    }
}
class Main
{
	public static void main (String[ ] args)
    {
		Sample S= new Sample();
		Sample S1= S.Fun();
		S1.str ="Hi";
		System.out.printf(S.str);
		System.out.printf(S1.str);
	}	 
}

A. The code gives an output as HelloHi.
B. The code gives output as HiHi.
C. The code reports an error.
D. The code gives an output as HelloHello.
ANSWER: B


## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/31st%2BJan%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/31st+Jan+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
