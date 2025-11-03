# 🧩 SQL Basic Query (2)

LIKE operator: Retrieve data by pattern matching <br>
% : matches any number of characters <br>
\_ : matches exactly one character <br>
Retrieve employees whose names end with ‘james’

```sql
SELECT *
FROM employees
WHERE
	name LIKE '%james';
```

---

Retrieve employees whose name pattern matches ‘garbie\_\_’

```sql
SELECT *
FROM employees
WHERE
	name LIKE 'garbie__';
```

---

Retrieve employees whose names match the pattern ‘%hi\_’

```sql
SELECT *
FROM employees
WHERE
	name LIKE '%hi_';
```

---

ORDER BY clause: Sort data <br>
ASC = ascending order <br>
DESC = descending order

```sql
SELECT *
FROM employees
ORDER BY name ASC, birth ASC;
```

---

Retrieve employees hired after 2000, sorted by name and birthdate:

```sql
SELECT *
FROM employees
WHERE
	hire_at >= '2000-01-01'
ORDER BY
	name ASC,
	birth ASC;
```

---

Retrieve female employees who are still working, sorted by name and birthdate:

```sql
SELECT *
FROM employees
WHERE
	gender = 'F'
	AND fire_at IS NULL
ORDER BY
	name ASC,
	birth ASC;
```

---

DISTINCT keyword: Remove duplicate rows

```sql
SELECT DISTINCT name, birth
FROM employees
ORDER BY name ASC;
```

---

GROUP BY clause: Group and summarize data <br>
Aggregate functions <br>
MAX() – Maximum value <br>
MIN() – Minimum value <br>
COUNT() – Count of rows <br>
AVG() – Average value <br>
SUM() – Sum of values <br>
Retrieve the highest salary per employee:

```sql
SELECT
	emp_id,
	MAX(salary) AS max_salary
FROM salaries
GROUP BY emp_id;
```

Retrieve employees whose highest salary is 50,000,000 or higher:

```sql
SELECT
	emp_id,
	MAX(salary) AS max_salary
FROM salaries
GROUP BY emp_id
HAVING max_salary >= 50000000;
```

Count employees by gender:

```sql
SELECT
	gender,
	COUNT(gender) AS count_gender
FROM employees
GROUP BY gender;
```

---

LIMIT and OFFSET: Restrict the number of rows returned <br>
Retrieve the first 10 employees sorted by employee ID:

```sql
SELECT *
FROM employees
ORDER BY emp_id ASC
LIMIT 10;
```

Pagination example — skip the first 5 and retrieve the next 5 rows:

```sql
SELECT *
FROM employees
WHERE fire_at IS NOT NULL
ORDER BY emp_id ASC
LIMIT 5 OFFSET 5;
```

---

ex) Retrieve top 5 currently highest-paid employees

```sql
SELECT
	sal_id,
	emp_id,
	salary
FROM salaries
WHERE end_at IS NULL
ORDER BY salary DESC
LIMIT 5;
```

---

Basic structure of a SELECT statement

```sql
SELECT [DISTINCT] [column_name]
FROM [table_name]
WHERE [conditions]
GROUP BY [column_name] HAVING [aggregate_function_condition]
ORDER BY [column_name ASC | column_name DESC]
LIMIT [n] OFFSET [n];
```
