---
kind: "coding-problem"
title: "Queries And Answers (Day 22)"
collection: "Course Practice"
topic: "Mixed Practice"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/ELITE FS COMPLETE/Day 22/Queries and Answers.txt"]
practice_status: "not-started"
last_practiced: null
source_solution_available: false
statement_available: true
topic_basis: "title-inference"
tags: ["career/library","coding/practice"]
---

# Queries And Answers (Day 22)

[[The Climb/Career Library/Coding Practice/Coding Practice]] · [[The Climb/Career Library/Coding Practice/Course Practice/Course Practice]]

## Source problem and examples

Query-1:
List the employees who are senior to their own manager


### Sample Output 

empno 	ename 	mgr 	hiredate 	mgrempo 	mgrename 	mgrhiredate 	
7369 	SMITH 	7902 	1980-12-17 	7902 		FORD 		1981-12-03

Note : Order by empno(ascending)

Answer:
-------------
select e.empno, e.ename, e.mgr, e.hiredate, m.empno as mgrempo, m.ename as
mgrename, m.hiredate as mgrhiredate from emp e
inner join emp m on e.mgr = m.empno and e.hiredate < m.hiredate
ORDER BY `e`.`empno` ASC


Query-2:
/*
Find all the names and salary of the employees who earn the minimum Salary for each job wise in ascending
order of their sal.
*/
Answer:
----------
select ename,sal from emp where sal in (select min(sal) from emp group by job)
order by sal asc;

Query-3:
/*
List the manager names who are senior to KING and who are junior to SMITH
*/

Answer:
-----------
select ename from emp where empno in (select mgr from emp where
hiredate < (select hiredate from emp where ename = 'king' ) and
hiredate > (select hiredate from emp where ename = 'smith'))
and mgr is not null;


Query-4:
/*
Display employee(s) empno,name,salary,dept number who are earning the grade 4 salary and working in
CHICAGO  or NEW YORK order by dept number in ascending order.


### Sample Output

EMPNO 	ENAME 	SAL 		DEPTNO  	
7782 	CLARK 	2450.00 	10

*/
Answer:
-----------
SELECT EMPNO, ENAME, SAL, DEPTNO FROM emp WHERE DEPTNO in 
(
SELECT DEPTNO FROM dept WHERE LOC='CHICAGO' or LOC='NEW YORK'
) AND SAL in (SELECT SAL FROM emp WHERE SAL BETWEEN 
		(SELECT LOSAL FROM salgrade WHERE GRADE=4) 
		AND (SELECT HISAL FROM salgrade WHERE GRADE=4)
	     ) 
order by deptno asc

Query-5:
/*
List the employee number, name, designation, salary, manager number,
dept number, name, and salary grade of the all the employees. Sort employee names in ascending order
*/
Answer:
----------
select e.empno, e.ename, e.job, e.mgr, e.sal, s.grade, d.loc, d.dname
from emp e inner join dept d on e.deptno = d.deptno
inner join
salgrade s on e.sal between s.losal and s.hisal order by e.ename

## My practice

### Approach and invariant

### Tests and edge cases

### Complexity

### Review notes

## Source provenance

- [Original TXT](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/ELITE%20FS%20COMPLETE/Day%2022/Queries%20and%20Answers.txt) · CODING RESOURCES/ELITE FS COMPLETE/Day 22/Queries and Answers.txt
