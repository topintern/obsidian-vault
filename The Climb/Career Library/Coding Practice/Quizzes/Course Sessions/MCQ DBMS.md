---
kind: "study-reference"
title: "MCQ DBMS"
collection: "Course Quizzes"
topic: "Quizzes"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 51 Solutions/MCQ DBMS.pptx"]
tags: ["career/library"]
source_status: "source-reference"
---

# MCQ DBMS

[[The Climb/Career Library/Career Library]]

## Slide 1

MCQ
Relational Algebra

## Slide 2

Suppose (A, B) and (C,D) are two relation schemas. Let r1 and r2 be the corresponding relation instances. B is a foreign key that refers to C in r2. If data in r1 and r2 satisfy referential integrity constraints, which of the following is ALWAYS TRUE?

Answer:(A)
B is a foreign key in r1 that refers to C in r2. r1 and r2 satisfy referential integrity constraints. So every value that exists in column B of r1 must also exist in column C of r2.

## Slide 3

Consider the following relations A, B, C. How many tuples does the result of the following relational algebra expression contain? 
Assume that the schema of A U B is the same as that of A.


Table A
Id   Name    Age
----------------
12   Arun    60
15   Shreya  24
99   Rohit   11



Table B
Id   Name   Age
----------------
15   Shreya  24
25   Hari    40
98   Rohit   20
99   Rohit   11

Table C
Id   Phone  Area
-----------------
10   2200   02  
99   2100   01

A. 7			B. 6 			C. 5				D.9

Result of AUB will be following table
Id   Name    Age
----------------
12   Arun    60
15   Shreya  24
99   Rohit   11
25   Hari    40
98   Rohit   20

The result of given relational algebra expression will be
Id   Name    Age  Id   Phone Area
---------------------------------
12   Arun    60   10   2200   02 
15   Shreya  24   10   2200   02   
99   Rohit   11   10   2200   02 
25   Hari    40   10   2200   02 
98   Rohit   20   10   2200   02 
99   Rohit   11   99   2100   01
98   Rohit   20   99   2100   01

## Slide 4

Let R and S be two relations with the following schema R(P,Q,R1,R2,R3) S(P,Q,S1,S2) Where {P, Q} is the key for both schemas. Which of the following queries are equivalent? 

A. Only I and II
B. Only I and III
C. Only I, II and III
D. Only I, III and IV

Answer (D)
In I, Ps from natural join of R and S are selected.
In III, all Ps from intersection of (P, Q) pairs present in R and S.
IV is also equivalent to III because (R – (R – S)) = R ∩ S.
II is not equivalent as it may also include Ps where Qs are not same in R and S.

## Slide 5

Explanation: 
The Relational Algebra expression in the question above, does 4 operations, step by step ( innermost braces first ) .
1. Select those tuples from relation r which satisfies expression/condition F1, say the result of this  operation is set A.
2. Select those tuples from set A which satisfies expression/condition F2, say the result of this
   operation is set B.
3. Select attrributes set A2 from set B, say the result of this operation is set C.
4. Select attrributes set A1 from set C, say the result is set D which is the final result.
Now to optimize this expression, we can combine operations/steps 1 and 2 by AND operator between F1 and F2 condition, like F1 ^ F2, and instead of selecting first attribute set A2, we can directly select attribute set A1 from the result of the combined operation, which is represented by expression in Option A .

## Slide 6

Consider the relational schema given below, where eId of the relation dependent is a foreign key referring to empId of the relation employee. Assume that every employee has at least one associated dependent in the dependent relation.
employee (empId, empName, empAge)
dependent(depId, eId, depName, depAge) 
Consider the following relational algebra query: 


The above query evaluates to the set of empIds of employees whose age is greater than that of
A. some dependent.
B. all dependents.
C. some of his/her dependents
D. all of his/her dependents.

Explanation: 
The below subquery after the subtraction sign produces id's of those employees who have at least one dependent with age greater than or equal the employee's age.


When the result of above subquery is subtracted from all employees, we get the employees whose age is greater than all dependents.

## Slide 7

