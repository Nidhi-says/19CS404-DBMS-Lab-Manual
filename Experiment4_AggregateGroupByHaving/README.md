# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
<img width="873" height="625" alt="image" src="https://github.com/user-attachments/assets/d6e29477-668a-4d45-8081-b6000f54a9ef" />

```sql
select strftime('%H',AppointmentDateTime) as HourOfDay,count(*) as TotalAppointments from Appointments
group by HourOfDay;
```

**Output:**

<img width="767" height="611" alt="image" src="https://github.com/user-attachments/assets/97353aab-9c18-4f9d-a091-cd31c49d21e6" />

**Question 2**
---
<img width="1076" height="501" alt="image" src="https://github.com/user-attachments/assets/34ffc340-70da-4a9f-9c57-22d13c8b044b" />

```sql
select Address,count(*) as TotalPatients from Patients
group by Address;
```

**Output:**

<img width="677" height="481" alt="image" src="https://github.com/user-attachments/assets/e6533c8d-0bae-47e9-9923-8a10228215d6" />

**Question 3**
---
<img width="1096" height="487" alt="image" src="https://github.com/user-attachments/assets/a940d361-962c-46e6-9903-f2792b24022e" />

```sql
select sum(workhour) as 'Total working hours' from employee1;
```

**Output:**

<img width="571" height="395" alt="image" src="https://github.com/user-attachments/assets/3d361715-ee73-4d1a-a041-9224e6dff43f" />

**Question 4**
---
<img width="784" height="483" alt="image" src="https://github.com/user-attachments/assets/e57dd676-5b8e-44f6-966e-9ea91368a4bc" />

```sql
select avg(length(email)) as avg_email_length from customer;
```

**Output:**

<img width="560" height="377" alt="image" src="https://github.com/user-attachments/assets/cf0e48cd-ec6c-4be0-a3aa-f72c8c70241f" />

**Question 5**
---
<img width="788" height="477" alt="image" src="https://github.com/user-attachments/assets/bd3e4105-265e-4257-959b-81a9b1bc2f58" />

```sql
select count(*) as COUNT from employee
where age>32;
```

**Output:**

<img width="468" height="376" alt="image" src="https://github.com/user-attachments/assets/c3967f0e-c084-4c6f-852b-0b58351f3d24" />

**Question 6**
---
<img width="928" height="507" alt="image" src="https://github.com/user-attachments/assets/49dbdb5d-d298-4812-bf27-3d61d2ce3f08" />

```sql
select (max(price)-min(price)) as price_diff from fruits;
```

**Output:**

<img width="435" height="379" alt="image" src="https://github.com/user-attachments/assets/ed637c32-5a58-43cd-9a4a-266b9d691d37" />

**Question 7**
---
<img width="1197" height="511" alt="image" src="https://github.com/user-attachments/assets/f4f6b8fb-0f66-4efc-9d31-2b78e9f1ff66" />

```sql
select category_id,count(*) as 'count(product_name)' from products
where category_id<3
group by category_id;
```

**Output:**

<img width="786" height="447" alt="image" src="https://github.com/user-attachments/assets/05b1e326-88ea-417b-ad7c-51e8c87cc32a" />

**Question 8**
---
<img width="1219" height="586" alt="image" src="https://github.com/user-attachments/assets/89cea031-f068-4185-a73b-1d16af43702d" />

```sql
select city,sum(income) as Income from employee
group by city
having sum(income)>200000;
```

**Output:**

<img width="630" height="605" alt="image" src="https://github.com/user-attachments/assets/2dfaa77e-1461-44ed-9915-db5aeaff5c38" />

**Question 9**
---
<img width="1218" height="516" alt="image" src="https://github.com/user-attachments/assets/340aad52-419a-4aba-b119-84f8f3a2a9ce" />

```sql
select age, min(income) as 'MIN(income)' from employee
group by age
having min(income)<400000;
```

**Output:**

<img width="628" height="466" alt="image" src="https://github.com/user-attachments/assets/4f2cfb17-6c83-4eb3-9253-00e9d8bb54c8" />

**Question 10**
---
<img width="1218" height="499" alt="image" src="https://github.com/user-attachments/assets/a736d084-f556-454d-87c2-011a02688c96" />

```sql
select (age/5)*5 as age_group, SUM(salary) as 'SUM(salary)'
from customer1
group by (age/5)*5
having SUM(salary)>5000;
```

**Output:**

<img width="642" height="432" alt="image" src="https://github.com/user-attachments/assets/f1f4fcc4-817d-4b42-98c8-4b01d6c46cad" />

## Module Examination (SEB):

<img width="1352" height="111" alt="image" src="https://github.com/user-attachments/assets/fdc39e18-213e-4b6b-880d-5205724ac4ad" />

## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
