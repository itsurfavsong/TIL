[How Syntax order and Execution order work at MySQL]

Syntax order -> Execution order

- Syntax Order

1. SELECT

2. FROM

3. WHERE

4. GROUP BY

5. HAVING

6. ORDER BY

- Execution Order

1. FROM → Go to the location where the data exists

2. WHERE → Filter only the data that meets the conditions

3. GROUP BY → Aggregate the data as desired

4. HAVING → Filter the aggregated data based on conditions

5. SELECT → Retrieve the final data

6. ORDER BY → Sort the result

[How Aliases work]

If a table alias is defined in the FROM clause (e.g., FROM Table1 AS T1),
it can be used in the SELECT and ORDER BY clauses (e.g., SELECT T1.Col1, ORDER BY T1.Col1).

If a column alias is defined in the SELECT clause (e.g., SELECT T1.Col1 AS TC),
it can be used in the ORDER BY clause (e.g., ORDER BY TC).

Note that T1.TC cannot be used in ORDER BY; cause TC replaces T1.Col1