Given two union compatible relations R1(A,B) and R2(C,D). What is the result of the operation R1⋈A=C∧ B=D R2    
R1 ∪ R2 
R1 Χ R2 
R1 - R2
R1 ∩ R2

## Slide 8

Consider the following schema :
Sailors (sid, sname, rating, age)
Boats (bid, bname, colour)
Reserves (sid, bid, day)
Two boats can have the same name but the colour differentiates them. The two relations
ρ (Tempsids, (Ⲡ  sid, bid  Reserves)/(Ⲡ bid ( σ bname ='Ganga' Boats))),
Ⲡ sname (Tempsids ⋈ Sailors)
If / is division operation, the above set of relations represents the query

A. Names of sailors who have reserved all boats called Ganga
B. Names of sailors who have not reserved any Gangaboat
C. Names of sailors who have reserved at least one Gangaboat
D. Names of sailors who have reserved at most one Ganga boat

Explanation: 
According to Division operator, Tempsids gives sid and bid of who have reserved all boats called Ganga And Ⲡ sname (Tempsids ⋈ Sailors) will return sname of sailors who have reserved all boats called Ganga So, option (A) is correct.

## Slide 9

Given the relations employee (name, salary, dept-no), and department (dept-no, dept-name,address) Which of the following queries cannot be expressed using the basic relational algebra operations (σ, π, x, -, ∪, p)

A. Department address of every employee
B. Employees whose name is the same as their department name
C. The sum of all employees' salaries
D. All employees of a given department

Explanation: 
The sum of all employees' salaries can not be found using these above operations as to calculate sum we need aggregate functions and operators. So, option (C) is correct.

## Slide 10

Suppose database table T1(P, R) currently has tuples {(10, 5), (15, 8), (25, 6)} and table T2 (A, C) currently has {(10, 6), (25, 3), (10, 5)}. Consider the following three relational algebra queries RA1, RA2 and RA3: 
RA1 : T1 ⨝ T1.P = T2.A T2 where ⨝is natural join symbol 
RA2 : T1 ⟕ T1.P = T2.A T2 where ⟕ is left outer join symbol 
RA3 : T1 ⨝ T1.P = T2.A and T1.R = T2.C T2 
The number of tuples in the resulting table of RA1, RA2 and RA3 are given by:
A. 2, 4, 2 respectively
B. 2, 3, 2 respectively
C. 3, 3, 1 respectively
D. 3, 4, 1 respectively

Explanation:  Option D is Correct
RA1 : T1 ⨝ T1.P = T2.A T2 where ⨝is natural join symbol. It will result 3 tuples:
P = 	A	R	C
	10	5	6
	10	5	5
	25	6	3
RA2 : T1 ⟕ T1.P = T2.A T2 where ⟕ is left outer join symbol. It will result in 4 tuples.
P = 	A	R	C
	10	5	6
	10	5	5
	15	8	Null
	25	6	3
RA3 : T1 ⨝ T1.P = T2.A and T1.R = T2.CT2. It will result in 1 tuple.
P = 	A	R = C
	10	5

## Slide 11

Which of the following query transformations (i.e., replacing the l.h.s. expression by the r.h.s. expression) is incorrect? R1 and R2 are relations. C1, C2 are selection conditions and A1, A2 are attributes of R1. 
a.  σC1( σC2R1)) → σC2(σC1(R1)) 
b.  σC1( πA1R1)) → πA1(σC1(R1)) 
c.  σC1( R1 ∪ R2 ) → σC1(R1) ∪ σC1(R2) 
d.  πA1(σC1(R1)) → σC1 (πA1 (R1))

Explanation: 
D is the answer. If the selection condition c1 is on attribute A2, then we can not replace LHS expression by RHS expression. In RHS first projection is on A1 then selection condition c1 will fail because no A2 will be present there.

## Deck conversion

Slide text, tables, and speaker notes are preserved. Review the original deck for slide layout and non-text visuals.

## Source provenance

- [Original PPTX](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2051%20Solutions/MCQ%20DBMS.pptx) · CODING RESOURCES/ELITE FS COMPLETE/Day 51 Solutions/MCQ DBMS.pptx

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
