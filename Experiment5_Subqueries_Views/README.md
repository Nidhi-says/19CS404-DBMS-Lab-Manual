# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
<img width="978" height="507" alt="image" src="https://github.com/user-attachments/assets/32414740-4a5a-4119-8f1e-7d1c0eb0a0c2" />

```sql
select * from Medications
where dosage=(select max(dosage) from Medications);
```

**Output:**

<img width="986" height="472" alt="image" src="https://github.com/user-attachments/assets/798a21fd-ffe2-43c0-9dbc-6452e59c6958" />

**Question 2**
---
<img width="1046" height="692" alt="image" src="https://github.com/user-attachments/assets/ee959e81-8b1e-4a11-8591-6ec1708f2840" />

```sql
select commission from salesman
where salesman_id in(
select salesman_id from customer
where city='Paris');
```

**Output:**

<img width="432" height="408" alt="image" src="https://github.com/user-attachments/assets/b885314c-8cfb-4144-9f74-9ed36a9dfccf" />

**Question 3**
---
<img width="1175" height="725" alt="image" src="https://github.com/user-attachments/assets/930065c5-7711-40c2-8363-d8ec8e7b14cd" />

```sql
select salesman_id, name from salesman
where salesman_id in(
select salesman_id from customer
group by salesman_id
having count(customer_id)>1);
```

**Output:**

<img width="695" height="548" alt="image" src="https://github.com/user-attachments/assets/eaa014c3-f1c8-42e0-aa78-c1aad21c4778" />

**Question 4**
---
<img width="1063" height="562" alt="image" src="https://github.com/user-attachments/assets/58c6b773-ff5f-407f-b6b4-d4e9c478364a" />

```sql
select name from customer
where phone in(
select phone from customer
group by phone
having count(*)=1);
```

**Output:**

<img width="560" height="528" alt="image" src="https://github.com/user-attachments/assets/ee5ec315-c420-437b-8cd8-1be1e0960eeb" />

**Question 5**
---
<img width="1056" height="536" alt="image" src="https://github.com/user-attachments/assets/760253ba-e960-416f-a7a4-7132bde6da35" />

```sql
select * from customer
where city <> (
select city from customer
where id= (select max(id) from customer));
```

**Output:**

<img width="1266" height="568" alt="image" src="https://github.com/user-attachments/assets/bb8480db-ca30-4e9e-b470-73d49abf74d2" />

**Question 6**
---
<img width="1102" height="614" alt="image" src="https://github.com/user-attachments/assets/d2c69b53-90ea-4953-b53d-a2d7b918fc96" />

```sql
select * from Employee
where age < (
select avg(age) from Employee
where income>1000000);
```

**Output:**

<img width="1262" height="505" alt="image" src="https://github.com/user-attachments/assets/91c0b5dd-e13c-4ea2-beec-6a353fda5fd6" />

**Question 7**
---
<img width="1194" height="802" alt="image" src="https://github.com/user-attachments/assets/9addb580-310b-4e5f-8756-3d4bfebcafee" />

```sql
select * from ORDERS
where salesman_id in(
select salesman_id from SALESMAN
where city='New York');
```

**Output:**

<img width="1267" height="556" alt="image" src="https://github.com/user-attachments/assets/c535db60-5816-4593-8de7-af9039107a71" />

**Question 8**
---
<img width="1272" height="630" alt="image" src="https://github.com/user-attachments/assets/64530fab-e4d1-41d6-b0cb-a531a305e3f5" />

```sql
select * from ORDERS
where purch_amt > (
select avg(purch_amt) from ORDERS
where ord_date='2012-10-10');
```

**Output:**

<img width="1259" height="527" alt="image" src="https://github.com/user-attachments/assets/d1f13bc7-0619-4450-95cd-5908f293fc4e" />

**Question 9**
---
<img width="1237" height="815" alt="image" src="https://github.com/user-attachments/assets/d2c2a1d8-6d92-4e45-818c-f49bd9330a36" />

```sql
select ord_no, purch_amt, ord_date, salesman_id from orders
where salesman_id in(
select salesman_id from salesman
where commission=(select max(commission) from salesman));
```

**Output:**

<img width="1049" height="537" alt="image" src="https://github.com/user-attachments/assets/35e4c698-cd5e-4d01-820f-64e179b3ce51" />

**Question 10**
---
<img width="987" height="682" alt="image" src="https://github.com/user-attachments/assets/dd02e0b4-295a-48e0-8d46-5dd70a2aaad9" />

```sql
select * from CUSTOMERS
where SALARY>4500;
```

**Output:**

<img width="1264" height="502" alt="image" src="https://github.com/user-attachments/assets/0ed0528f-fce7-4f49-89de-429f1a28a872" />

## Module Examination (SEB)
<img width="1079" height="73" alt="image" src="https://github.com/user-attachments/assets/24113dff-8424-4294-aca0-5426cdf145f2" />

## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
