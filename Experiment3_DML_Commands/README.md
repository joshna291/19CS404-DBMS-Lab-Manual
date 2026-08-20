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
Write a SQL query to classify value2 in the Calculations table as 'Small', 'Medium', or 'Large' based on whether it is less than 10, between 10 and 50, or greater than 50, respectively.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0


```sql
SELECT
   id,
   value2,
   CASE 
     WHEN value2<10 THEN 'Small'
     WHEN value2 BETWEEN 10 AND 50 THEN 'Medium'
     ELSE 'Large'
    END AS size_category
FROM Calculations;
```

**Output:**

<img width="838" height="442" alt="image" src="https://github.com/user-attachments/assets/65ae1daf-c03d-4325-98da-6a2236711c27" />


**Question 2**
---
Write a SQL query to retrieve the year, month, and day from the hiredate column in the emp table.

For example:

Result
Year        Month       Day
----------  ----------  ----------
1981        04          02
1981        09          28
1981        05          01
1981        06          09
1982        12          09
1981        11          17
1981        09          08

```sql
SELECT 
   strftime('%Y',hiredate) AS Year,
   strftime('%m',hiredate) AS Month,
   strftime('%d',hiredate) AS Day
FROM emp;
```

**Output:**

<img width="810" height="368" alt="image" src="https://github.com/user-attachments/assets/75618528-b9f9-4219-b55a-7af089ef89af" />


**Question 3**
---
Write a SQL query to Delete customers with 'CUST_COUNTRY' 'UK' and 'WORKING_AREA' 'London' whose 'GRADE' is less than 3

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000
```sql
DELETE FROM Customer
WHERE CUST_COUNTRY='UK'
      AND WORKING_AREA='London'
      AND GRADE<3;
```

**Output:**

<img width="1197" height="485" alt="image" src="https://github.com/user-attachments/assets/096105cf-4829-42ec-a6b7-480cec982211" />


**Question 4**
---
Write a query to get information of Employees from EmployeeInfo1 table where the Employee is not assigned to any department.

EmpID

EmpFname

EmpLname

Department

Project

Address

DOB

Gender

1

Sanjay

Mehra

HR

P1

Hyderabad(HYD)

01/12/1976

M

2

Ananya

Mishra

Admin

P2

Delhi(DEL)

02/05/1968



```sql
SELECT*FROM EmployeeInfo1
WHERE Department IS NULL;

```

**Output:**

<img width="1196" height="267" alt="image" src="https://github.com/user-attachments/assets/a9a89427-d5d1-40ea-a5b3-4d9418b2d862" />


**Question 5**
---
Write a SQL query to Delete customers with 'GRADE' 3 and whose 'CUST_NAME' contains the substring 'BBB', and 'PAYMENT_AMT' is greater than 2000

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 

```sql
DELETE FROM Customer
WHERE GRADE=3 AND CUST_NAME LIKE '%BBB%' AND PAYMENT_AMT>2000;
```

**Output:**

<img width="1217" height="528" alt="image" src="https://github.com/user-attachments/assets/89567705-3c85-46b5-81c2-c5bfc4a6cc5e" />


**Question 6**
---
Write a SQL query to remove rows from the table 'customer' with the following condition -

1. 'cust_country' must be 'India',

2. 'cus_city' must not be 'Chennai',

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000
```sql
DELETE FROM customer
WHERE CUST_COUNTRY='India'
AND CUST_CITY<>'Chennai';
```

**Output:**

<img width="1205" height="897" alt="image" src="https://github.com/user-attachments/assets/f6299801-f726-42cd-b304-1e610556681c" />


**Question 7**
---
Write a SQL statement to change salary of employee to 8000 whose Employee ID is 105, if the existing salary is less than 5000.


Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id 
```sql
UPDATE Employees
SET SALARY='8000'
WHERE SALARY<5000 AND EMPLOYEE_ID=105;
```

**Output:**

<img width="1188" height="245" alt="image" src="https://github.com/user-attachments/assets/c1ccb6f8-6f04-422b-805b-533c5fa94d43" />

**Question 8**
---
Write a query to retrieve the EmpFname and EmpLname in a single column as “FullName”. The first name and the last name must be separated with space from EmployeeInfo table.
EmpID

EmpFname

EmpLname

Department

Project

Address

DOB

Gender

1

Sanjay

Mehra

HR

P1

Hyderabad(HYD)

01/12/1976

M

2

Ananya

Mishra

Admin

P2

Delhi(DEL)

02/05/1968

F



```sql
SELECT
  CAST((EmpFname||' '||EmpLname) AS TEXT) AS FullName
FROM EmployeeInfo;
```

**Output:**

<img width="605" height="326" alt="image" src="https://github.com/user-attachments/assets/63aad6fa-373b-4f63-b8f1-4827f8d8cfb4" />


**Question 9**
---
Write a SQL query to identify the top 3 most expensive discounted products. Return product_id, original_price, discount_percentage, and discounted_price.

Sample table: Products

product_id | original_price | discount_percentage

 ------------+----------------+--------------------- 

101 | 50.00 | 0.10 

102 | 150.00 | 0.15 

103 | 200.00 | 0.20 

104 | 300.00 | 0.25

```sql
SELECT
    product_id,
    original_price,
    discount_percentage,
    original_price*(1-discount_percentage) AS discounted_price
FROM Products
ORDER BY discounted_price DESC
LIMIT 3;
```

**Output:**

<img width="1206" height="307" alt="image" src="https://github.com/user-attachments/assets/3674c762-5dcf-4772-b255-eb082169c350" />


**Question 10**
---
Write a SQL statement to update the product_name as 'Grapefruit' whose product_id is 4 in the products table.


products table

---------------
product_id
product_name
category_id
availability 

```sql
UPDATE products
SET product_name='Grapefruit'
WHERE product_id='4';
```

**Output:**

<img width="1210" height="247" alt="image" src="https://github.com/user-attachments/assets/e7bacc47-9123-4bcd-8296-1857f7dd083c" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
