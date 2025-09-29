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
-- Insert a record with EmployeeID 001, Name Sarah Parker, Position Manager, Department HR, and Salary 60000 into the Employee table.

For example:

Test	Result
SELECT * FROM Employee WHERE EmployeeID = 001;
EmployeeID  Name          Position    Department  Salary
----------  ------------  ----------  ----------  ----------
1           Sarah Parker  Manager     HR          60000


```sql
-- INSERT INTO Employee (Employeeid,name,position,department,salary) VALUES ('001','Sarah Parker','Manager','HR',60000) 
```

**Output:**

<img width="1340" height="356" alt="image" src="https://github.com/user-attachments/assets/62552f76-9b0f-49ec-aada-f1f76083108a" />


**Question 2**
---
-- Create a table named ProjectAssignments with the following constraints:
AssignmentID as INTEGER should be the primary key.
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).
AssignmentDate as DATE should be NOT NULL.

Test	Result
INSERT INTO ProjectAssignments (AssignmentID, EmployeeID, ProjectID, AssignmentDate) VALUES (2, 99, 1, '2024-01-03');
Error: FOREIGN KEY constraint failed

```sql
-- CREATE TABLE ProjectAssignments (
AssignmentID INT PRIMARY KEY,
EmployeeID INT ,
ProjectID INT ,
AssignmentDate DATE NOT NULL,
FOREIGN KEY (EmployeeID) REFERENCES 
Employees(EmployeeID), 
FOREIGN KEY (ProjectID) REFERENCES
Projects(ProjectID)
);
```

**Output:**

<img width="1276" height="393" alt="image" src="https://github.com/user-attachments/assets/1db88c51-3f9f-46f0-8ef9-6681ba0905bf" />


**Question 3**
---
-- Write an SQL query to add two new columns, first_name and last_name, to the table employee. Both columns should have a data type of varchar(50).

For example:

