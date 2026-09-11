6.1


DROP TABLE employees;
DROP TABLE employees CASCADE;
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(100) NOT NULL,
    emp_salary DECIMAL(10, 2) NOT NULL,
      emp_city VARCHAR(100) NOT NULL
);

INSERT INTO employees (emp_id, emp_name, emp_salary, emp_city) VALUES
(101, 'Amit Sharma', 85000.00, 'Mumbai'),
(102, 'Priya Patel', 95000.00, 'Mumbai'),
(103, 'Rahul Verma', 60000.00, 'Delhi'),
(104, 'Ananya Iyer', 110000.00, 'Bangalore'),
(105, 'Vikram Singh', 55000.00, 'Delhi'),
(106, 'Sneha Reddy', 105000.00, 'Bangalore'),
(107, 'Rohan Das', 72000.00, 'Kolkata')



SELECT * FROM employees

CREATE OR REPLACE VIEW EMP_VIEW_617A AS
SELECT EMP_ID , EMP_NAME FROM employees
WHERE EMP_ID=101

SELECT * FROM EMP_VIEW_617A 

 
DELETE FROM EMP_VIEW_617A
WHERE EMP_ID=101



6.2

DROP TABLE employees;
DROP TABLE employees CASCADE;
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(100) NOT NULL,
    emp_salary DECIMAL(10, 2) NOT NULL,
      emp_city VARCHAR(100) NOT NULL
);

INSERT INTO employees (emp_id, emp_name, emp_salary, emp_city) VALUES
(101, 'Amit Sharma', 85000.00, 'Mumbai'),
(102, 'Priya Patel', 95000.00, 'Mumbai'),
(103, 'Rahul Verma', 60000.00, 'Delhi'),
(104, 'Ananya Iyer', 110000.00, 'Bangalore'),
(105, 'Vikram Singh', 55000.00, 'Delhi'),
(106, 'Sneha Reddy', 105000.00, 'Bangalore'),
(107, 'Rohan Das', 72000.00, 'Kolkata')



SELECT * FROM employees

CREATE MATERIALIZED VIEW EMP_VIEW_617A_MV AS
SELECT EMP_ID , EMP_NAME FROM employees
WHERE EMP_ID=101
WITH NO DATA 

SELECT * FROM EMP_VIEW_617A_MV

-- 
REFRESH MATERIALIZED VIEW  EMP_VIEW_617A_MV