# 🧩 SQL functions (2)

1. Data Type Conversion Functions <br>

1-1. CAST (old version) and CONVERT (new version) mean convert the number 1234 into a character string of fixed length 4.

```sql
SELECT
	1234,
	CAST(1234 AS CHAR(4)),
	CONVERT(1234, CHAR(4));
```

---

2. Control Flow Functions

2-1. IF(condition, value_if_true, value_if_false)<br>

- Used to perform conditional branching.

Example: If gender is M, return “남자 (Male)”; otherwise, “여자 (Female)”.

```sql
SELECT
	emp_id,
	name,
	IF(gender = 'M', '남자', '여자') AS ko_gender
FROM employees;
```

Equivalent to (Case expression):

```sql
SELECT *
FROM employees
WHERE
	name LIKE '%hi_';
```

2-2. IFNULL(expression1, expression2) <br>

Returns expression2 if expression1 is NULL. <br>
Otherwise, returns expression1.

```sql
SELECT
	emp_id,
	IFNULL(end_at, '9999-12-31') AS ifnull_end_at
FROM title_emps;
```

2-3. NULLIF(expression1, expression2) <br>

Returns NULL if the two expressions are equal. (expression1 = expression2)<br>
Otherwise, returns expression1.

```sql
SELECT
	emp_id,
	name,
	NULLIF(gender, 'F') AS nullif_gender
FROM employees;
```

---

3. String Functions <br>

3-1. CONCAT(string1, string2, …) <br>
Concatenates multiple strings.

```sql
SELECT CONCAT('Hello, ', 'Database!');
SELECT CONCAT(gender, name)
FROM employees;
```

3-2. CONCAT_WS(separator, string1, string2, …) <br>
Concatenates strings with a separator.

```sql
SELECT CONCAT_WS(', ', 'Strawberry', 'Kiwi', 'Watermelon');
```

3-3. FORMAT(number, decimal_places) <br>
Returns a number as a formatted string with commas and decimal places.

```sql
SELECT FORMAT(314595675, 8);
```

3-4. LEFT(string, length) and RIGHT(string, length) <br>
Extracts characters from the left or right side of a string.

```sql
SELECT LEFT('abcdef', 2);
SELECT RIGHT('abcdef', 2);
```

3-5. UPPER(string) / LOWER(string)

```sql
SELECT UPPER('AbCde'), LOWER('AbCde');
```

3-6. LPAD(string, length, pad_string) / RPAD(string, length, pad_string) <br>
Pads the left or right side of a string to the specified total length.

```sql
SELECT LPAD('1', 4, '0'), RPAD('1', 4, '0');
```

3-7. TRIM(string), RTRIM(string), LTRIM(string) <br>
Removes whitespace from both sides, right side, or left side of a string.

```sql
SELECT
	TRIM('     trim  '),
	RTRIM('     trim  '),
	LTRIM('     trim  ');
```

3-8. TRIM([direction] substring FROM string) <br>
Removes a specific substring from one or both sides of a string.

Directions:
LEADING – left side
TRAILING – right side
BOTH – both sides

Example: remove "Bearer " prefix.

```sql
SELECT TRIM(LEADING 'Bearer ' FROM 'Bearer dfkajldsfjafjksdjalfkjds');
```

3-9. SUBSTRING(string, start_position, length) <br>
Extracts a substring starting from a position.

```sql
SELECT SUBSTRING('abcdef', 3, 2);
```

3-10. SUBSTRING_INDEX(string, delimiter, count) <br>
Returns a substring from the string before (or after, if count < 0) the nth occurrence of the delimiter.

```sql
SELECT SUBSTRING_INDEX('your_fav_song', '_', 2);
```

---

4. Mathematical Functions

CEILING(x) - Rounds up
FLOOR(x) - Rounds down
ROUND(x) - Rounds to nearest integer

```sql
SELECT CEILING(1.2), FLOOR(1.9), ROUND(1.5);
```

4-1. TRUNCATE(number, decimal_places) <br>
Cuts off digits after the specified number of decimal places.

```sql
SELECT TRUNCATE(3.14847895, 2);
```

---

5. Date and Time Functions
   5-1. NOW() <br>
   Returns the current date and time (YYYY-MM-DD HH:mm:ss).

```sql
SELECT NOW();
```

5-2. DATE(datetime) <br>
Converts a datetime value to a date (YYYY-MM-DD).

```sql
SELECT DATE(NOW());
```

5-3. ADDDATE(date, INTERVAL number unit) <br>
Adds (or subtracts, if negative) an interval to a date.

```sql
SELECT ADDDATE(NOW(), INTERVAL 1 YEAR);
SELECT ADDDATE(NOW(), INTERVAL -2 YEAR);
```

---

6. Aggregate Functions <br>

6-1. Common Aggregate Functions
SUM(column) - Total sum
MAX(column) - Maximum value
MIN(column) - Minimum value
COUNT(column) - Number of non-null records
AVG(column) - Average value

```sql
SELECT
	SUM(salary),
	MAX(salary),
	MIN(salary),
	COUNT(salary),
	AVG(salary)
FROM salaries;
```

- Notes on COUNT
  COUNT(\*) → Counts all rows (includes NULL)
  COUNT(column) → Counts only non-null rows

```sql
SELECT COUNT(*), COUNT(end_at)
FROM salaries;
```

---

7. Ranking Functions
   7-1. RANK() OVER(ORDER BY column ASC/DESC) <br>
   Assigns ranks based on a column’s order. <br>
   Tied values receive the same rank.

```sql
SELECT
	emp_id,
	salary,
	RANK() OVER(ORDER BY salary ASC) AS sal_rank
FROM salaries
LIMIT 5;
```

7-2. ROW_NUMBER() OVER(ORDER BY column ASC/DESC) <br>
Assigns a unique sequential number to each row, even for tied values.

```sql
SELECT
	emp_id,
	salary,
	ROW_NUMBER() OVER(ORDER BY salary ASC) AS sal_rank
FROM salaries;
```