Test	Result
pragma table_info('employee');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          integer     0                       0
1           salary      number      0                       0
2           first_name  varchar(50  0                       0
3           last_name   varchar(50  0                       0


```sql
-- PALTER TABLE Employee 
ADD COLUMN first_name varchar(50);
ALTER TABLE Employee 
ADD COLUMN last_name varchar(50);

```

**Output:**

<img width="1250" height="400" alt="image" src="https://github.com/user-attachments/assets/8cad3633-459a-4612-a68e-7d2814e36144" />


**Question 4**
---
-- create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.
For example:

Test	Result
INSERT INTO jobs (job_id, job_title, min_salary, max_salary) VALUES (1, 'Software Engineer', 9000, 15000);
SELECT * FROM jobs;
job_id      job_title          min_salary  max_salary
----------  -----------------  ----------  ----------
1           Software Engineer  9000        15000

```sql
-- CREATE TABLE Jobs(
job_id INT PRIMARY KEY,
job_title VARCHAR(100) DEFAULT" ",
min_salary INT DEFAULT 8000,
max_salary INT DEFAULT NULL
);
```

**Output:**
<img width="1280" height="397" alt="image" src="https://github.com/user-attachments/assets/0cabc9dd-0470-4edc-8adf-c29114e1fc40" />


**Question 5**
---
-- In the Employee table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

EmployeeID  Name          Position    Department  Salary
----------  ------------  ----------  ----------  ----------
5           George Clark  Consultant
7           Noah Davis    Manager     HR          60000
8           Ava Miller    Consultant  IT

```sql
-- INSERT INTO Employee (EmployeeID,Name,Position,Department,Salary)VALUES(5,'George Clark','Consultant',NULL,NULL);
INSERT INTO Employee (EmployeeID,Name,Position,Department,Salary)VALUES(7,'Noah Davis','Manager','HR',60000); 
INSERT INTO Employee (EmployeeID,Name,Position,Department,Salary)VALUES(8,'Ava Miller','Consultant','IT',NULL); 
```

**Output:**

<img width="1271" height="378" alt="image" src="https://github.com/user-attachments/assets/eca2ed38-6089-4ef6-af22-2936a1f67cdc" />

**Question 6**
---
-- Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

For example:

Test	Result
select * from Products;
ProductID   ProductName     Price       Stock
----------  --------------  ----------  ----------
101         Old Smartphone  199.99      0
102         Vintage Laptop  399.99      10
103         Classic Tablet  149.99      5


```sql
--INSERT INTO Products( ProductID, ProductName, Price, Stock )
SELECT  ProductID, ProductName, Price, Stock 
FROM Discontinued_products;
```

**Output:**

<img width="1255" height="429" alt="image" src="https://github.com/user-attachments/assets/7f4a6823-8e75-4978-b109-63786f1bc36e" />


**Question 7**
---
--Create a table named Employees with the following columns:

EmployeeID as INTEGER
FirstName as TEXT
LastName as TEXT
HireDate as DATE
For example:

Test	Result
pragma table_info('Employees');
cid   name        type        notnull     dflt_value  pk
----  ----------  ----------  ----------  ----------  ----------
0     EmployeeID  INTEGER     0                       0
1     FirstName   TEXT        0                       0
2     LastName    TEXT        0                       0
3     HireDate    DATE        0                       0


```sql
-- CREATE TABLE Employees(
EmployeeID INTEGER,
FirstName TEXT,
LastName TEXT,
HireDate DATE

);
```

**Output:**

<img width="1224" height="410" alt="image" src="https://github.com/user-attachments/assets/2561bef1-1abc-43e4-b57f-dcb70e528f61" />


**Question 8**
---
-- Write a SQL query to Add a new column Country as text in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0
For example:

Test	Result
pragma table_info('Student_details');
cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      int         0                       1
1           Name        VARCHAR(10  1                       0
2           Gender      TEXT        1                       0
3           Subject     VARCHAR(30  0                       0
4           MARKS       INT (3)     0                       0
5           Country     TEXT        0                       0


```sql
-- ALTER TABLE Student_details
ADD COLUMN Country TEXT ;
```

**Output:**

<img width="1254" height="469" alt="image" src="https://github.com/user-attachments/assets/36ba488c-081b-479d-816b-51b9089175bd" />


**Question 9**
---
-- Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	Result
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
INSERT INTO Invoices (InvoiceID, InvoiceDate, Amount, DueDate, OrderID) VALUES (1, '2024-08-01', 100.0, '2024-09-01', 1);
SELECT * FROM Invoices;
InvoiceID   InvoiceDate  Amount      DueDate     OrderID
----------  -----------  ----------  ----------  ----------
1           2024--08-01   100.0       2024-09-01  1

```sql
-- CREATE TABLE Invoices(
InvoiceID INTEGER PRIMARY KEY,
InvoiceDate  DATE,
Amount  REAL CHECK (Amount>0),
DueDate  DATE CHECK (DueDate>InvoiceDate),
OrderID  INTEGER,
FOREIGN KEY (OrderID)REFERENCES Orders(OrderID)

);
```

**Output:**

<img width="1213" height="373" alt="image" src="https://github.com/user-attachments/assets/fa35e5f9-79fb-4e98-873a-fe30911c9a34" />


**Question 10**
---
-- Create a table named Products with the following constraints:

ProductID should be the primary key.
ProductName should be NOT NULL.
Price is of real datatype and should be greater than 0.
Stock is of integer datatype and should be greater than or equal to 0.
For example:

Test	Result
INSERT INTO Products
VALUES (1, NULL,0,5);
Error: NOT NULL constraint failed: Products.ProductName


```sql
--CREATE TABLE Products (
ProductID INTEGER PRIMARY KEY,
ProductName TEXT NOT NULL,
Price REAL CHECK(Price>0),
Stock INTEGER CHECK (Stock>=0)


);
```

**Output:**

<img width="1227" height="372" alt="image" src="https://github.com/user-attachments/assets/3b41b598-1cc8-4efb-8a45-d9d2c5509967" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
