# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
<img width="732" height="226" alt="Screenshot 2025-10-08 100622" src="https://github.com/user-attachments/assets/739a2127-c555-4166-9f74-a40a70e420e4" />

```sql
update products
set availability=availability*2
where product_id=1;
```

**Output:**

<img width="1218" height="324" alt="Screenshot 2025-10-08 100636" src="https://github.com/user-attachments/assets/b0f22a97-a35c-4ecc-aade-b2655f6b5045" />

**Question 2**
---
<img width="972" height="284" alt="Screenshot 2025-10-08 100654" src="https://github.com/user-attachments/assets/87ae9625-4acc-43ff-9639-f80e179b5bee" />

```sql
update sales
set sell_price=sell_price*1.05
where product_id=15 and sale_date='2023-01-31';
```

**Output:**

<img width="1221" height="529" alt="Screenshot 2025-10-08 100710" src="https://github.com/user-attachments/assets/522795c6-cebf-451f-bb9a-4026296cc25c" />

**Question 3**
---
<img width="1222" height="534" alt="Screenshot 2025-10-08 100728" src="https://github.com/user-attachments/assets/998edbf4-e6c1-449e-bd91-56dfb6401286" />

```sql
update products
set reorder_lvl=reorder_lvl*1.3
where category='Food' and quantity<50;
```

**Output:**

<img width="1213" height="481" alt="Screenshot 2025-10-08 100740" src="https://github.com/user-attachments/assets/aac3c3cd-8d13-44ee-9005-9bf9576e9834" />

**Question 4**
---
<img width="1212" height="638" alt="image" src="https://github.com/user-attachments/assets/2bed2890-2643-4894-a5b7-1e1a675efd5c" />

```sql
delete from Customer
where WORKING_AREA='New York';
```

**Output:**

<img width="1218" height="801" alt="image" src="https://github.com/user-attachments/assets/c0193e17-76a3-40c1-8639-3c9d2fc87212" />

**Question 5**
---
<img width="1221" height="538" alt="image" src="https://github.com/user-attachments/assets/d746b110-3574-4266-9e30-a1a8c2203c1a" />

```sql
delete from Doctors
where specialization in ('Pediatrics','Cardiology') and last_name='Brown';
```

**Output:**

<img width="1217" height="853" alt="image" src="https://github.com/user-attachments/assets/162a68e4-c842-4650-aeb6-07de52e8d71d" />

**Question 6**
---
<img width="834" height="536" alt="image" src="https://github.com/user-attachments/assets/d9a1d799-dde4-43d8-b784-c622ba938143" />

```sql
delete from Doctors
where specialization is null;
```

**Output:**

<img width="1226" height="815" alt="image" src="https://github.com/user-attachments/assets/e66a405a-5b3f-4400-9087-a9cf787c0a0b" />

**Question 7**
---
<img width="855" height="468" alt="image" src="https://github.com/user-attachments/assets/c4ae27ad-e1f9-4306-8de1-8820e3f36cab" />

```sql
select * from EmployeePosition
order by Salary desc
limit 3;
```

**Output:**

<img width="1227" height="351" alt="image" src="https://github.com/user-attachments/assets/c4d1f35b-e12e-4886-b6fd-dd129f272064" />

**Question 8**
---
<img width="974" height="492" alt="image" src="https://github.com/user-attachments/assets/f62f8e75-a89c-4b6e-baf1-5a0fed06bab6" />

```sql
select * from EmployeeInfo
where EmpID between 5 and 9;
```

**Output:**

<img width="1212" height="322" alt="image" src="https://github.com/user-attachments/assets/8da37a97-1bb3-4278-be07-dae81494500f" />

**Question 9**
---
<img width="1216" height="558" alt="image" src="https://github.com/user-attachments/assets/bb55ab51-889b-49c8-b072-0715eca0885e" />

```sql
select customer_id,city,grade,
case
when grade>=300 then 'High Rating'
else 'Low Rating'
end as Rating
from customer
order by customer_id asc;
```

**Output:**

<img width="1215" height="613" alt="image" src="https://github.com/user-attachments/assets/5f0320b9-15be-4375-8047-7115df251950" />

**Question 10**
---
<img width="1210" height="487" alt="image" src="https://github.com/user-attachments/assets/285c339e-f549-499d-b9ba-a72808a520e8" />

```sql
select * from customer
where city='New York' or grade<=100;
```

**Output:**

<img width="1215" height="506" alt="image" src="https://github.com/user-attachments/assets/40db4c67-137e-492a-ac53-9d39a68b828d" />

## Module Examination (SEB):

<img width="1345" height="78" alt="image" src="https://github.com/user-attachments/assets/75799fd6-2122-4732-85c8-93c3f23d375e" />

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
