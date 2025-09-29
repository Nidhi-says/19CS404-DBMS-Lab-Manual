# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
<img width="1224" height="448" alt="Screenshot 2025-09-29 133540" src="https://github.com/user-attachments/assets/9d93570e-f9f3-4a1f-ac90-26d818ca32ac" />

```sql
create table item(
item_id text primary key,
item_desc text not null,
rate int not null,
icom_id text check(length(icom_id=4)),
foreign key (icom_id) references company(com_id)
on update cascade
on delete cascade
);
```

**Output:**

<img width="1225" height="432" alt="Screenshot 2025-09-29 133628" src="https://github.com/user-attachments/assets/509dcd1f-d1e6-4472-b281-914d50a97510" />

**Question 2**
---
<img width="1223" height="415" alt="Screenshot 2025-09-29 133741" src="https://github.com/user-attachments/assets/7ee652de-a7b7-4e5f-be8a-073a679d5039" />

```sql
create table Events(
EventID INTEGER,
EventName TEXT,
EventDate DATE
);
```

**Output:**

<img width="1226" height="457" alt="Screenshot 2025-09-29 133758" src="https://github.com/user-attachments/assets/21de0bd8-79bf-47ce-a39e-65dbb9e3a7c5" />

**Question 3**
---
<img width="1218" height="470" alt="Screenshot 2025-09-29 133820" src="https://github.com/user-attachments/assets/446b1cc1-2fbd-4bc1-ab71-ac651033662c" />

```sql
insert into Books(ISBN,Title,Author,Publisher,Year)
values('978-1234567890','Introduction to AI','John Doe',null,null),
('978-9876543210','Deep Learning','Jane Doe','TechPress',2022),
('978-1122334455','Cybersecurity Essentials','Alice Smith',null,2021);
```

**Output:**

<img width="1223" height="374" alt="Screenshot 2025-09-29 133836" src="https://github.com/user-attachments/assets/65d89983-8a83-4fff-bb4b-32f1bc2add63" />

**Question 4**
---
<img width="1221" height="438" alt="Screenshot 2025-09-29 133901" src="https://github.com/user-attachments/assets/0ff3e6dd-67ff-424c-8073-6efa61f96824" />

```sql
create table Attendance(
AttendanceID int primary key,
EmployeeID int,
AttendanceDate date,
Status text check(Status in ('Present','Absent','Leave')),
foreign key (EmployeeID) references Employees(EmployeeID)
);
```

**Output:**

<img width="1220" height="367" alt="Screenshot 2025-09-29 133918" src="https://github.com/user-attachments/assets/dc469af3-b9b7-4b48-9e77-4ccd7253176d" />

**Question 5**
---
<img width="1227" height="648" alt="Screenshot 2025-09-29 133940" src="https://github.com/user-attachments/assets/0e90fc9a-f1af-4a85-b7e9-9aa3a96c8192" />

```sql
alter table Student_details add column mobilenumber number
```

**Output:**

<img width="1219" height="446" alt="Screenshot 2025-09-29 133956" src="https://github.com/user-attachments/assets/2c29964b-bea4-4272-89a5-667683279de4" />

**Question 6**
---
<img width="1216" height="480" alt="Screenshot 2025-09-29 134015" src="https://github.com/user-attachments/assets/0f6a46fe-c22b-4c58-bd69-bd9e834d18d5" />

```sql
insert into Student_details(RollNo,Name,Gender)
values(204,'Samuel Black','M');
```

**Output:**

<img width="1218" height="391" alt="Screenshot 2025-09-29 134048" src="https://github.com/user-attachments/assets/bf7498ff-4fd1-41be-a77b-1da4f6bb088c" />

**Question 7**
---
<img width="1223" height="390" alt="Screenshot 2025-09-29 134106" src="https://github.com/user-attachments/assets/d96c4043-a098-44ad-ab78-20427196642f" />

```sql
alter table Employees add column salary INTEGER check(salary>0)
```

**Output:**

<img width="1216" height="372" alt="Screenshot 2025-09-29 134126" src="https://github.com/user-attachments/assets/20667f7c-aae8-479c-9d69-7d5db4ae9ac3" />

**Question 8**
---
<img width="1218" height="402" alt="Screenshot 2025-09-29 134158" src="https://github.com/user-attachments/assets/ae007b2d-aba2-4a12-b26d-b8ba291f7ad4" />

```sql
create table Products(
ProductID int primary key,
ProductName text unique not null,
Price real check(Price>0),
StockQuantity int check(StockQuantity>0)
);
```

**Output:**

<img width="1215" height="365" alt="Screenshot 2025-09-29 134216" src="https://github.com/user-attachments/assets/33b68e9e-b3b6-4d76-a637-9f99bc19c8ce" />

**Question 9**
---
<img width="1216" height="361" alt="Screenshot 2025-09-29 134237" src="https://github.com/user-attachments/assets/a4222c30-00aa-4603-9db0-88ff656149d2" />

```sql
create table Shipments(
ShipmentID int primary key,
ShipmentDate date,
SupplierID int,
OrderID int,
foreign key (SupplierID) references Suppliers(SupplierID)
foreign key (OrderID) references Orders(OrderID)
);
```

**Output:**

<img width="1218" height="322" alt="Screenshot 2025-09-29 134449" src="https://github.com/user-attachments/assets/c180edb2-c221-4a9b-986a-09fe7d6799f9" />

**Question 10**
---
<img width="1217" height="362" alt="Screenshot 2025-09-29 134504" src="https://github.com/user-attachments/assets/bc2beec9-5ede-48b0-a8f9-6cd5f00e321f" />

```sql
insert into Products(ProductID,ProductName,Price,Stock)
select ProductID,ProductName,Price,Stock
from Discontinued_products;
```

**Output:**

<img width="1221" height="376" alt="Screenshot 2025-09-29 134908" src="https://github.com/user-attachments/assets/a97203c6-1b94-4221-a538-db47d5c102ee" />

## Module Examination(SEB):
<img width="1363" height="85" alt="Screenshot 2025-09-29 142843" src="https://github.com/user-attachments/assets/e4ed9fe3-7507-495c-a6e2-60c34604532f" />

## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
