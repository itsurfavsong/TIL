# 🧩 Subquery

A **subquery** is a query nested inside another SQL statement.  
It’s often used inside `WHERE`, `FROM`, or `SELECT` clauses to filter or compute results dynamically.

---

📍Used in the WHERE clause <br>
Because there is an "=" operator, it must be a one-to-one match. <br>
Therefore, if the subquery returns multiple results (1-to-many), <br>
you must use "IN" instead.

[example] Print the employee ID and name of the manager of department D001.

```sql
SELECT 
	emp.emp_id,
	emp.`name`
FROM employees AS emp
WHERE 
	emp.emp_id = (
		SELECT 
			depm.emp_id
		FROM department_managers AS depm
		WHERE 	
			depm.end_at IS NULL
			AND depm.dept_code = 'D001'
	);

```
---

🔁 Multi-row Subquery <br>
When the subquery returns two or more rows, <br>
you must use multi-row comparison operators such as: <br>
IN, ALL, ANY, SOME, EXISTS, etc.

```sql
SELECT 
	emp.emp_id,
	emp.`name`
FROM employees AS emp
WHERE
	emp.emp_id IN (
		SELECT 
			depm.emp_id
		FROM department_managers AS depm
		WHERE 	
			depm.end_at IS NULL
	);
```
---

🧮 Multi-column Subquery <br>
(JOIN is usually preferred.) <br>
When the subquery returns multiple columns, <br>
it can compare multiple conditions at once with the main query. 

[example] Get the joining date of the current manager of department D002.

```sql
SELECT
	department_emps.*
FROM department_emps
WHERE 
	(department_emps.emp_id, department_emps.dept_code) IN (
		SELECT 
			department_managers.emp_id,
			department_managers.dept_code
		FROM department_managers
		WHERE
			department_managers.dept_code = 'D002'
			AND department_managers.end_at IS NULL
	);
```
---

🔗 Correlated Subquery <br>
A correlated subquery references a column from the outer (main) query. <br>

[example] Print information of employees who have ever held a manager position.

```sql
SELECT 
	employees.*
FROM employees
WHERE 	
	employees.emp_id IN (
		SELECT department_managers.emp_id
		FROM department_managers
		WHERE 
			department_managers.emp_id = employees.emp_id
	);
```
