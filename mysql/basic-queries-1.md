# 🧩 SQL Basic Query (1)

1. SELECT clause

Retrieve all columns from a table (All data)
```sql
SELECT * 
FROM employees;
```
Retrieve specific columns (selecting some of columns)
```sql
SELECT 
	name,
	birth,
	hire_at
FROM employees;
```
---
2. WHERE clause: Retrieve data that matches a specific column value (shows who got that emp_id)
```sql
SELECT *
FROM employees
WHERE
	emp_id = 5;
```
Retrieve an employee whose name is ‘jennie’ and gender is ‘F’
```sql
SELECT *
FROM employees
WHERE 
	name = 'jennie'
	AND gender = 'F';
```
---
2-1. Filter by date
```sql
SELECT *
FROM employees
WHERE 
	hire_at >= '2023-01-01';
```
---
2-2. Retrieve only employees who are still working (NULL check) ('fire_at is null' means someone hasn't quit and still be at work)
```sql
SELECT *
FROM employees
WHERE 
	fire_at IS NULL;
```
---
2-3. Using AND and OR together in a WHERE clause <br>

Retrieve employees who were hired after 2025-01-01 or before 2000-01-01, and have already left the company.
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
2-4. BETWEEN operator: Retrieve data within a specific range (YYYY-MM-DD ~ YYYY-MM-DD)
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
2-5. IN operator: Retrieve data that matches one of several values (you can use 'IN' for collecting multiple numbers)
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
