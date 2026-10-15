---
kind: "study-reference"
title: "DATA ANALYST CRASH COURSE"
collection: "SQL and Databases"
topic: "SQL and Databases"
imported: "2026-10-13"
source_files: ["INTERVIEW PREP NOTES/DATA ANALYST CRASH COURSE.docx"]
tags: ["career/library"]
source_status: "source-reference"
---

# DATA ANALYST CRASH COURSE

[[The Climb/Career Library/Career Library]]

			   **DATA ANALYST CRASH COURSE**

## SQL

A database is a structured collection of data that is stored and managed in a way that allows for efficient retrieval, manipulation, and storage of the data.

- **GROUP BY**

- The GROUP BY statement is used to arrange identical data into groups. This can be particularly useful when combined with aggregate functions like COUNT (), SUM(), AVG(), MAX(), and MIN(), as it allows you to perform calculations on each group of data separately.

- 

- **SELECT column1, ****aggregate_function****(column2)**

- **FROM ****table_name**

- **WHERE condition**

- **GROUP BY column1;**

- 

- •	Columns in the SELECT clause that are not used in aggregate functions must be included in the GROUP BY clause.

- •	You can group by multiple columns by listing them in the GROUP BY clause, separated by commas.

- id | product | quantity | price

- ---|---------|----------|------

-  1 | Apple   |       10 |   1.5

-  2 | Banana  |       15 |   1.2

-  3 | Apple   |        5 |   1.5

-  4 | Orange  |       20 |   1.3

-  5 | Banana  |       10 |   1.2

- Group by product

- If you want to know the total quantity sold for each product, you can use the GROUP BY statement with the SUM aggregate function:

- 

- SELECT product, SUM(quantity) as total_quantity

- FROM sales

- GROUP BY product;

- The result will be:

- 

- product | total_quantity

- --------|----------------

- Apple   |             15

- Banana  |             25

- Orange  |             20

- 

- **HAVING**

- 

- Suppose in the below query

- 

- SELECT product, SUM(quantity) as total_quantity

- FROM sales

- WHERE SUM(quantity) > 15

- GROUP BY product;

- 

- Will fail, because because we are trying to filter by the aggregate column before the result is formed using GROUP BY.

- 

- This is precisely what HAVING was made for

- 

- SELECT product, SUM(quantity) as total_quantity

- FROM sales

- WHERE quantity > 5

- GROUP BY product

- HAVING SUM(quantity) > 15;

- 

- WHERE is used to filter non-aggregated data / (rows before any groupings are made). 

- HAVING is used to filter aggregated data / (groups after the GROUP BY clause has been applied).

- 

- **LIMIT**

- 

- You know how LIMIT works normally, so some other cases with it is:

- 

- SELECT * 

- FROM employee_demographics 

- ORDER BY age DESC

- LIMIT 2, 1;

- 

- What this does is selects 2nd row of result and returns 1 row after it so it basically returns the 3rd row of result (like 3rd highest age)

- 

- If you do 2,2 it returns 2 records after 2nd row i.e 3rd and 4th highest ages

- 

- Offsetting with OFFSET: The OFFSET 1 clause skips the first row and starts returning rows from the second one.

- 

- SELECT name, department, salary 

- FROM employees 

- ORDER BY salary DESC 

- LIMIT 3 OFFSET 1;

	So starts from the second row and returns top 3 (2,3,4)

- **JOINS**

- 

- By default, JOIN is INNER JOIN, can also mention explicit INNER

- 

- Returns rows which have same values in the matching columns that we tie on

- 

- SELECT *

- FROM employee_demographics dem

- INNER JOIN employee_salary sal

- 	ON dem.employee_id = sal.employee_id;

- 

- **LEFT** or **LEFT OUTER JOIN**

- 

- Returns all the records from the left and only the matching records from the right

-  SELECT *

- FROM employee_demographics dem

- LEFT JOIN employee_salary sal

- 	ON dem.employee_id = sal.employee_id;

- 

- **Similar with RIGHT JOIN**

- 

- **SELF JOIN**

- 

- SELECT *

- FROM employee_salary emp1

- JOIN employee_salary emp2

- 	ON emp1.employee_id +1 = emp2.employee_id;

- 

- Self-join where each is assigned to next employee id

- 

- **JOINING MULTIPLE TABLES**

- 

- SELECT *

- FROM employee_demographics dem

- INNER JOIN employee_salary sal

- 	ON dem.employee_id = sal.employee_id

- INNER JOIN parks_departments pd

- ON sal.dept_id = pd.department_id;

## Source provenance

- [Original DOCX](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/INTERVIEW%20PREP%20NOTES/DATA%20ANALYST%20CRASH%20COURSE.docx) · INTERVIEW PREP NOTES/DATA ANALYST CRASH COURSE.docx

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
