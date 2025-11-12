# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.

**Program:**
```sql
SET SERVEROUTPUT ON;

BEGIN
   EXECUTE IMMEDIATE 'DROP TABLE employee_log';
EXCEPTION WHEN OTHERS THEN NULL;
END;
/
BEGIN
   EXECUTE IMMEDIATE 'DROP TABLE employees';
EXCEPTION WHEN OTHERS THEN NULL;
END;
/

CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    salary NUMBER
);

CREATE TABLE employee_log (
    log_id NUMBER GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    salary NUMBER,
    log_time TIMESTAMP
);

CREATE OR REPLACE TRIGGER trg_log_employee_insert
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
   INSERT INTO employee_log (emp_id, emp_name, salary, log_time)
   VALUES (:NEW.emp_id, :NEW.emp_name, :NEW.salary, SYSTIMESTAMP);

   DBMS_OUTPUT.PUT_LINE('New employee inserted: ' || :NEW.emp_name ||
                        ' | Salary: ' || :NEW.salary);
END;
/

BEGIN
   INSERT INTO employees (emp_id, emp_name, salary)
   VALUES (1, 'John Doe', 5000);

   INSERT INTO employees (emp_id, emp_name, salary)
   VALUES (2, 'Jane Smith', 7000);

   COMMIT;
END;
/

BEGIN
   DBMS_OUTPUT.PUT_LINE('----- Employee Log Table -----');
   FOR r IN (SELECT emp_id, emp_name, salary, log_time FROM employee_log) LOOP
      DBMS_OUTPUT.PUT_LINE('Emp ID: ' || r.emp_id ||
                           ' | Name: ' || r.emp_name ||
                           ' | Salary: ' || r.salary ||
                           ' | Logged at: ' || TO_CHAR(r.log_time, 'DD-MON-YYYY HH24:MI:SS'));
   END LOOP;
END;
/
```

**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

<img width="760" height="361" alt="image" src="https://github.com/user-attachments/assets/2071210e-c379-4012-886e-a6ac13a86d85" />

---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

**Program:**
```sql
SET SERVEROUTPUT ON;

BEGIN
   EXECUTE IMMEDIATE 'DROP TABLE sensitive_data';
EXCEPTION
   WHEN OTHERS THEN NULL;
END;
/

CREATE TABLE sensitive_data (
    id NUMBER PRIMARY KEY,
    info VARCHAR2(100)
);

INSERT INTO sensitive_data VALUES (1, 'Top Secret');
INSERT INTO sensitive_data VALUES (2, 'Confidential');
COMMIT;

CREATE OR REPLACE TRIGGER trg_prevent_delete
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
   RAISE_APPLICATION_ERROR(-20001, 'ERROR: Deletion not allowed on this table.');
END;
/

BEGIN
   DELETE FROM sensitive_data WHERE id = 1;
   COMMIT;
EXCEPTION
   WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('Trigger prevented deletion: ' || SQLERRM);
END;
/
```

**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`

<img width="757" height="373" alt="image" src="https://github.com/user-attachments/assets/98dfc763-fd44-4076-b038-e45eb5ab8412" />

---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

**Program:**
```sql
CREATE TABLE products (
    product_id NUMBER PRIMARY KEY,
    product_name VARCHAR2(50),
    price NUMBER,
    last_modified TIMESTAMP
);

INSERT INTO products VALUES (1, 'Laptop', 60000, NULL);
INSERT INTO products VALUES (2, 'Mobile', 30000, NULL);
COMMIT;

CREATE OR REPLACE TRIGGER trg_update_last_modified
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
   :NEW.last_modified := SYSTIMESTAMP;
END;
/

UPDATE products
SET price = 65000
WHERE product_id = 1;

COLUMN product_id FORMAT 999
COLUMN product_name FORMAT A15
COLUMN price FORMAT 999999
COLUMN last_modified FORMAT A30

SELECT product_id, product_name, price, TO_CHAR(last_modified, 'DD-MON-YYYY HH24:MI:SS') AS last_modified
FROM products;
```

**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.

<img width="760" height="350" alt="image" src="https://github.com/user-attachments/assets/98b19c88-64cd-42f9-8678-c1a8e212cf7c" />

---

## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

**Program:**
```sql
BEGIN
   EXECUTE IMMEDIATE 'DROP TABLE audit_log';
   EXECUTE IMMEDIATE 'DROP TABLE customer_orders';
EXCEPTION
   WHEN OTHERS THEN NULL;
END;
/

CREATE TABLE customer_orders (
    order_id NUMBER PRIMARY KEY,
    customer_name VARCHAR2(50),
    amount NUMBER
);

INSERT INTO customer_orders VALUES (1, 'John Doe', 1000);
INSERT INTO customer_orders VALUES (2, 'Jane Smith', 2000);
COMMIT;

CREATE TABLE audit_log (
    table_name VARCHAR2(50),
    update_count NUMBER DEFAULT 0
);

INSERT INTO audit_log (table_name, update_count)
VALUES ('CUSTOMER_ORDERS', 0);
COMMIT;

CREATE OR REPLACE TRIGGER trg_count_customer_updates
AFTER UPDATE ON customer_orders
BEGIN
   UPDATE audit_log
   SET update_count = update_count + 1
   WHERE table_name = 'CUSTOMER_ORDERS';
END;
/

UPDATE customer_orders SET amount = amount + 100 WHERE order_id = 1;
UPDATE customer_orders SET amount = amount + 200 WHERE order_id = 2;
UPDATE customer_orders SET amount = amount + 300 WHERE order_id = 1;
COMMIT;

SET FEEDBACK OFF
SET VERIFY OFF
SET PAGESIZE 50
COLUMN table_name FORMAT A20
COLUMN update_count FORMAT 9999

SELECT table_name, update_count FROM audit_log;
```

**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.

<img width="751" height="321" alt="image" src="https://github.com/user-attachments/assets/490ae911-2c5c-45f0-8679-f48aaad44933" />

---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

**Program:**
```sql
BEGIN
   EXECUTE IMMEDIATE 'DROP TABLE employees';
EXCEPTION
   WHEN OTHERS THEN NULL;
END;
/

CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    salary NUMBER
);

CREATE OR REPLACE TRIGGER trg_check_salary
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
   IF :NEW.salary < 3000 THEN
      RAISE_APPLICATION_ERROR(-20002, 'ERROR: Salary below minimum threshold.');
   END IF;
END;
/

INSERT INTO employees VALUES (1, 'John Doe', 5000);
INSERT INTO employees VALUES (2, 'Jane Smith', 2500);
```

**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`

<img width="756" height="396" alt="image" src="https://github.com/user-attachments/assets/053fa949-d1e1-4908-b9f8-5325236a40e6" />

## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.

