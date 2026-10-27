# PostgreSQL Stored Procedure — Update Employee Salary

## 1. Create Employee Table

```sql
CREATE TABLE EMPLOYEE (
    EMP_ID INT PRIMARY KEY,
    EMP_NAME VARCHAR(100),
    SALARY NUMERIC(10,2)
);
```

---

## 2. Insert Employee Data

```sql
INSERT INTO EMPLOYEE (EMP_ID, EMP_NAME, SALARY)
VALUES
(201, 'Amit', 40000),
(202, 'Rahul', 35000),
(203, 'Priya', 45000);
```

---

## 3. Create Stored Procedure

```sql
CREATE OR REPLACE PROCEDURE UPDATE_SAL_PROC2(
    IN P_EMPID INT,
    OUT STATUS VARCHAR(20),
    IN OUT P_SALARY NUMERIC
)
AS $$

DECLARE
    CURRENT_SAL NUMERIC(10,2);
BEGIN

    SELECT SALARY INTO CURRENT_SAL
    FROM EMPLOYEE
    WHERE EMP_ID = P_EMPID;

    IF NOT FOUND THEN
        RAISE EXCEPTION 'EMPLOYEE NOT FOUND';
    END IF;

    P_SALARY := CURRENT_SAL + P_SALARY;

    UPDATE EMPLOYEE
    SET SALARY = P_SALARY
    WHERE EMP_ID = P_EMPID;

    STATUS := 'Success';

END;

$$ LANGUAGE PLPGSQL;
```

---

## 4. Call the Procedure

```sql
CALL UPDATE_SAL_PROC2(201, NULL, 5208);
```

---

## 5. Verify Updated Salary

```sql
SELECT * FROM EMPLOYEE;
```
