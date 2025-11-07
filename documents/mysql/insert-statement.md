# 🧩 INSERT Statement

Used to add new records to a table.
```sql
INSERT INTO employees(
	name,
	birth,
	gender,
	hire_at,
	fire_at,
	sup_id,
	created_at,
	updated_at,
	deleted_at	
)
VALUES(
	'송보미',
	'1993-02-04',
	'F',
	'2025-10-21',
	NULL,
	NULL,
	NOW(),
	NOW(),
	NULL
);
```
```sql
INSERT INTO salaries(
	emp_id,
	salary,
	start_at,
	end_at,
	created_at,
	updated_at,
	deleted_at
)
VALUES (
	'100005',
	'1000000000',
	'2025-10-21',
	NULL,
	NOW(),
	NOW(),
	NULL
);
```
---
**INSERT Using SELECT** <br>

You can insert new data into one table using values selected from another.
```sql
INSERT INTO salaries (
	emp_id,
	salary,
	start_at
)
SELECT 
	emp_id,
	30000000,
	created_at
FROM employees
WHERE 
	emp_id = '100005'
	AND name = '송보미';
```


