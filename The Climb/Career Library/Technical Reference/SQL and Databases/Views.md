---
kind: "study-reference"
title: "Views"
collection: "SQL and Databases"
topic: "SQL and Databases"
imported: "2026-10-13"
source_files: ["CODING RESOURCES/c++ material/views.sql"]
tags: ["career/library"]
source_status: "source-reference"
---

# Views

[[The Climb/Career Library/Career Library]]

```sql
# -----------------------------------------

use test;

DROP VIEW IF EXISTS empDetails;

CREATE VIEW empDetails AS
SELECT 
    empno, ename, job, deptno, count(job) as total 
FROM
    emp
GROUP by job
ORDER BY ename;

select * from empDetails;

# -----------------------------------------

DROP VIEW IF EXISTS empDept;

CREATE or REPLACE VIEW empDept AS
  select emp.empno, emp.ename, dept.dname, emp.job
  from emp
  inner join dept
  on emp.deptno=dept.deptno
  ORDER BY ename;

select * from empDept;

-- Show Create View empDept;

Alter view empDept
As
  select emp.empno, emp.ename, dept.dname
  from emp
  inner join dept
  on emp.deptno=dept.deptno;

select * from empDept;


DROP VIEW IF EXISTS empDetails;

CREATE VIEW empDetails AS
SELECT 
    empno, ename, job, deptno 
FROM
    emp;

select * from empDetails;

desc information_schema.views;

select * from information_schema.views where
TABLE_SCHEMA = 'test';

Select table_schema, table_name, is_updatable from information_schema.views where
TABLE_SCHEMA = 'test';

DROP VIEW IF EXISTS empDetails2;

CREATE VIEW empDetails AS
SELECT 
    empno, ename, job, deptno 
FROM
    emp;

select * from empDetails2;
```

## Source provenance

- [Original SQL](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/CODING%20RESOURCES/c%2B%2B%20material/views.sql) · CODING RESOURCES/c++ material/views.sql

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
