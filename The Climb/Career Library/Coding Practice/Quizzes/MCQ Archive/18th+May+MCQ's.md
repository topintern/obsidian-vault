---
kind: "study-reference"
title: "18th+May+MCQ's"
collection: "MCQ Archive"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/Quiz Mcqs/18th+May+MCQ's.txt"]
tags: ["career/library"]
source_status: "source-reference"
---

# 18th+May+MCQ's

[[The Climb/Career Library/Career Library]]

1) Assuming number of nodes >2 in a linked list, which of the following codes 
will delete two nodes from the linked list ?

a)Next[x]= Next[Next[x]];
b)Next[Next[x]]=x;
c)Next[x]=Next[Next[Next[x]]];
d)x=Next[Next[x+1]];























Ans- c



2) If the address of the first node of a linked list consisting of an integer and a 
pointer to next node is 1000, what will be the address of the second node
of the same linked list ?


a)1004
b)1008
c)1006
d)1002
e)None of these
















Ans-  None of these





3) Convert the following infix expression to postfix expression:

A+B*C-D/E*F

Assume the following precedence of operators

'/' > '*' > '+' > '-' 


a)ABC*+DEF/*-
b)ABC*+D/EF*-
c)ABC*+DEF/-*
d)ABC*+DE/F*-














Ans-d



4)
Consider a 2-D Array A[5...10][5...10] stored in a row-major order, 
where each element A[i][j], 5 <=i<=10 and 5<=j<=10 is of 4 bytes and the 
address of A[5][5] is 1000. what is the address of A[7][9] ?


a)1104
b)1108
c)1064
d)1068















  Ans- C

Formulae to calcuate the address of a Row Major order is 

	B + [(i-LB1) * N + (j-LB2)] * S

       Where B is the Base Address (1000)
       i,j are the indexs to find  (i=7,j=9)
       N is the Number of Columns  (6)
       S is the Size of the element (4) 

       Number of rows M =  UB1-LB1 +1   = 10-5+1 = 6
       Number of columns N = UB2-LB2+1 = 10 -5+1 = 6

       1000 + [(7-5) * 6 + (9-5)] * 4
       1000 + [ 2 * 6 + 4] * 4
       1000 + 16* 4
       1000 + 64
       
       =1064

  Ans- C


   5)
Consider a 2-D Array A[5...10][5...10] stored in a column-major order, 
where each element A[i][j], 5 <=i<=10 and 5<=j<=10 is of 4 bytes and the 
address of A[5][5] is 1000. what is the address of A[7][9] ?

a)1104
b)1108
c)1064
d)1068

Ans - A


address to calculate the column major order  is 

	B + [(i-LB1)+(j-LB2)*M]*S

	Where B is the Base Address (1000)
       i,j are the indexs to find  (i=7,j=9)
       S is the Size of the element (4) 
       Number of rows M =  UB1-LB1 +1   = 10-5+1 = 6
       Number of columns N = UB2-LB2+1 = 10 -5+1 = 6


      1000 + [  (7-5) + (9-5)*6] * 4
      1000 + [ 2 + 4*6 ] * 4
      1000 + 26 * 4
      1000 +  104
      1104


6)Identify the output of the following program in CPP
#include<iostream.h>
void main() {
	cout<<(int i=5)<<"\t"<<(int j=9);
}

a) 5 9
b) compile error
c) runtime error
d) blank screen













Ans- B



7)

In the case of nested loops in CPP, which of the following options will 
run the maximum number of times ?

a)Outermost loop
b)Innermost loop
c)Cannot be determined without checking the actual loop
d)Both loops will run same number of times







ans-c



8)#include<iostream.h>
void main() {
	switch(10) {
case 10 :
	cout<< "1" << endl;
	break;
case 10:
	cout <<"2" << endl;
}
}

a)1
b) 
1
2
c) 2
d) Error: Duplicate case value












Ans- d


9)

Considering the following enum in CPP, what will be value of Sunday ?
enum days { Sunday,Monday=5, Tuesday=6, Wednesday=7 }

a)4
b)0
c)Generate an error
d)No value until you assing it




















Ans- b




10)
#include <iostream>
using namespace std;

int main() {
	int a=10;
	int const &b=a;
	a=12;
	a+6;
	cout<<a;
	cout<<b;
	return 0;
}

a) 1818
b) 1010
c) 1212
d) Compilation error




















ans- c



11)
#include<stdio.h>
void main() {
	int i;
	char a[5] = {97,99,101, 103, 105};
	for(i=0 ; i<5 ; i = i+2)
		printf("%c", a[++i]);
	printf(",  %d", i);
}


a)ci, 6
b)ag, 6
c)ag, 5
d)Infinite loop















Ans-a


12)
#include<stdio.h>
void main() {
char arr[10] = "rectangle" ; //Line 3
int i;
for(i=0;i<=7;i++)
	printf(" %d ", arr[i]);
arr++;  //Line 7
}

a)No Error
b)We cannot declare an array of character type (Line3)
c)arr cannot be incremented (Line7)
d)improper array declaration (Line3)













Ans - c



13)
#include<stdio.h>

void main() {
static int a[5];
int i;
for(i=0;i<=4;i++)
	printf("\n%d",a[i]);
}

a) Some Garbage value

b)
1
1
1
1
1

c)
0
0
0
0
0
d) None of these













Ans- c


14)
#include<stdio.h>
int main() {
	int i;
	char x[]="\0";
	if(printf("%s\n",x))
	  printf("Ok here \n");
	else
	  printf("Forget it\n");
	}


	a)Forget it
	b)Ok here
	c)Error
	d)None of these













Ans- b





15)#include<stdio.h>
void main() {
char b[]="12345\0";
int x = strlen(b);
printf("here in 3 %d\n ", ++x);
}


a)here in 3 3
b)here in 3 6
c)here in 3 9
d)here in 3 5












ans-b



16) class Test {
public static void main(String [] args) {
class Foo {
public int i = 3;
}
Object o=(Object)new Foo(); 
Foo foo = (Foo)o;
System.out.println("i = " +foo.i);
}
}



a) i=3
b) Compilation fails
c) i=5
d) ClassCastException will occur







ans- a


17)

Given:

11. Float pi = new Float(3.14f);
12. if (pi > 3) {
13. System.out.print("pi is bigger than 3. ");
14. }
15. else {
16. System.out.print("pi is not bigger than 3. ");
17. }
18. finally {
19. System.out.println("Have a nice day.");
20. }

What is the result?
A. Compilation fails.
B. pi is bigger than 3.
C. An exception occurs at runtime.
D. pi is bigger than 3. Have a nice day.
E. pi is not bigger than 3. Have a nice day.













Answer: A



18)

Given:

11. public class Test {
12.
13. public static void go(Long n) {System.out.println("Long ");}
14. public static void go(Short n) {System.out.println("Short ");}
15. public static void go(int n) {System.out.println("int ");}
16. public static void main(String [] args) {
17. short y = 6;
18. long z = 7;
19. go(y);
20. go(z);
21. }
22. }

What is the result?

A. int Long
B. Short Long
C. Compilation fails.
D. An exception is thrown at runtime.












Answer: A



19) Given:

11. public class Test {
12. public static void main(String [] args) {
13. int x = 5;
14. boolean b1 = true;
15. boolean b2 = false;
16.
17. if ((x == 4) && !b2 )
18. System.out.print("1 ");
19. System.out.print("2 ");
20. if ((b2 = true) && b1 )
21. System.out.print("3 ");
22. }
23. }

What is the result?
A. 2
B. 3
C. 1 2
D. 2 3
E. 1 2 3
F. Compilation fails.
G. An exception is thrown at runtime.













Answer: D


20)
Given:
42. public class ClassA {
43. public int getValue() {
44.int value=0;
45. boolean setting = true;
46. String title="Hello";
47. if (value || (setting && title == "Hello")) { return 1; }
48. if (value == 1 & title.equals(”Hello”)) { return 2; }
49. }
50. }

And:
70. ClassA a = new ClassA();
71. a.getValue();

What is the result?
A. 1
B. 2
C. Compilation fails.
D. The code runs with no output.
E. An exception is thrown at runtime.
















Answer: C



## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/Quiz%20Mcqs/18th%2BMay%2BMCQ's.txt) · CODING RESOURCES/Quiz Mcqs/18th+May+MCQ's.txt

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
