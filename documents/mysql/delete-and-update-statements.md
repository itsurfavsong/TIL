# 🧩 SQL delete and update statements

1. DELETE Statement <br>

Used to delete specific records from a table.

```sql
DELETE FROM salaries
WHERE 
	emp_id = 100005;
```
```sql
DELETE FROM employees
WHERE 
	emp_id = 100005;
```
---
2. UPDATE Statement <br>

Used to modify existing data in a table.
```sql
UPDATE salaries
SET 
	salary = 35000000
WHERE 
	sal_id = 1022179;
```
