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
-- Create a table named Bonuses with the following constraints:
BonusID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
BonusAmount as REAL should be greater than 0.
BonusDate as DATE.
Reason as TEXT should not be NULL.

```
CREATE TABLE Bonuses(
    BonusID INTEGER PRIMARY KEY,
    EmployeeID INTEGER,
    BonusAmount REAL CHECK(BonusAmount>0),
    BonusDate DATE,
    Reason TEXT NOT NULL,
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);
```

**Output:**

<img width="1221" height="292" alt="image" src="https://github.com/user-attachments/assets/4693ac77-c841-41a1-91ff-7df1e12fda3c" />


**Question 2**
---
In the Student_details table, insert a student record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

RollNo      Name            Gender      Subject      MARKS
----------  ------------    ----------  ----------   ----------
205         Olivia Green    F
207         Liam Smith      M           Mathematics  85
208         Sophia Johnson  F           Science

```
INSERT INTO Student_details
VALUES('205','Olivia Green','F',NULL,NULL),('207','Liam Smith','M','Mathematics','85'),('208','Sophia Johnson','F','Science',NULL) 
```

**Output:**

<img width="1206" height="227" alt="image" src="https://github.com/user-attachments/assets/d7bd5f62-2cf3-4c97-b2d7-3dadde24b62d" />


**Question 3**
---
Create a table named Reviews with the following columns:

ReviewID as INTEGER
ProductID as INTEGER
Rating as REAL
ReviewText as TEXT

```
CREATE TABLE Reviews(
ReviewID INTEGER,
ProductID INTEGER,
Rating REAL,
ReviewText TEXT 
);
```

**Output:**

<img width="1198" height="341" alt="image" src="https://github.com/user-attachments/assets/5cd222d1-29e4-4504-adcc-c6184e6d0a66" />


**Question 4**
---
Write a SQL Query  to change the name of attribute "name" to "first_name"  and add mobilenumber as number ,DOB as Date in the table Companies. 

```sql
ALTER TABLE Companies
RENAME COLUMN name TO first_name;
ALTER TABLE Companies 
ADD COLUMN mobilenumber number;
ALTER TABLE Companies 
ADD COLUMN DOB Date;
```

**Output:**

<img width="1152" height="282" alt="image" src="https://github.com/user-attachments/assets/5218eb0f-67c7-4dcc-9019-ccbbacfa753f" />


**Question 5**
---
Insert the below data into the Customers table, allowing the City and ZipCode columns to take their default values.

CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St      

Note: The City and ZipCode columns will use their default values.
 
```sql
INSERT INTO Customers(CustomerID,Name,Address)
VALUES('304','Peter Parker','Spider St') 
```

**Output:**

<img width="1177" height="300" alt="image" src="https://github.com/user-attachments/assets/bffdbda5-bb2f-4a31-aecf-d8cb5826de38" />


**Question 6**
---
Create a table named Employees with the following columns:

EmployeeID as INTEGER
FirstName as TEXT
LastName as TEXT
HireDate as DATE
```sql
CREATE TABLE Employees(
EmployeeID INTEGER,
FirstName TEXT,
LastName TEXT,
HireDate DATE 
);
```

**Output:**

<img width="1227" height="332" alt="image" src="https://github.com/user-attachments/assets/70ece555-7c45-4770-8513-4332265b780a" />


**Question 7**
---
Create a new table named products with the following specifications:
product_id as INTEGER and primary key.
product_name as TEXT and not NULL.
list_price as DECIMAL (10, 2) and not NULL.
discount as DECIMAL (10, 2) with a default value of 0 and not NULL.
A CHECK constraint at the table level to ensure:
list_price is greater than or equal to discount
discount is greater than or equal to 0
list_price is greater than or equal to 0

```sql
CREATE TABLE products(
product_id INTEGER PRIMARY KEY,
product_name TEXT NOT NULL,
list_price DECIMAL(10,2) NOT NULL CHECK(list_price>=0),
discount DECIMAL(10,2) NOT NULL DEFAULT 0 CHECK(discount>=0),
CHECK(list_price>=discount)
);
```

**Output:**

<img width="1211" height="287" alt="image" src="https://github.com/user-attachments/assets/0294682d-f563-4919-914f-ffcffead531e" />


**Question 8**
---
Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.

```sql
CREATE TABLE Products(
ProductID PRIMARY KEY,
ProductName NOT NULL,
Price REAL CHECK(Price>0),
Stock INTEGER CHECK(Stock>=0)
);
```

**Output:**

<img width="1200" height="292" alt="image" src="https://github.com/user-attachments/assets/c4743c1a-1961-4964-8d75-4a4d01b889d4" />


**Question 9**
---
Write a SQL query to Rename the "city" column to "location" in the "customer" table.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002
```sql
ALTER TABLE customer
RENAME COLUMN city TO location;
```

**Output:**

<img width="1217" height="355" alt="image" src="https://github.com/user-attachments/assets/fea637d4-f03b-464c-be7e-1a04390f5b59" />


**Question 10**
---
Insert the following customers into the Customers table:

CustomerID  Name         Address     City        ZipCode
----------  -----------  ----------  ----------  ----------
302         Laura Croft  456 Elm St  Seattle     98101
303         Bruce Wayne  789 Oak St  Gotham      10001

```sql
INSERT INTO Customers
VALUES('302','Laura Croft','456 Elm St','Seattle','98101'),('303','Bruce Wayne','789 Oak St','Gotham','10001') 
```

**Output:**

<img width="1242" height="353" alt="image" src="https://github.com/user-attachments/assets/f7a81c78-83e1-4e4c-aa8e-7796fcd8462a" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
