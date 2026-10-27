**Question 9.1:** Implement a Row-Level BEFORE UPDATE Trigger on the `Salary_Hike` table that restricts a salary increase to no more than 15% of the `:OLD.salary` value. If the increase exceeds this limit, the trigger must raise a custom user-defined exception with a specific message.

## SQL Code

```sql
CREATE OR REPLACE TRIGGER trg_salary_hike
BEFORE UPDATE OF salary ON Salary_Hike
FOR EACH ROW
BEGIN
    IF :NEW.salary > :OLD.salary * 1.15 THEN
        RAISE_APPLICATION_ERROR(
            -20001,
            'Salary hike cannot exceed 15% of the old salary.'
        );
    END IF;
END;
/
```

**Result:** The trigger prevents any salary increase greater than 15% of the old salary.


# Problem Statement 9.2

Create an **Employee Payroll Management System in PostgreSQL** using row-level and statement-level triggers.

## Requirements

Create an `employee` table containing the following attributes:

- `emp_id`
- `emp_name`
- `per_hour_salary`
- `working_hours`
- `payable_amount`

Implement the following requirements:

1. Create a **row-level trigger** that automatically calculates `payable_amount` using:

   `per_hour_salary × working_hours`

   The calculation must occur whenever an employee is inserted or updated.

2. The row-level trigger must check whether the calculated `payable_amount` is greater than `25,000`.
   - If it is greater than `25,000`, reject the operation using `RAISE EXCEPTION`.
   - Otherwise, allow the operation.

3. Create a **statement-level trigger** that executes after an `INSERT` or `UPDATE` statement and displays the message:

   `Rows Updated Successfully`

4. Demonstrate the working of both triggers using suitable `INSERT` and `UPDATE` statements, including at least one case where the payable amount exceeds `25,000`.

## SQL Code

### 1. Row-Level Trigger

```sql
CREATE OR REPLACE FUNCTION calculate_payable()
RETURNS TRIGGER
LANGUAGE plpgsql
AS $$
BEGIN
    NEW.payable_amount :=
        NEW.per_hour_salary * NEW.working_hours;

    IF NEW.payable_amount > 25000 THEN
        RAISE EXCEPTION
            'Amount greater than 25000 Not Allowed';
    END IF;

    RETURN NEW;
END;
$$;

CREATE TRIGGER trg_calculate_payable
BEFORE INSERT OR UPDATE ON employee
FOR EACH ROW
EXECUTE FUNCTION calculate_payable();
```

### 2. Statement-Level Trigger

```sql
CREATE OR REPLACE FUNCTION employee_statement_log()
RETURNS TRIGGER
LANGUAGE plpgsql
AS $$
BEGIN
    RAISE NOTICE 'Rows Updated Successfully';
    RETURN NULL;
END;
$$;

CREATE TRIGGER trg_employee_msg
AFTER INSERT OR UPDATE ON employee
FOR EACH STATEMENT
EXECUTE FUNCTION employee_statement_log();
```
