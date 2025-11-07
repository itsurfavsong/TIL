# 🧩 JOIN Statements

A JOIN combines data from two or more tables into a single result set. <br>

1. INNER JOIN
Returns only the records that have matching values in both tables. <br>
You specify the join condition using the ON keyword (similar to a WHERE condition).
```sql
SELECT 
	emp.emp_id,
	emp.name,
	sal.salary
FROM employees emp	
	JOIN salaries sal
		ON emp.emp_id = sal.emp_id
			AND sal.end_at IS NULL
ORDER BY emp.emp_id ASC;
```
💡 Note: <br>
You could also use WHERE sal.end_at IS NULL instead of adding it in the ON clause.

Example: Display currently employed workers’ ID, name, birth date, and department name <br>
The left table (department_emps) is the base in this case.
```sql
SELECT 
	depe.emp_id,
	emp.name,
	emp.birth,
	dept.dept_code,
	dept.dept_name
FROM department_emps depe
	JOIN departments dept
		ON depe.dept_code = dept.dept_code
	JOIN employees emp
		ON depe.emp_id = emp.emp_id
			AND emp.fire_at IS NULL
WHERE 
	depe.end_at IS NULL;
```
---
2. LEFT JOIN <br>
Returns all rows from the left table, and the matched rows from the right table. <br>
If there is no match, the result is NULL.
```sql
SELECT 
	emp.emp_id,
	emp.name,
	sal.salary
FROM employees emp
	LEFT JOIN salaries sal
		ON emp.emp_id = sal.emp_id
			AND sal.end_at IS NULL;
```
💡 Note: <br>
When there’s no corresponding record in salaries, the salary column will show NULL.

---
3. UNION and UNION ALL
Used to combine the results of two or more SELECT statements. <br>
UNION → removes duplicate rows <br>
UNION ALL → keeps duplicates
```sql
SELECT 
	emp.emp_id AS junior_id,
	emp.name AS junior_name,
	supemp.emp_id AS supervisor_id,
	supemp.name AS supervisor_name
FROM employees emp
	JOIN employees supemp
		ON emp.sup_id = supemp.emp_id
WHERE 	
	emp.emp_id = 98415;
```
---
**👇️Practical Tip** <br>

When designing databases: <br>
- Try to normalize data to reduce redundancy by splitting one big messy table <br>
into smaller, related tables, and connecting them with foreign keys. <br>
- But be aware that too many JOINs can slow down queries. <br>
- In most cases, limit JOINs to 3 tables or fewer for performance and readability.
