# 🧩 SQL Basic Query (1)

Retrieve all columns from a table
```sql
SELECT * 
FROM employees;
```
---
Retrieve specific columns
```sql
SELECT 
	name,
	birth,
	hire_at
FROM employees;
```
---
WHERE clause: Retrieve data that matches a specific column value
```sql
SELECT *
FROM employees
WHERE
	emp_id = 5;
```
ex) Retrieve an employee whose name is ‘강영화’ and gender is ‘M’
```sql
SELECT *
FROM employees
WHERE 
	name = '강영화'
	AND gender = 'M';
```
---
Filter by date
```sql
SELECT *
FROM employees
WHERE 
	hire_at >= '2023-01-01';
```
---
Retrieve only employees who are still working (NULL check)
```sql
SELECT *
FROM employees
WHERE 
	fire_at IS NULL;
```
---
Using AND and OR together in a WHERE clause
ex) Retrieve employees who were hired after 2025-01-01 or before 2000-01-01, <br>
and have already left the company.
```sql
SELECT *
FROM employees
WHERE 
	(
		hire_at >= '2025-01-01'
		OR hire_at <= '2000-01-01'
	)
	AND fire_at IS NOT NULL;
```
---
BETWEEN operator: Retrieve data within a specific range
```sql
SELECT *
FROM employees
WHERE 
	emp_id BETWEEN 10000 AND 10010;
```
Equivalent to:
```sql
SELECT *
FROM employees
WHERE 
	emp_id >= 10000
	AND emp_id <= 10010;
```
---
IN operator: Retrieve data that matches one of several values
```sql
SELECT *
FROM employees 
WHERE 
	emp_id IN (5, 7, 9, 12);
```
Equivalent to:
```sql
SELECT *
FROM employees
WHERE
	emp_id = 5
	OR emp_id = 7
	OR emp_id = 9
	OR emp_id = 12;
```
