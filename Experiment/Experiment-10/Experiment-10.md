# SQL Subqueries: Find the 2nd and 3rd Highest Salaries

## 10.1 Question

Write SQL queries using **subqueries** to find the second-highest and third-highest distinct salaries from the `employee` table.

Assume the table contains a column named `salary`.

## 10.1.1 Query to Find the Second-Highest Salary

```sql
SELECT MAX(salary) AS second_highest_salary
FROM employee
WHERE salary < (
    SELECT MAX(salary)
    FROM employee
);
```

## 10.1.2 Query to Find the Third-Highest Salary

```sql
SELECT MAX(salary) AS third_highest_salary
FROM employee
WHERE salary < (
    SELECT MAX(salary)
    FROM employee
    WHERE salary < (
        SELECT MAX(salary)
        FROM employee
    )
);
```


## 10.2 Find Food Items Costing More Than the Average Cost

**Problem Link:** https://www.codechef.com/learn/course/sql-intermediate/SQ00BS04/problems/GSQ71

### SQL Query

```sql
SELECT f_name, f_cost, f_type
FROM food
WHERE f_cost > (
    SELECT AVG(f_cost)
    FROM food
);
```


## 10.3 Find Food Items with an Average Rating of at Least 4

**Problem Link:** https://www.codechef.com/learn/course/sql-intermediate/SQ00BS04/problems/GSQ74?tab=statement

### SQL Query

```sql
SELECT f_name, f_cost, f_type
FROM food
WHERE f_id IN (
    SELECT f_id
    FROM ratings
    GROUP BY f_id
    HAVING AVG(f_rating) >= 4
);
```
